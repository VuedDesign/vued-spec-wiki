---
name: Figma 插件集成规范 Plugin Integration
type: meta
last_updated: 2026-09-23
---

# Figma 插件集成规范

> 本文档定义 Figma 审核插件如何加载、路由、执行本 Wiki 的规则集。任何 Wiki 内规则的结构性变更，都需要与本文档同步。

---

## 一、插件的规则加载策略

### 加载入口

插件启动时读取 `vued-spec-wiki/_meta/plugin-integration.md`（本文件）+ 各 App 的 `_index.md`，得知规则清单。

### 过滤条件

只加载满足以下条件的规范文档：

- `frontmatter.figma_plugin_active: true`
- `frontmatter.status: production`
- 用户当前设计文件所属的 App（Ctrip / Trip）

### 路由规则

按 `frontmatter.app` 分桶：

- 当前审核的设计文件被标注为 Ctrip → 加载所有 `app: ctrip` 或 `app: shared` 的规范
- 被标注为 Trip → 加载所有 `app: trip` 或 `app: shared` 的规范
- 未标注时 → 提示用户选择

### 规范优先级

同一 App 内采用：**brand / feature 专属规范认领优先，general 规范兜底**。目录层级用于组织内容，不代表规则可以叠加执行。专属规范引用 general Token 时，只复用 Token 名称与基础值，不继承 general 的场景审核逻辑。

---

## 二、规则执行顺序

插件必须先完成“专属认领”，再执行“通用兜底”。不得仅按 general → brand → feature 的目录顺序依次叠加规则。

1. **收集专属规范 (Collect Dedicated Rules)**
   - 加载当前 App 下所有 `scope: brand` 与 `scope: feature` 的生产规则
   - 对每个待校验图层执行相应的 `scope_gate` / Hit Test
2. **建立图层管辖映射 (Ownership Map)**
   - 命中专属作用域 → 记录该图层及其被认领子树的 owner
   - 未命中 → owner 为空，保留给 general 兜底
   - 同一图层命中多个专属规范时，选择作用域更具体者；无法唯一判定时报告路由冲突，不叠加执行
3. **执行专属规则 (Dedicated Validation)**
   - 对 owner 不为空的图层，仅执行其 owner 对应的 brand / feature 规则
   - 专属页面引用 general Token，仅用于解析 Token 名称和基础值，不触发 general 的语义审核条件
4. **执行通用规则 (General Fallback)**
   - 对 owner 为空的图层执行 general 图层级规则
   - owner 不为空的图层必须从 general 图层级校验中排除，避免重复或矛盾报错
5. **执行全局占比规则 (Global Rules)**
   - 以顶级 Frame / Module 为校验单元，按各 general 页面明示的统计口径计算
   - 专属图层是否进入分子或分母，必须由对应全局规则明确声明；未声明时不得自行推断
6. **报错聚合**
   - 收集所有触发规则，记录规则来源与 owner
   - 按严重程度（error / warning）分组呈现

---

## 三、判定条件的转译约定

Wiki 里 "插件触发条件" 的自然语言表述如何转成 JS 校验：

### 常见模式

| 自然语言 | JS 实现建议 |
|---|---|
| "图层色值为 #XXXXXX" | `layer.fills[0].color === '#XXXXXX'` |
| "图层/父级名称包含 X" | `layer.name.includes('X') \|\| layer.parent.name.includes('X')` |
| "字符数 > 20" | `layer.characters.length > 20` |
| "字号 ≥ 18px 且字重 ≥ Bold" | `layer.fontSize >= 18 && layer.fontWeight >= 700` |
| "对比度 < 4.5:1" | `contrastRatio(fg, bg) < 4.5` |
| "面积占比 < 60%" | 累加子图层 `bbox.area` / 父级 `bbox.area` |
| "组件名匹配 `Ctrip-Self/*`" | `layer.mainComponent?.name.startsWith('Ctrip-Self/')` |

### 关键词库（Keyword Registry）

Wiki 里频繁出现的关键词（`Link`、`Button`、`Error`、`Placeholder` 等），插件应维护统一的正则表，避免每份规范单独实现。**建议表位置**：`plugin/src/keyword-registry.ts`。

---

## 四、报错文案的引用方式

Wiki 里"插件报错文案"章节的文字应作为**模板**注册到插件，通过规则 ID 引用：

```javascript
{
  ruleId: 'ctrip-info-color/blue-1/rule-A',
  severity: 'warning',
  messageTemplate: '文本字数过长：不建议大段使用 Blue-1，建议更换为 Token/Black-1 (#111111)。'
}
```

**变更同步**：Wiki 里报错文案改了，插件端必须重新同步。建议加自动化脚本。

---

## 五、准确率与回归

- 每份规范 frontmatter 中 `accuracy_baseline` 字段是**实测基线**
- 每次规范修订后，回归测试集应验证准确率**不低于** baseline
- 若准确率降低，需在 [[_meta/conflicts]] 里说明并调整规则

---

## 六、当前投产规范

| 规范 | 版本 | Baseline | 状态 |
|---|---|---|---|
| [[ctrip/general/info-color]] | 1.7 | 0.90 | production |
| [[ctrip/brand/ctrip-self]] | 1.5 | 0.90 | production |

---

## 七、待补的插件工程侧任务

- [ ] Frontmatter 解析器（YAML → 内存规则集）
- [ ] 关键词正则库（keyword-registry）
- [ ] 报错文案模板加载器
- [ ] 面积占比计算引擎（用于 general 层全局规则）
- [ ] Hit Test 引擎（用于 brand 层作用域判定）
- [ ] 生成规则的加载路径（未来支持"生成合规稿"能力时使用）
