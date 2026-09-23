---
name: 全局索引 Root Index
type: index
last_updated: 2026-09-23
---

# 设计规范知识库 · 全局索引

> **AI 请注意**：这是一套**双 App、三分层**的设计规范知识库。回答问题前，先根据用户所在 App（Ctrip / Trip）定位子索引，再进入具体规范。

---

## 双 App 入口

- [[ctrip/_index]] — **Ctrip App** 全部规范（携程主品牌）
- [[trip/_index]] — **Trip App** 全部规范（Trip 国际品牌，规范待建）

---

## 分层说明（每个 App 内部）

每个 App 的规范都按三层组织：

| 层级 | 目录 | 内容 | 举例 |
|---|---|---|---|
| **General 通用型** | `{app}/general/` | 原子级规范，跨品牌跨场景通用 | 颜色、字号、间距、圆角、无障碍 |
| **Brand 品牌类** | `{app}/brand/` | 品牌专用视觉规范 | 携程自营、携程优选 |
| **Feature 功能类** | `{app}/feature/` | 特定组件/场景的规范 | Foot bar、Banner、信息提示 |

**引用与管辖关系**：品牌类与功能类可以引用通用层的 Token 名称和基础值，但专属场景的允许范围、组合方式与审核逻辑由对应的 brand / feature 规范定义。**Token 复用不等于规则继承**：图层一旦被专属规范认领，专属规范优先，general 规范对该图层让渡、不重复校验；只有未被任何专属规范认领的内容，才由 general 规范兜底。专属规范也可以定义通用层没有的专属值。

---

## 共享区域

- [[_shared/]] — 跨 App 共享的规范索引
  - [[_shared/figma-structure]] — Figma 图层结构与机器可读性规范（草稿，审核与生成的结构基础）
- [[_sources/]] — 原始规范文档存档
- [[_meta/]] — Wiki 元数据（Schema、变更日志、冲突清单、插件集成说明）

---

## AI 查询流程

1. **确定 App**：用户在 Ctrip 还是 Trip 场景？
2. **先判定专属作用域**：问题或图层是否明确属于某个 brand / feature？若命中，先进入对应专属规范并执行其作用域判定。
3. **再由 general 兜底**：仅当内容未被任何专属规范认领时，才进入 general；属性是颜色、字号或间距，并不自动意味着优先查 general。
4. **打开对应页面**：读 frontmatter 与正文，必要时沿 `[[link]]` 查询 Token 基础定义，但不得借此把通用审核规则重新施加到专属图层。
5. **回答时给出实际管辖页面**：例如携程自营颜色问题引用 `[[ctrip/brand/ctrip-self]]`，普通 Ctrip 信息色问题引用 `[[ctrip/general/info-color]]`。

---

## 面向 Figma 插件

本 Wiki 同时作为 Figma 审核插件的规则源。插件加载规则时的路由方式见 [[_meta/plugin-integration]]。

每份规范文档的 frontmatter 都带 `figma_plugin_active` 与 `accuracy_baseline` 字段，标注产线状态与实测准确率。
