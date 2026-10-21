# 原始规范文档存档

存放"喂"给本 Wiki 的所有原始规范文档（PDF、Word、Markdown、Figma 导出、飞书导出等）。

## 用途

- **审计追溯**：Wiki 页面被质疑时回查原始来源
- **重编译源**：规范升版时（v1.7 → v1.8），把新版放进来触发重编译
- **保底存档**：即使 Wiki 出错也不丢失原始信息

## 已归档来源

- `shared/general/figma-dom-for-designers-2026-09-17.pdf` — [[_shared/figma-structure]] 的原始科普材料
- `ctrip/general/info-color-black-5-user-2026-10-20.md` — [[ctrip/general/info-color-v1-8]] 的用户输入来源；Black-3 占位用途已按用户决议移除，Black-4 灰底例外已补 ID
- `ctrip/general/info-color-orange-red-hierarchy-2026-10-20.md` — 用户确认 Orange-1 为重点提醒（Attention）、Red-1 为更高等级警示（Warning／Alert）；v1.8 正式稿据此区分提示层级
- `trip/general/trip-info-color-v1.6-2026-10-20.md` — [[trip/general/info-color]] 的原始 Markdown（Trip 信息色彩 1.6，SHA-256：`2a77bebadf0322ce17195a6374722e856dd73390a08aa3db341761d93d4e28cb`）；已原样归档，#003–#006 的后续用户决议见下述澄清记录
- `trip/general/trip-score-name-clarification-2026-10-20.md` — 用户确认 `Score` 是点评分、`Hot Score` 是景点热度分，修正原稿的宽泛 `Score` 名称命中
- `trip/general/trip-color-scope-clarification-2026-10-20.md` — 用户确认专有色计入全局 10%、减价／优惠数值使用 Discount，静态品牌色以官方品牌组件身份认领
- `trip/general/trip-best-info-scope-clarification-2026-10-20.md` — 用户要求先确认官方 Trip Best 才认领专有色，信息色只审核文字与图标、不含背景；全局面积分母待裁定 #007
- `trip/general/trip-placeholder-clarification-2026-10-20.md` — 用户最终确认录入项暗提示 `color-text-Placeholder (#6F7685)`；与 `color-text-tertiary (#6F7685)` 同色但 Token ID 不同
- `trip/general/trip-area-ratio-clarification-2026-10-20.md` — 用户确认全局分母为所有信息文字与图标，60%／30%／10% 及 Discount 额外 5% 仅为可因特殊场景偏离的理想参考比例，不做报错或警示
- `ctrip/brand/ctrip-select-v1.0-text-2026-10-13.md` — [[ctrip/brand/ctrip-select]] 的飞书草稿《携程优选1.0》纯文字来源；原始 Markdown 与本地含图 ZIP 的 SHA-256 见文件头。七张原稿图片仅维护者本地留存，**不上传 GitHub**
- `ctrip/brand/ctrip-select-figma-inspection-2026-10-13.md` — 同页所用 Figma 组件区的**只读观察记录**，不是另一个经批准的规范原稿
- `ctrip/brand/ctrip-select-color-clarification-2026-10-13.md` — 用户在 2026-10-13 补充并随后纠正的信息文字可用色清单；原话保留作溯源，后续明确排除金色
- `ctrip/brand/ctrip-select-info-group-clarification-2026-10-20.md` — 用户对优选信息组示意图标、组件占位符和标题／正文 `Token/Black-1 (#111111)` 的决议记录；原话保留作溯源
- `ctrip/brand/ctrip-select-final-scope-clarification-2026-10-20.md` — 用户确认反白 Logo 本版限官方蓝底面性标签、其余品牌文字五色用途由设计师自主决定
- `ctrip/brand/ctrip-select-filter-logo-clarification-2026-10-20.md` — 用户确认优选筛选标识为专用矢量四字与橙色勾组成的完整 Logo，撤销“删 Logo 只剩优选文字”的误判

## 组织方式

建议按 App + scope 分子目录：

```
_sources/
├── ctrip/
│   ├── general/
│   │   └── info-color-v1.7-2026-09.md
│   └── brand/
│       └── ctrip-self-v1.5-2026-09.md
└── trip/
    ├── general/
    │   └── trip-info-color-v1.6-2026-10-20.md
    └── brand/
```

## 命名建议

- `{规范短名}-v{版本号}-{年月}.{格式}`
- 例：`info-color-v1.7-2026-09.md`

## 引用方式

Wiki 页面 frontmatter 的 `sources` 字段指向这里：

```yaml
sources:
  - _sources/ctrip/general/info-color-v1.7-2026-09.md
```
