# 设计规范知识库

> 服务于 Ctrip App 与 Trip App 的双品牌设计规范知识库。既是设计师查规范的 LLM Wiki，也是 Figma 审核插件的规则源。

---

## 一句话说明

**这个文件夹里的 Markdown 既供人查询，也为规则编译提供来源**；只有满足 `status: production` 且 `figma_plugin_active: true` 的规范才进入当前 Figma 插件自动校验。

## 现有规范与插件状态

- **Ctrip / general / info-color** v1.8 — Wiki 现行正式规范（`ctrip/general/info-color-v1-8.md`），含 `Token/Black-5 (#C5C5C5)`；已上传 GitHub，Figma 插件尚未接入。旧版 `ctrip/general/info-color.md` v1.7 保留为现有插件基线（实测 0.90）
- **Ctrip / brand / ctrip-self** v1.5 — Wiki 正式、Figma 插件已投产，实测准确率 90%+
- **Ctrip / brand / ctrip-select** v1.1 — Wiki 已定稿；Figma 插件规则待另一位负责人接入与验证，尚无实测准确率基线

## Trip 当前状态

- **Trip / general / info-color** v1.6 — Wiki 已定稿，仅审信息文字／图标并补 `color-text-Placeholder (#6F7685)`；面积比例为非阻断设计参考，Figma 插件尚未接入（`figma_plugin_active: false`）

## 目录一览

```
vued-spec-wiki/
├── README.md                       此文件
├── AGENTS.md                       AI 使用规则（本库的 AI 入口）
├── index.md                        全局路由
│
├── ctrip/                          Ctrip App 规范
│   ├── _index.md
│   ├── general/                    通用型（颜色、字号、间距…）
│   ├── brand/                      品牌类（携程自营、携程优选…）
│   └── feature/                    功能类（foot bar、banner…）
│
├── trip/                           Trip App 规范
│   ├── _index.md
│   ├── general/                    通用型（信息色彩 info-color v1.6 已定稿）
│   ├── brand/                      品牌类（待建）
│   └── feature/                    功能类（待建）
│
├── _shared/                        两个 App 完全共用的规范
├── _sources/                       原始规范文档存档
└── _meta/                          Wiki 元数据
    ├── schema.md                   规范文档的元规范
    ├── changelog.md                变更日志
    ├── conflicts.md                冲突清单
    └── plugin-integration.md       Figma 插件集成规范
```

## 使用场景

### 场景一：设计师查规范

打开 Claude 桌面版或 Cursor，把这个文件夹连接进来，直接问：
- "Ctrip 的主按钮颜色是什么？"
- "携程自营 Logo 可以用金色吗？"

### 场景二：Figma 插件审核设计稿

插件按 `_meta/plugin-integration.md` 加载规则，扫描 Figma 图层并给出违规提示。

### 场景三：Figma 插件生成合规稿（规划中）

需要为每份规范补上"生成决策树"章节。当前 v1 版本尚未支持。

## 贡献流程

- 新增规范：把源文档放入 `_sources/`，按 `_meta/schema.md` 补 frontmatter 后放到对应目录
- 修订规范：直接编辑，同时在 `_meta/changelog.md` 加一行
- 发现冲突：写进 `_meta/conflicts.md`，@ 相关负责人

## 联系人

- 项目发起 / 维护：（待填）
- Figma 插件负责人：（待填）
