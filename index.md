---
name: 全局索引 Root Index
type: index
last_updated: 2026-09-17
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

**引用关系**：品牌类与功能类**引用**通用型的令牌，不重复定义。例如"携程自营"页面里的可用颜色列表，全部引用 `ctrip/general/info-color` 中定义的 Token。

---

## 共享区域

- [[_shared/]] — 跨 App 共享的规范索引
  - [[_shared/figma-structure]] — Figma 图层结构与机器可读性规范（草稿，审核与生成的结构基础）
- [[_sources/]] — 原始规范文档存档
- [[_meta/]] — Wiki 元数据（Schema、变更日志、冲突清单、插件集成说明）

---

## AI 查询流程

1. **确定 App**：用户在 Ctrip 还是 Trip 场景？
2. **确定分层**：问题涉及原子规范（general）？品牌规范（brand）？功能组件（feature）？
3. **打开对应页面**：读 frontmatter 与正文
4. **沿引用跳转**：如遇 `[[link]]`，跟随打开
5. **回答时给出出处**：`按 [[ctrip/general/info-color]] 的规定...`

---

## 面向 Figma 插件

本 Wiki 同时作为 Figma 审核插件的规则源。插件加载规则时的路由方式见 [[_meta/plugin-integration]]。

每份规范文档的 frontmatter 都带 `figma_plugin_active` 与 `accuracy_baseline` 字段，标注产线状态与实测准确率。
