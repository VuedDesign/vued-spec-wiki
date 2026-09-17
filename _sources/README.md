# 原始规范文档存档

存放"喂"给本 Wiki 的所有原始规范文档（PDF、Word、Markdown、Figma 导出、飞书导出等）。

## 用途

- **审计追溯**：Wiki 页面被质疑时回查原始来源
- **重编译源**：规范升版时（v1.7 → v1.8），把新版放进来触发重编译
- **保底存档**：即使 Wiki 出错也不丢失原始信息

## 已归档来源

- `shared/general/figma-dom-for-designers-2026-09-17.pdf` — [[_shared/figma-structure]] 的原始科普材料

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
