---
name: 规范文档元规范 Schema
type: meta
last_updated: 2026-10-20
---

# Schema：规范文档的元规范

> 本文件定义"每一份设计规范文档应该长什么样"。所有新增、编辑规范时必须遵循。这是保证全库一致性、机器可读性、插件可对接的基础。

---

## 一、Frontmatter 字段

### 必填字段

| 字段 | 类型 | 说明 | 允许值 |
|---|---|---|---|
| `id` | string | 全库唯一 ID，kebab-case | 如 `ctrip-info-color` |
| `name` | string | 显示名（人读） | 如 `Ctrip 信息色彩规范` |
| `version` | string | 规范版本号 | 如 `"1.7"` |
| `app` | enum | 所属 App | `ctrip` \| `trip` \| `shared` |
| `scope` | enum | 三层分类 | `general` \| `brand` \| `feature` |
| `category` | string | 更细的类目 | `color` / `spacing` / `brand-identity` / `component` … |
| `status` | enum | 生命周期状态 | `draft` \| `review` \| `production` \| `deprecated` |
| `last_updated` | date | 最后更新日期 | `2026-09-11` |
| `figma_plugin_active` | bool | 是否已投产到 Figma 插件 | `true` / `false` |

### 选填字段

| 字段 | 类型 | 说明 |
|---|---|---|
| `accuracy_baseline` | float | 插件实测准确率（0–1） |
| `scope_gate` | string | 前置作用域判定说明（如"必须先通过 Hit Test"） |
| `related` | list | 相关规范页面路径 |
| `sources` | list | 来源原始文档路径 |
| `tags` | list | 检索标签 |
| `owner` | string | 内容负责人 |
| `deprecated_by` | string | 若已弃用，指向替代页 |

---

## 二、正文结构约定

### 通用型 (general) 规范推荐结构

```
## 核心校验逻辑与全局规则 (Global Rules)
    面积占比 / 全局约束（表格：属性 / 令牌 / 占比 / 判定逻辑 / 报错文案）

## 图层级 Token 校验字典
    每个 Token 一节：
    - Token ID / Hex 映射 / 语义标签
    - 表格：推荐场景 / 禁用场景 / 插件触发条件 / 插件报错文案
```

### 品牌类 (brand) 规范推荐结构

```
## 品牌介绍 (Brand Context)
    非校验内容，供 AI / 设计师理解

## 全局作用域判定 (Hit Test) 【统一前置】
    命中条件 / 图形结构定义 / Miss 情况

## 图层级校验字典
    每个组件/元素一节，含视觉规格 + 判定表格
```

### 功能类 (feature) 规范推荐结构

```
## 概述
    这是什么组件，出现在哪些场景

## 视觉规格
    尺寸、颜色（引用 Token）、圆角、间距

## 交互规则
    状态、反馈、动效

## 校验规则
    每条规则含：触发条件 / 判定逻辑 / 报错文案

## 常见问答
```

---

## 三、判定规则表格的推荐列（这是机器可读的关键）

参考现有 `ctrip/general/info-color-v1-8` 和 `ctrip/brand/ctrip-self` 的写法：

| 列名 | 内容要求 |
|---|---|
| **推荐场景 (DO)** | 明确列举合适场景，最好带具体示例 |
| **禁用场景 (DON'T)** | 明确列举错误用法，最好也带示例 |
| **插件触发条件** | 用"规则 A / 规则 B"分开写，每条明确 target + 条件 |
| **插件报错文案** | 用"情况 A / 情况 B"给出成品文案，插件直接引用 |

**核心原则**：判定条件用**结构化的 if-then 语言**（图层名匹配 XXX 且 色值 = XXX），不用散文。

---

## 四、双向校验规则（进阶模式）

对于品牌类专属色 / 组件（如榜单棕、携程自营 Logo），除了"不该用却用了"，还要写"该用却没用"：

- **规则 A（非法使用）**：不在专属场景，却使用了专属色 → 报错
- **规则 B（漏用专属）**：处于专属场景，却没使用专属色 → 报错

范例见 [[ctrip/general/info-color-v1-8]] 的 Brown-1 / [[ctrip/brand/ctrip-self]] 的 Logo。

---

## 五、状态定义

| 状态 | 含义 | AI 使用时的行为 |
|---|---|---|
| `draft` | 初稿，未 review | 回答时提示"此规范尚未定稿" |
| `review` | Review 中 | 回答时提示"此规范正在评审" |
| `production` | Wiki 规范内容已定稿；不等于已上传 GitHub 或接入 Figma 插件 | 正常引用；实际发布与插件加载另行核对 |
| `deprecated` | 已弃用 | 引导至 `deprecated_by` |

> `status` 描述规范内容的正式程度，`figma_plugin_active` 描述插件接入状态；正式 Wiki 可以暂不进入插件。插件只加载 `production` 且 `figma_plugin_active: true` 的当前 App 规范，见 [[_meta/plugin-integration]]。

---

## 六、命名约定

- 文件名：小写、连字符：`info-color.md`、`ctrip-self.md`、`foot-bar.md`
- 目录：`{app}/{scope}/{filename}.md`
- Wiki 互链：`[[ctrip/general/info-color-v1-8]]`
