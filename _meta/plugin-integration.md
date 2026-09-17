---
name: Figma 插件集成规范 Plugin Integration
type: meta
last_updated: 2026-09-11
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

---

## 二、规则执行顺序

对每个待校验图层，按以下顺序执行：

1. **作用域判定 (Scope Gate)**
   - 若某规范 frontmatter 有 `scope_gate` 字段（如"携程自营"的 Hit Test），先执行判定
   - 未通过判定 → 跳过整份规范
2. **全局占比规则 (Global Rules)**
   - 以顶级 Frame / Module 为单元
   - 累加面积后计算比例
   - 只对 general 层规范触发
3. **图层级 Token 规则 (Layer-Level Rules)**
   - 逐图层遍历
   - 按各规范的"插件触发条件"章节判定
4. **报错聚合**
   - 收集所有触发的规则
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
