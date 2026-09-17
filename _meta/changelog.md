---
name: 变更日志 Changelog
type: meta
last_updated: 2026-09-17
---

# 变更日志

> 每次修改任何规范文档都在此加一行。格式：`日期 · 文件路径 · 变更内容 · 起因`。最新的在最上面。

---

## 2026-09

- **2026-09-17** · `_shared/figma-structure.md` · 从《写给设计师的 DOM 科普：AI 时代，你的图层树为什么突然重要了》提炼 Figma 图层结构与机器可读性原则；原 PDF 归档至 `_sources/shared/general/`，并更新共享索引、全局索引与来源清单。页面设为 `status: draft`、`figma_plugin_active: false`，尚未形成可执行规则，不影响现有生产校验 · 起因：用户授权将科普材料消化进 Wiki
- **2026-09-14** · 全库 · AI 入口文件改名：`CLAUDE.md` → `AGENTS.md`。理由：`CLAUDE.md` 是 Claude 专属加载名，换用其他 AI 工具时规则不会自动生效，与「纯 Markdown、不绑供应商」的定位矛盾；`AGENTS.md` 为跨工具通用约定名，Claude / Codex / Cursor 均可自动加载。同步更新文件内标题与 `README.md` 目录一览 · 起因：用户提出命名应中性化
- **2026-09-14** · 全库 · 根目录改名：`knowledge-base` → `vued-spec-wiki`。同步更新 `README.md` 目录一览与 `_meta/plugin-integration.md` 的插件加载入口两处写死路径 · 起因：用户指定新目录名。**注意：插件按路径读取本库，改名后需同步插件侧的配置，否则加载入口失效**
- **2026-09-11** · `ctrip/general/info-color.md` · 修正 Red\-1 的「插件触发条件」色值：`#D02C2A` → `#F5190A`，与同节「Hex 映射」对齐 · 起因：编译复核发现同节红值不一致（`#D02C2A` 为误写）
- **2026-09-11** · `ctrip/general/info-color.md` · Brown 一节：定义由"复杂信息层级中弱于主色的次要高亮"（原为误抄自 BlueGray 的文案）改为"携程榜单专用色值"；「语义标签」与「禁用场景」中的 `Trip Best` 全部改为 `携程榜单` · 起因：Trip Best 是 Trip 端榜单叫法，Ctrip 端统一称"携程榜单"，同一概念不跨 App 混用
- **2026-09-11** · 全库 · 建立知识库骨架，包含 Ctrip / Trip 双 App、general/brand/feature 三层、\_meta / \_shared / \_sources 辅助目录 · 起因：LLM Wiki 项目正式启动，从演练版升级为对接 Figma 插件的生产版
- **2026-09-11** · `ctrip/general/info-color.md` · 从原有 v1.7 版本搬入 Wiki，仅补加 frontmatter，内容原样保留 · 起因：内容已在 Figma 插件投产，实测准确率 90%+，直接标为 `status: production`
- **2026-09-11** · `ctrip/brand/ctrip-self.md` · 从原有 v1.5 版本搬入 Wiki，仅补加 frontmatter，内容原样保留 · 起因：同上

---

> 编辑说明：
> - 时间格式统一 YYYY-MM-DD
> - 页面用相对路径，如 `ctrip/general/info-color.md`
> - 起因可以是：会议决议 / 新版规范发布 / 用户反馈 / 冲突处理 / 插件校验发现 等
