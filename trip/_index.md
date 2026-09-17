---
name: Trip App 规范索引
type: index
app: trip
last_updated: 2026-09-11
---

# Trip App · 设计规范索引

Trip 国际品牌 App 的完整设计规范知识库。

> ⚠️ **当前状态**：Trip 版规范尚未建立。目录结构已就位，等待 Ctrip 版跑稳后按同结构平行迁移。

---

## General 通用型规范

- （待建）info-color — 信息色彩（Trip 版）
- （待建）typography
- （待建）spacing
- （待建）radius

---

## Brand 品牌类规范

- （待建）Trip 主品牌规范
- （待建）Trip 子品牌规范

---

## Feature 功能类规范

- （待建）foot-bar
- （待建）banner
- （待建）info-tip

---

## 迁移策略（记录）

Trip 版建立时应遵循的原则：

1. **架构镜像 Ctrip**：目录结构、frontmatter schema、判定逻辑格式完全一致
2. **仅品牌层差异**：颜色语义可能相同（Primary / Warning / Success），但**色值不同**
3. **优先复用 general**：无障碍、间距、圆角等大概率与 Ctrip 完全一致，可挪到 [[_shared/]]
4. **frontmatter 的 `app: trip`** 让插件按需加载对应规则集
