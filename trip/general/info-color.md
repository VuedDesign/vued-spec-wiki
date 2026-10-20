---
id: trip-info-color
name: Trip 信息色彩规范 v1.6
version: "1.6"
app: trip
scope: general
category: color
status: production
last_updated: 2026-10-20
figma_plugin_active: false
related:
  - trip/_index
  - _meta/plugin-integration
  - _meta/conflicts
sources:
  - _sources/trip/general/trip-info-color-v1.6-2026-10-20.md
  - _sources/trip/general/trip-score-name-clarification-2026-10-20.md
  - _sources/trip/general/trip-color-scope-clarification-2026-10-20.md
  - _sources/trip/general/trip-best-info-scope-clarification-2026-10-20.md
  - _sources/trip/general/trip-placeholder-clarification-2026-10-20.md
  - _sources/trip/general/trip-area-ratio-clarification-2026-10-20.md
tags: [color, token, trip, plugin-rule]
---

# Trip 信息色彩规范 1.6

> **本页已定稿为 Trip Wiki 信息色彩规范；Figma 插件尚未接入。** 内容取自 Trip v1.6 原稿和用户后续澄清；Ctrip 只供对照文档结构，不是 Trip 色值或审核逻辑来源。图层级语义规则为正式 Wiki 口径，插件触发与反馈为负责人待实现、待回归的转译约定；面积比例仅作非阻断的设计师提醒，**不生成报错或警示**。处理记录见 [[_meta/conflicts]] 已归档 #003–#007。

**规则路由与校验对象**：先确认 App 是 Trip，再判定图层是否已由 Trip 的 brand／feature 专属规范认领；本篇只观察**信息文字与图标的可见颜色**，**不审核背景填充**。图层级 Token 语义规则仅兜底未被 Trip brand／feature 专属规范认领的目标；页面／模块的非阻断色彩构成可观察其中**所有信息文字与图标**，但不会对专属图层重复执行 general 的图层级审核。若以后新增更具体的 Trip 品牌或功能规范，应先核对本页静态品牌色、Trip Best 等专有色的归属，避免两处规则叠加；本页不继承任何 Ctrip 业务语义。

### 核心校验逻辑与全局规则 (Global Rules)

**观察范围与分母**：以原稿的顶级 Frame／Page／独立内容模块为观察单元。该单元中**所有可见信息文字与图标的面积总和**是分母；背景填充不计入。各颜色类别的分子只累加同一单元中对应颜色的信息文字与图标。若单元没有可统计的信息文字／图标，则不计算比例。

**比例的性质**：下列数值是体验上的**理想参考目标**，不是强制上限或下限。偏离目标时最多给设计师**非阻断的信息性提醒**；特殊场景可合理超出。所有面积比例均**不生成报错或警示**，也不改变 brand／feature 对图层级规则的管辖权。

|全局属性分类|色彩 Token 类型|理想面积比例|观察逻辑（非报错／警示）|给设计师的信息性提醒|
|---|---|---|---|---|
|**中性色**|`Neutral/*`, `color-text-Placeholder`|**>60%**|该类信息文字与图标的可见面积／本单元全部信息文字与图标的可见面积；包含录入项暗提示 `color-text-Placeholder (#6F7685)`。|**可检查中性色层级**：中性色信息占比偏离理想参考值时，请结合页面目的判断是否调整；特殊场景可保留现状。|
|**主色**|`Brand`|**<30%**|Brand 类信息文字与图标的可见面积／同一分母。|**可检查主色聚焦**：主色信息占比偏离理想参考值时，请结合重点信息判断是否调整。|
|**辅助／功能色／专有色**|`Functional/*`, `Discount`, `color-specific-rate`, `color-specific-trip-best`|**<10%**|上述颜色的文字与图标可见面积合计／同一分母；`color-accent-discount (#D81E60)` 计入合计且在合计中只计一次，同时另看自身 <5% 的理想参考目标。|**可检查强调色密度**：该类信息占比偏离理想参考值时，请按体验诉求判断；特殊场景可超出，不报错、不发警示。|

