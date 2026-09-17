---
name: 跨 App 共享规范索引
type: index
app: shared
last_updated: 2026-09-17
---

# 跨 App 共享规范

存放同时适用于 Ctrip 和 Trip 两个 App 的规范。**只有确认两个 App 完全一致的规则才应放这里**，任何有品牌差异的都不适合。

## 已收录

- [[_shared/figma-structure]] — **Figma 图层结构与机器可读性规范 v0.1** · 审核与生成共用的结构原则（草稿，暂不参与插件校验）

## 典型候选

- **无障碍标准**（WCAG AA 对比度、最小点击区等）—— 大概率通用
- **动效原则**（缓动曲线、时长基线）—— 可能通用
- **Toast / 全局反馈的交互逻辑** —— 可能通用

## 使用方式

在 Ctrip / Trip 各自的 _index.md 中引用：

```markdown
- [[_shared/accessibility]] — 无障碍标准（Ctrip 与 Trip 共用）
```

frontmatter 里 `app: shared`，插件加载时对两个 App 都生效。

## 何时不该放这里

- Ctrip 与 Trip 有色值差异 → 各自放 general/
- 组件外观有品牌差异 → 各自放 brand/ 或 feature/
- 只是"看起来差不多"但未严格核对 → 先各放一份，等确认再合并
