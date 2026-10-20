---
name: Figma 插件集成规范 Plugin Integration
type: meta
last_updated: 2026-10-20
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

> **Wiki 现行正式规范、插件待接入**：[[ctrip/general/info-color-v1-8]] v1.8 在 Black-3 移除录入项占位用途，并新增 `Token/Black-5 (#C5C5C5)` 用于查询框／表单等录入项暗提示；灰色背景上若默认色可读性差，可由设计师加深至 `Token/Black-4 (#AAAAAA)`，没有机器阈值，不把条件例外编成自动报错。该页当前 `status: production`、`figma_plugin_active: false`；现有插件仍使用上表 v1.7 基线。插件负责人须先落实可靠的暗提示身份识别、正反样本和与既有 Black-1／Black-3 规则的回归，再单独接入并启用 v1.8。不要把 v1.7 的 0.90 实测基线挪到 v1.8。现行 v1.8 另按用户澄清将 Orange-1 定位为重点提醒（`Attention`）、Red-1 定位为更高等级警示（`Warning`／`Alert`）；仅图层名中的 `Warning` 字样不能自动决定层级，含义不明时人工复核，禁用态不能一律导向 Red；Orange 用于禁用文字时的 Black-3 仅作人工复核建议，不自动报错或强制替换。用户已确认热卖（Hot）与即将售罄场景可使用 `Token/Red-1 (#F5190A)`；插件识别需可靠业务证据，不能仅靠文字包含 `Hot`。

> **Trip 信息色彩 v1.6 Wiki 正式稿、插件待接入**：[[trip/general/info-color]] v1.6 已按 Trip 原稿与用户澄清定稿，当前 `status: production`、`figma_plugin_active: false`；不能把 Wiki 定稿当作插件已上线。用户已确认 `Score` 为点评分、`Hot Score` 为景点热度分，按精确命名及更具体的 `Hot Score` 归属优先处理，旧 `includes("Score")` 规则不得自动使用；插件仍需回归。用户也确认全局辅助／功能／专有色 `<10%` 包含 Rate、Trip Best 和 Discount；Discount 自身另有 `<5%` 理想参考目标，两项比例分别观察但均非强制报错／警示，分母已按所有信息文字与图标的可见面积总和确认。减价／优惠数值归 `color-accent-discount (#D81E60)`，静态品牌色需依据官方品牌专属组件身份而非 `Logo`／`Brand`／`Header` 名称关键词；#003–#006 已归档。用户进一步确认 Trip Best 先过官方组件／Logo 身份，信息色只检查文字与图标，背景填充不进入分子；第 9 节按 Token 独立重排 Neutral Primary／Secondary／Tertiary／color-text-Placeholder，保留原稿触发语义；录入项暗提示 `color-text-Placeholder (#6F7685)` 与 `color-text-tertiary (#6F7685)` 同色但为用户确认的官方组件中两个实际 Token，需可靠读取组件 Token／变量绑定身份；无法读取时人工复核，不单凭 Hex 判错。全局中性色 `>60%`、主色 `<30%`、功能／专有色 `<10%` 与 Discount 额外 `<5%` 均以所有可见信息文字与图标的面积总和为分母，**仅能作为特殊场景可偏离的非阻断设计师提醒，不得生成报错或警示**；#007 已归档。插件仍需核验实际组件身份、面积计算与正反样本；不得仅因原稿已有“插件触发条件”就将其投产，也不得用 Ctrip 规则填补 Trip 未决口径。

### Wiki 正式、插件待接入

- [[ctrip/brand/ctrip-select]] v1.1：`status: production`、`figma_plugin_active: false`。内容已定稿供查询，**当前不进入插件自动规则集**；实际接入、回归、发布及实测基线由插件负责人完成，不能借用携程自营的 0.90 基线。
- 该页记录了优选专属作用域判定和 Logo / 标签 / 筛选 / Banner / 品牌页候选规则，8 个条目均列出 target、规则 A/B 和对应反馈；其中部分 B 为人工复核而非自动报错。当前只有官方优选组件身份可靠命中；手绘近似、未登记的插件标记与普通图层名称不能作为自动 Hit。用户确认的优选品牌文字五色清单已归档：`Token/Blue-1 (#006FF6)`、`Token/Black-1 (#111111)`、`Token/Black-2 (#555555)`、`Token/Black-3 (#888888)`、`Token/White (#FFFFFF)`。它与图形勾 `Token/Orange-1 (#FF5500)` 的局部用途分开。用户已确认：官方优选品牌页／浮层优势信息组的标题与正文以组件的 `Token/Black-1 (#111111)` 为准，原稿蓝色赞只是图标示意、组件默认图标须按当前句子含义替换；信息组图标与文字色不再是冲突。此精确文字色仅适用于可靠识别的信息组标题／正文，优先于五色候选清单；本版白色反白 Logo 仅用于官方蓝底面性标签；其余可靠归属的优选品牌文字可在五色清单内由设计师自行选用，不设固定文字角色或背景映射，且不能自动继承自营的语义审核条件。组件 Key 只作为 `_sources/ctrip/brand/ctrip-select-figma-inspection-2026-10-13.md` 的核对证据。筛选中的官方完整矢量 Logo 本体可独立命中第 1 条规则，不要求独立 Filter Chip 身份，也不设“删掉 Logo 只剩优选文字”的漏用规则。插件投产前仍须确认未登记矢量的身份边界、混合容器及面积统计口径，建立品牌文字与信息组节点角色识别，生成正反样本并回归；不得仅因 Wiki 定稿就声称插件已上线。


**携程优选插件转译的自营参考边界**：借鉴“先官方身份 Hit → 建立 Ownership Map → 只检查被认领 target → 用正反例回归”的执行顺序；不复制 `Ctrip-Self/*` 组件路径、图形结构／比例阈值、`plugin-data` 标记、白色 Logo 深底条件、金色规则、ΔE 阈值或 50 字硬上限。优选官方品牌页／浮层只认领已定义的品牌结构与优势信息组；普通卡片或普通筛选容器内的官方优选 Logo 只认领 Logo 本体，不能扩散到外层容器。未登记手工矢量的身份、反白 Logo 承载组件身份、混合字符计数、混合容器全局面积口径均维持人工复核，不因自营已投产而自动补全优选的插件实现。正反样本清单见 [[ctrip/brand/ctrip-select]] 第三章末尾。

---

## 七、待补的插件工程侧任务

- [ ] Frontmatter 解析器（YAML → 内存规则集）
- [ ] 关键词正则库（keyword-registry）
- [ ] 报错文案模板加载器
- [ ] 面积占比计算引擎（用于 general 层全局规则）
- [ ] Hit Test 引擎（用于 brand 层作用域判定）
- [ ] 生成规则的加载路径（未来支持"生成合规稿"能力时使用）
