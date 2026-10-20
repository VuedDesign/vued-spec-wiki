# Trip 录入项暗提示 Token · 用户补充记录

- **来源**：2026-10-20 当前对话中的用户直接补充，目标是 `[[trip/general/info-color]]` 第 9 节中性色阶。
- **用户原话**：“在这个规范里我也加增加暗提示颜色，就是用在查询框、表单等录入项中。色值是#6F7685。tokenid是Placeholder    ，放在9. 中性色阶 Neutral Colors (Black & Gray)里”。
- **后续用户纠正（现行口径）**：“统一写成这个`color-text-Placeholder`”。因此实际 Token ID 统一为 `color-text-Placeholder`、Hex `#6F7685`，用于 Trip 查询框、表单等录入项暗提示；先前原话中的 `Placeholder` 仅留作历史记录。原稿已有 `color-text-tertiary (#6F7685)` 用于辅助说明；两个 Token ID 共享色值但语义不同，不能只凭 Hex 判定绑定。读不到变量／样式身份时人工复核。
- **范围**：信息色仅审核文字与图标，不审核录入项背景。第 9 节的中性色候选分子可包含 `color-text-Placeholder (#6F7685)` 暗提示文字，但全局占比的分母仍待 `[[_meta/conflicts]]` #007 确认。
- **后续组件确认**：用户补充“虽然两个颜色一样，但是确实是在组件里的两个token”。因此这两个同色 Token 是组件中实际并存的不同身份，而不是本 Wiki 自拟别名；插件判定应尽量读取组件中的 Token／变量绑定，不能只以 Hex 相等判同。
- **状态**：已编入 Trip v1.6 草稿，Figma 插件未启用。