> 单个 Banner、Tag、字段不单独作为全局观察单元，其信息文字与图标仍计入所属页面／模块；背景不计入。原稿中的品牌／营销特殊页面例外保留作为设计师判断依据，但本版任何场景都不会因面积比例偏离而报错或发警示。

---


### 图层级 Token 校验字典 (Layer Logic Rules)



以下为具体的颜色知识库，包含来源所提供的 **Figma Token ID、Hex、语义与候选判定、反馈文案**；原稿未列 RGB／OKLCH 数值，本页不自行计算或补造。



### 1. 品牌色 Brand Color (Static)



> **定义**：Trip 静态品牌色，仅用于极少数全局强品牌感知的场景。
>
>



- **Token ID**: `color-brand-static-blue` \| `color-brand-static-yellow`

- **Hex 映射**: `#2346FF` \(TripBlue\) \| `#FFB400` \(TripYellow\)

- **语义标签**：`Brand Identifier` / `Logo` / `Brand Banner` / `Copyright`

|维度|条件定义与判定逻辑 \(Plugin Rules Engine\)|
|---|---|
|**推荐场景 \(DO\)**|文字或图标位于官方 Trip 品牌专属组件内（如：`Header/Logo`、`Card/BrandBanner`、`Footer/CopyRight`）；组件背景填充不在本页校验范围。|
|**禁用场景 \(DON'T\)**|常规 UI 控件（按钮、常规标签、图标、正文、背景）。|
|**插件触发条件**|**前置身份**：仅对确认属于 Trip App 的图层检查；先核对是否位于**官方 Trip 品牌专属组件**内，如 `Header/Logo`、`Card/BrandBanner`、`Footer/CopyRight` 的官方实例。组件／主组件身份可靠时优先，普通图层仅因名称含 `Logo`、`Brand`、`Header` 或 `Footer` 不能被自动认领。<br>**规则 A（静态品牌色越界）**：target 使用 `color-brand-static-blue (#2346FF)` 或 `color-brand-static-yellow (#FFB400)`，且可靠确认不属于官方 Trip 品牌专属组件 → 候选报错；身份不明先人工复核，不能误报合法的官方 `Footer/CopyRight`。|
|**插件报错文案**|情况 A：**Trip 静态品牌色误用**：`color-brand-static-blue (#2346FF)`／`color-brand-static-yellow (#FFB400)` 仅用于已确认的 Trip 官方品牌专属组件（含官方 `Footer/CopyRight`），不用于普通 UI 控件；需要交互主色时请核对 `color-brand-primary (#2C61FE)`。组件身份无法核对时先人工复核，不自动报错。|



---



### 2. 交互主色 Primary Color (UI Blue)



> **定义**：页面引导用户操作的核心视觉焦点与价格显示。
>
>



- **Token ID**: `color-brand-primary`

- **Hex 映射**: `#2C61FE`

- **语义标签**：`Primary Action` / `Text Link` / `Price Highlight` / `Focus State`

|维度|条件定义与判定逻辑 \(Plugin Rules Engine\)|
|---|---|
|**推荐场景 \(DO\)**|1\. 关键行动点 \(Primary Button\)<br>2\. 文本链接 \(Text Link\)<br>3\. 价格数字 \(Price\)<br>4\. 品宣高亮/图标高亮|
|**禁用场景 \(DON'T\)**|用于产能、服务力、履约能力等保障性/描述性信息。|
|**插件触发条件**|图层或其父级名称包含 `Service`, `Facility`, `Guarantee`（服务/设施/保障），却使用了 `#2C61FE`。|
|**插件报错文案**|**主色语义误用**：主色 `Brand` 不可用于服务力或设施保障类信息。请改用中性色 `Neutral/Primary (#121826)` 或辅助色。|



---



### 3. 功能色 - 积极 Positive (Cyan)



> **定义**：用于传递对用户有利的正向信息及低价区间；减价／优惠数值已由用户确认使用第 6 节 `color-accent-discount (#D81E60)`。
>
>



- **Token ID**: `color-functional-positive`

- **Hex 映射**: `#047C88`

- **语义标签**：`Positive Status` / `Low Price Range`

|维度|条件定义与判定逻辑 \(Plugin Rules Engine\)|
|---|---|
|**推荐场景 \(DO\)**|1\. 利好信息标签（如：“免费取消”、“含早餐”）<br>2\. 价格区间中的“低价区间”标识；减价／优惠数值不在本节，见第 6 节 Discount|
|**禁用场景 \(DON'T\)**|警示信息、报错、价格上涨、非利好客观描述，以及已确认属于减价／优惠数值的图层（应使用 Discount）。|
|**插件触发条件**|**规则 A（不利语义误用）**：target 已可靠确认为加价、价格上涨、高价或警示／报错场景，却使用 `color-functional-positive (#047C88)` → 候选报错；仅凭 `+` 字符或名称关键词而无业务上下文时人工复核。<br>**规则 B（减价色归属）**：target 已确认是价格明细里的减价／优惠数值，却使用 `color-functional-positive (#047C88)` → 候选报错，改按第 6 节 `color-accent-discount (#D81E60)`；不得因同一图层亦可称“利好”而重复执行两套颜色规则。|
|**插件报错文案**|情况 A：**Positive 语义误用**：`color-functional-positive (#047C88)` 用于利好信息和低价区间，当前经确认属于负向／涨价／警示场景，请核对。<br>情况 B：**减价数值用色错误**：经确认的减价／优惠数值应使用 `color-accent-discount (#D81E60)`，而非 `color-functional-positive (#047C88)`。|



---



### 4. 功能色 - 警示 Warning (Orange)



> **定义**：提醒用户关注，否则可能影响出行/入住，或表示价格中等/上涨。
>
>



- **Token ID**: `color-functional-warning`

- **Hex 映射**: `#C74401`

- **语义标签**：`Caution Notice` / `Price Increase` / `Medium Price Range` / `Risk Alert`

|维度|条件定义与判定逻辑 \(Plugin Rules Engine\)|
|---|---|
|**推荐场景 \(DO\)**|1\. 需关注的出行提醒（如：“需办理过境签”）<br>2\. 供应商/航司导致的价格自然上涨<br>3\. 价格划分中的“中价区间”|
|**禁用场景 \(DON'T\)**|致命阻断性错误、促销优惠信息、无风险的普通描述。|
|**插件触发条件**|图层文本包含 `-` \(减价\) 或图层名包含 `Success`, `Discount`，却使用了 `#C74401`。|
|**插件报错文案**|**警示色误用**：橙色 `Warning` 用于表达需关注的风险或中价区间，不可用于优惠促销或成功提示。|



---



### 5. 功能色 - 严重警告/热门 Alert & Popular (Red)



> **定义**：极高风险阻断信息、高价区间、报错及热卖标。
>
>



- **Token ID**: `color-functional-danger`

- **Hex 映射**: `#D02C2A`

- **语义标签**: `Critical Alert` / `System Error` / `High Price Range` / `Popular Badge` / `Popularity Score`

- **热度分身份**：用户确认景点热度分叫 `Hot Score`；若其内部另有名为 `Score` 的子图层，先按更具体的 `Hot Score` 归属判断，不以 `Score` 子串误认成点评分。业务组件身份与名称冲突时先人工复核。

|维度|条件定义与判定逻辑 \(Plugin Rules Engine\)|
|---|---|
|**推荐场景 \(DO\)**|1\. 影响出行成功与否的严重阻断信息<br>2\. 价格划分中的“高价区间”<br>3\. 系统 Error 报错提示<br>4\. 热门/热卖商品 Badge（如：“Selling Fast”）<br>5\.商品即将售罄（如Only 1 left at this price）<br>6\. 热度分（`Hot Score`），0\.1 到 10 的景点热度分数；按本节 `color-functional-danger (#D02C2A)` 用色|
|**禁用场景 \(DON'T\)**|普通提示、减价优惠、无风险的客观描述。|
|**插件触发条件**|**规则 A（高警示色误用）**：target 使用 `color-functional-danger (#D02C2A)`，但已可靠确认既非严重阻断／系统错误、高价区间、热卖／即将售罄场景，也非景点热度分 `Hot Score` → 候选报错；归属无法确认先人工复核。<br>**规则 B（Hot Score 未用热度分色）**：target 或已确认的所属组件**精确名为** `Hot Score`，且确认是景点热度分，最终色值 ≠ `color-functional-danger (#D02C2A)` → 候选提示。若祖先为 `Hot Score` 而子图层名为 `Score`，优先按热度分处理，不触发第 7 节点评分规则。仅名称包含 `Score` 的其他节点不自动命中。|
|**插件报错文案**|情况 A：**高警示色滥用**：`color-functional-danger (#D02C2A)` 用于严重阻断／报错、高价区、热卖／即将售罄及景点热度分；已确认的普通提示不属于这些场景，请按实际语义核对。<br>情况 B：**热度分颜色请核对**（待启用）：已确认的 `Hot Score` 景点热度分按本节使用 `color-functional-danger (#D02C2A)`，不要将它当作点评分 `Score`。|



---



### 6. 功能色 - 促销/收藏 Discount (Pink)



> **定义**：促销折扣与收藏（Heart）专有颜色；面积比例是可因特殊场景调整的理想参考目标。
>
>



- **Token ID**: `color-accent-discount`

- **Hex 映射**: `#D81E60`

- **语义标签**：`Promotion Discount` / `Favorite Heart`

- **双层面积参考**：`color-accent-discount (#D81E60)` 计入功能／专有色理想合计 `<10%`，同时另看自身理想占比 `<5%`。两项分别供设计师参考，5% 不替代 10%；特殊场景均可合理超出，**不触发报错或警示**。分母均为本单元所有信息文字与图标的可见面积之和。

|维度|条件定义与判定逻辑 \(Plugin Rules Engine\)|
|---|---|
|**推荐场景 \(DO\)**|1\. 促销／折扣直接相关的 Tag、文字及价格明细中的减价／优惠数值（如 `20% OFF`、`-$20`）<br>2\. 商品收藏 Icon \(Heart/Favorite\)|
|**禁用场景 \(DON'T\)**|用于无折扣的普通价格或描述；自身超过 5% 仅偏离理想比例，不是本行的禁用错误。|
|**插件触发条件**|**规则 A（面积参考提醒，非报错／警示）**：仅统计页面／模块内 `color-accent-discount (#D81E60)` 的信息文字与图标可见面积，除以**该单元所有信息文字与图标的可见面积之和**；偏离理想 `<5%` 时可向设计师展示非阻断提醒。Discount 同时进入功能／专有色理想 `<10%` 合计，两项比例分别观察；特殊场景可超出，**不得生成错误或警示**。<br>**规则 B（非法使用）**：已确认非折扣／减价／优惠数值或非收藏图层使用 `color-accent-discount (#D81E60)` → 候选报错；身份不明时人工复核。|
|**设计师面积提醒文案**|情况 A（非报错／警示）：`color-accent-discount (#D81E60)` 自身信息色占比高于理想的 5%；请结合体验目标判断是否需要精简，特殊场景可保持当前方案。|
|**插件报错文案**|情况 B（语义误用）：`color-accent-discount (#D81E60)` 用于促销／折扣、减价／优惠数值或收藏图标；已确认的普通无折扣价格／描述请使用对应规范色。|



---

### 7. 专有色 - 点评分 Rate (Indigo Blue) 【严格独占规则】



> **定义**：点评分（Rating Score）的**唯一**专有颜色，具备双向排他性。用户确认点评分目标名为 `Score`，景点热度分名为 `Hot Score`；后者优先，不因包含 `Score` 子串而继承点评分规则。
>
>



- **Token ID**: `color-specific-rate`

- **Hex 映射**: `#173CD2`

- **语义标签**：`Rating Score` / `Rating Tag` \(专属独占\)

|维度|条件定义与判定逻辑 \(Plugin Rules Engine\)|
|---|---|
|**推荐场景 \(DO\)**|**有且仅有**：0\.1到5\.0点评分数文本。形式上可以带分母如4\.9/5，可以单分子加单位，如4\.9分。评分后可衔接分数形容词，超棒、很好、满意、不错等等。点评分 Tag 内的分数文字／图标；Tag 背景填充不属于本页校验。经确认的点评分目标名为 `Score`。|
|**禁用场景 \(DON'T\)**|1\. 已确认的点评分目标不得使用非 `color-specific-rate (#173CD2)` 色值。<br>2\. `color-specific-rate (#173CD2)` 不得用于已确认的非点评分元素，尤其不能误用于 `Hot Score` 热度分。<br>3\. `recommended`、`reviews` 等普通评价字段并非分数目标，不单凭字段或图层名的子串自动认领。|
|**双向校验规则**|**前置身份**：先检查 target 及已确认所属组件是否精确名为 `Hot Score`；若命中热度分，直接交第 5 节。只有精确名为 `Score` 且没有 `Hot Score` 归属，或官方身份可靠确认为点评分，才进入点评分规则。若命名和组件身份相互矛盾，先人工复核；不凭 0.1–5 分值或 `includes("Score")` 单独命中。<br>**规则 A（非法使用）**：target 使用 `color-specific-rate (#173CD2)`，但已可靠确认它不属于点评分（含已确认的 `Hot Score` 热度分或普通评价字段）→ 候选报错；归属未知时人工复核。<br>**规则 B（漏用专有色）**：target 已可靠确认为 `Score` 点评分目标，但最终色值 ≠ `color-specific-rate (#173CD2)` → 候选报错。|
|**插件报错文案**|情况 A：**点评分专有色误用**：`color-specific-rate (#173CD2)` 仅用于已确认的 `Score` 点评分文字／图标；不校验 Tag 背景，热度分 `Hot Score` 不属于点评分。<br>情况 B：**点评分漏用专有色**：已确认的 `Score` 点评分目标应使用 `color-specific-rate (#173CD2)`；请核对当前色值。|



---



### 8. 专有色 - Trip Best 【严格独占规则】

定义：Trip Best 榜单的唯一专有颜色，具备双向排他性。

- **Token ID**: `color-specific-trip-best`

- **Hex 映射**: `#673114`

- **语义标签**: `Trip Best Rank` / `Trip Best Tag` \(榜单专属独占\)

|**维度**|**条件定义与判定逻辑**|
|---|---|
|**推荐场景 \(DO\)：**|仅限用于**已确认的官方 Trip Best 榜单单元内的信息文字与图标**，不包括背景：<br>1. Trip Best 普通榜单，如上海全球旅客精选景点第9名，入选上海人气景点<br>2. Trip Best 年度榜单，2026 China 100\-人气景点<br>3. 与 Trip Best Logo 同属一个榜单单元的所有跟随描述文字（含排名、入选说明、榜单名、品类后缀），例如"第 9 名""入选上海人气景点""2026 China 100""人气景点"|
|**禁用场景 \(DON’T\)：**|1\. `color-specific-trip-best (#673114)` 不得用于已确认的非 Trip Best 普通文字或图标。<br>2\. 官方 Trip Best 单元中已确认的专属排名／描述信息文字和图标不应漏用该色；普通业务内容与背景填充不在此规则的目标内。|
|**双向校验规则**|**前置 Trip Best Hit**：target 须有可靠证据确认属于**官方 Trip Best 组件／Logo**，只认领该官方单元内的专属信息文字与图标；“Top”“入选”“上榜”“榜单”等文案、数字排名或普通图层名称只能辅助人工查找，**不得独立触发 Hit**。未能核对官方身份时不执行 A/B，先人工复核。<br>**规则 A（非法使用）**：已确认不属于官方 Trip Best 单元的信息文字／图标使用 `color-specific-trip-best (#673114)` → 候选报错；仅凭缺少某个关键词不得报错。<br>**规则 B（漏用专有色）**：已确认的官方 Trip Best 单元内，明确归属其专属排名／入选描述或 Logo 的文字／图标最终色值 ≠ `color-specific-trip-best (#673114)` → 候选报错；不扩散到整页、相邻普通业务内容或背景填充。|
|**插件报错文案**|情况 A：**Trip Best 专有色越界**：`color-specific-trip-best (#673114)` 仅用于已确认的官方 Trip Best 信息文字与图标；当前目标已确认不属该官方单元，请核对。<br>情况 B：**Trip Best 专属信息漏色**：已确认的官方 Trip Best Logo／排名／跟随描述信息应使用 `color-specific-trip-best (#673114)`；普通业务图层与背景不纳入此项。|


---



### 9. 中性色阶 Neutral Colors (Black & Gray)

> **定义**：构建页面客观描述的信息层级，以及查询框、表单等录入项的暗提示。

> **同色不同 Token**：用户确认官方组件中确实存在 `color-text-tertiary (#6F7685)` 与 `color-text-Placeholder (#6F7685)` 两个独立 Token。前者用于辅助说明，后者用于录入项暗提示；同一个 Hex 不能替代组件中的 Token 身份。校验时应核对可靠的组件 Token／变量绑定，无法读取时人工复核。

#### Neutral Primary（主要中性色）

- **Token ID**：`color-text-primary`
- **Hex 映射**：`#121826`
- **语义标签**：`Primary Text`

|维度|条件定义与判定逻辑 (Plugin Rules Engine)|
|---|---|
|**推荐场景 (DO)**|核心标题、卡片主标题、关键属性文本。|
|**禁用场景 (DON'T)**|原稿列出的误用情形：字号 `<12px` 的文本或辅助信息使用 Primary；其他字号／场景不自行扩展。|
|**插件触发条件**|**规则 A（小字号使用主文本色）**：文本字号 `<12px` 且使用 `color-text-primary (#121826)` → 候选提示。<br>**规则 B（辅助信息层级过重）**：已可靠确认为辅助信息却使用 `color-text-primary (#121826)` → 候选提示；归属不明先人工核对。|
|**插件报错文案**|情况 A／B：**文本层级过重**：辅助性或次要信息使用了 `color-text-primary (#121826)` 时，请核对是否需改用 `color-text-secondary (#4F5563)`；小字号场景请按实际信息层级检查。|

---

#### Neutral Secondary（次级中性色）

- **Token ID**：`color-text-secondary`
- **Hex 映射**：`#4F5563`
- **语义标签**：`Secondary Text`

|维度|条件定义与判定逻辑 (Plugin Rules Engine)|
|---|---|
|**推荐场景 (DO)**|副标题、次要属性描述、输入框 Label。|
|**禁用场景 (DON'T)**|原稿不推荐用于字号 `≥20px` 的页面级一级标题。|
|**插件触发条件**|**规则 A（标题强调不足）**：已确认是页面级一级标题，且字号 `≥20px` 却使用 `color-text-secondary (#4F5563)` → 候选提示。原稿未给出其他自动触发条件。|
|**插件报错文案**|情况 A：**标题强调不足**：页面级一级标题使用了 `color-text-secondary (#4F5563)`，请核对是否应提升为 `color-text-primary (#121826)`。|

---

#### Neutral Tertiary（辅助中性色）

- **Token ID**：`color-text-tertiary`
- **Hex 映射**：`#6F7685`
- **语义标签**：`Tertiary Caption`

|维度|条件定义与判定逻辑 (Plugin Rules Engine)|
|---|---|
|**推荐场景 (DO)**|辅助说明、置灰信息、解说性小字。|
|**禁用场景 (DON'T)**|主标题或正文关键信息使用 Tertiary，可能导致可读性不足；不把相同 Hex 的 `color-text-Placeholder` Token 视为本条用途。|
|**插件触发条件**|**规则 A（关键信息层级过低）**：已可靠确认为主标题或正文关键信息，却使用 `color-text-tertiary (#6F7685)` → 候选提示；只看到 `#6F7685` 且无法核对 Token 身份时不得误报 `color-text-Placeholder`。|
|**插件报错文案**|情况 A：**文本可读性过低**：关键信息使用辅助中性色 `color-text-tertiary (#6F7685)`，可能影响可读性；请核对信息层级。|

---

#### color-text-Placeholder（录入项暗提示）

- **Token ID**：`color-text-Placeholder`
- **Hex 映射**：`#6F7685`
- **语义标签**：`Input Placeholder`

|维度|条件定义与判定逻辑 (Plugin Rules Engine)|
|---|---|
|**推荐场景 (DO)**|查询框、表单等录入项尚未输入内容时的暗提示文字。|
|**禁用场景 (DON'T)**|不把已输入内容、表单 Label 或背景当作暗提示。|
|**插件触发条件**|**规则 A（暗提示漏用）**：target 经可靠结构确认是 Trip 录入项暗提示，且最终文字色值 ≠ `color-text-Placeholder (#6F7685)` → 候选提示。<br>**规则 B（Token 身份）**：target 已绑定变量／样式且可可靠读取，绑定 Token ID ≠ `color-text-Placeholder` → 候选提示；读不到绑定时，不能仅凭 `#6F7685` 区分它与 `color-text-tertiary`，改为人工复核，不自动报错。|
|**插件报错文案**|情况 A：**暗提示色不符**：已确认的 Trip 查询框／表单暗提示应使用 `color-text-Placeholder (#6F7685)`。<br>情况 B：**暗提示 Token 需核对**：当前色值可能正确，请确认绑定的是 `color-text-Placeholder` 而非同色的 `color-text-tertiary (#6F7685)`；绑定不可读时人工确认。|

---


### 10. 中性色阶 Neutral Colors (White)



> **定义**：深色背景上的中性信息色
>
>



- **Token ID**: `color-text-Inversed`

- **Hex 映射**: `#FFFFFF`

- **语义标签**：`Dark-Background Text` / `Dark-Button Text` / `Dark-Label Text`

|维度|条件定义与判定逻辑 \(Plugin Rules Engine\)|
|---|---|
|**推荐场景 \(DO\)**|1\. 用于深色背景（如深色按钮、深色标签、深色卡片、深色蒙层、深色占位色块）上的高强调文字及图标。|
|**插件触发条件**|**无需触发报错**，白色文字均绑定标签、按钮、图片、蒙层等出现|

---

## 来源与评审边界

- **原稿**：`_sources/trip/general/trip-info-color-v1.6-2026-10-20.md`（原文件逐字节归档，SHA-256：`2a77bebadf0322ce17195a6374722e856dd73390a08aa3db341761d93d4e28cb`）。
- **Trip 专属**：本页的 `Brand`、`Functional/*`、`Neutral/*` 和 `color-specific-*` 及其 Hex 均来自 Trip 原稿；与 Ctrip 的同名语义或偶然相同色值不构成跨 App 规则继承。
- **用户已澄清的口径**：录入项暗提示 `color-text-Placeholder (#6F7685)` 与同色 Tertiary 的不同 Token 用途见 `_sources/trip/general/trip-placeholder-clarification-2026-10-20.md`；Trip Best 官方身份及仅文字／图标的范围见 `_sources/trip/general/trip-best-info-scope-clarification-2026-10-20.md`；分数命名见 `_sources/trip/general/trip-score-name-clarification-2026-10-20.md`；专有色面积、减价用色及官方品牌组件归属见 `_sources/trip/general/trip-color-scope-clarification-2026-10-20.md`，处理记录见 [[_meta/conflicts]] 已归档 #003–#006；全局分母及仅作设计师提醒的性质已由用户确认，见 `_sources/trip/general/trip-area-ratio-clarification-2026-10-20.md`；#007 已归档。上述插件触发仍为待实现、待回归的候选写法；身份或背景无法可靠判断时先人工复核。
- **插件状态**：`status: production` 表示 Wiki 内容已定稿；`figma_plugin_active: false` 表示 Trip 审核插件尚未接入。无 Trip 插件实测基线；不得借用 Ctrip 的 0.90。
