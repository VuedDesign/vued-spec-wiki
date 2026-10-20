---
name: Trip App 规范索引
type: index
app: trip
last_updated: 2026-10-20
---

# Trip App · 设计规范索引

Trip 国际品牌 App 的完整设计规范知识库。

> ⚠️ **当前状态**：Trip 信息色彩 v1.6 已按原稿与用户后续决议定稿为 Wiki 正式规范；仅审信息文字与图标、不含背景。面积比例采用所有信息文字与图标为分母，仅作可因特殊场景偏离的设计师提醒；#003–#007 已归档。插件身份判定与回归仍待负责人完成，当前未启用。其他 Trip 规范仍待建立。不得将 Ctrip 规则直接迁入。

---

## General 通用型规范

- [[trip/general/info-color]] — **Trip 信息色彩 v1.6（Wiki 正式稿）** · 已按 Trip 原稿及用户决议编入色阶与 `color-text-Placeholder (#6F7685)`；面积比例仅供设计师参考，插件未接入
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

1. **仅参考结构与排版**：目录结构、frontmatter Schema 和“全局规则 → 图层级 Token 字典 → 规则表”的文档形式可对照 Ctrip。
2. **内容逻辑独立编译**：Trip 的 Token、Hex、语义、允许／禁用场景、阈值与作用域均以 Trip 来源为准；不能假设差异只在品牌层或只在色值。
3. **共享须有依据**：无障碍、间距、圆角等是否跨 App 共用，须有正式来源并经确认，不能因为看起来相近就迁入 `[[_shared/]]`。
4. **插件分桶但不提前启用**：frontmatter 使用 `app: trip`；草稿规则保持 `figma_plugin_active: false`，获得来源、评审与回归后再讨论接入。
