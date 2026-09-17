---
name: Ctrip App 规范索引
type: index
app: ctrip
last_updated: 2026-09-11
---

# Ctrip App · 设计规范索引

携程主品牌 App 的完整设计规范知识库。

---

## General 通用型规范

跨品牌、跨场景的原子级规范。所有 brand / feature 规范都应引用这里的令牌。

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

- 用户问"颜色相关"时先查 general/info-color
- 用户问"携程自营 Logo / 标签 / Banner"时先查 brand/ctrip-self，但必须先通过其"作用域判定"
- 品牌类规范里的"可用颜色白名单"通常是 general/info-color 中令牌的子集——冲突时以品牌类为准（局部覆盖优先）
