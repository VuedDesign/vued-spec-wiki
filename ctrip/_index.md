---
name: Ctrip App 规范索引
type: index
app: ctrip
last_updated: 2026-09-23
---

# Ctrip App · 设计规范索引

携程主品牌 App 的完整设计规范知识库。

---

## General 通用型规范

面向未被专属规范认领内容的通用原子规范，也提供可被 brand / feature 复用的 Token 名称和基础值。专属规范可以引用这些 Token，但是否允许使用、如何组合及如何审核，仍由专属规范决定。

- [[ctrip/general/info-color]] — **信息色彩规范 v1.7** · 全局面积占比 + 10 类语义色的图层级判定（生产中，准确率 90%+）
- （待建）typography — 字号、字重、行高
- （待建）spacing — 间距刻度
- （待建）radius — 圆角规范
- （待建）shadow — 阴影层级
- （待建）motion — 动效时长与曲线

---

## Brand 品牌类规范

品牌专属的视觉标识与规则。每份规范前都有"作用域判定"，未通过判定的图层跳过本规范。

- [[ctrip/brand/ctrip-self]] — **携程自营 v1.5** · Logo + 标签体系 + Banner + 浮层落地页（生产中，准确率 90%+）
- （待建）ctrip-premium — 携程优选
- （待建）其他品牌类

---

## Feature 功能类规范

特定组件或页面模块的规范。

- （待建）foot-bar — 底部导航栏
- （待建）banner — 通用横幅
- （待建）info-tip — 信息提示
- （待建）其他功能类

---

## 使用提示（给 AI）

- **先识别专属场景，再识别属性。** “颜色相关”不自动等于先查 general/info-color。
- 用户问“携程自营 Logo / 标签 / Banner / 颜色”时，先查 [[ctrip/brand/ctrip-self]] 并执行其作用域判定；命中后由携程自营规范独立管辖，general/info-color 对这些图层让渡、不重复校验。
- 只有普通 Ctrip 内容或未被任何 brand / feature 规范认领的颜色问题，才由 [[ctrip/general/info-color]] 兜底。
- 品牌类规范可以复用 general 中的 Token 名称和基础值，也可以定义专属值；**复用 Token 不代表继承 general 的审核条件**。
- 同一属性发生冲突时，以作用域更具体的专属规范为准（局部覆盖优先）。
