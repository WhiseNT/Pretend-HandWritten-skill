# 示例：生成出的模仿 Skill 包（新版说明）

这是 `pretend-handwritten` 在完成风格蒸馏后应输出的标准模仿 Skill 成品（精简版说明），目的是让下游模型或工程师能立即使用或验证产物。

核心理念：上游做充分的证据蒸馏（feature inventory + 频率分析 + 来源分类），下游仅消费已整理好的结论并按**仿写决策顺序**与**证据优先级**执行，不在运行时做来源归因。

包含文件与使用要点：

- `SKILL.md`：技能主体，描述触发场景、执行顺序、仿写决策顺序与证据优先级（下游运行时不得重新判断来源）。
- `references/style-profile.md`：完整风格报告，必须包含 **特征总表**（每条特征有归因、信号强度、置信度、证据、纳入策略）与 **频率概览**（注释频率、常用内容频率）。
- `references/representative-snippets.md`：按语言与层级组织的代表性代码片段，供下游直接参照微习惯（命名、控制流、错误处理等）。
- `evals/evals.json`：至少包含 3 组验证用例（报告生成、按风格续写、来源边界维持）。

快速使用流程：

1. 上游：运行蒸馏流程并产出 `references/style-profile.md`（含 feature total）与 `references/representative-snippets.md`（涵盖多语言/多层级/多来源）。
2. 下游：加载 `SKILL.md`，按 `仿写决策顺序` 执行：近邻文件 → 目标语言高置信度规则 → 代表性片段 → 跨语言共性 → 社区常规补全。
3. 证据冲突时按 `证据优先级` 取舍（近邻源码优先）。

设计要点提醒：

- 上游风格报告必须列出“所有发现的特征”并标注信号强度与置信度，避免把外部 API / 框架约定误记为用户偏好。请参见 `references/style-profile.md`。
- 下游 Skill 不应包含运行时代价的来源判断逻辑；来源边界与禁止误迁移规则应保留在上游报告中。请参见 `SKILL.md` 中的运行时约束。
- README 与 SKILL 的说明应能让审核者或下游模型明确知道输入（样本范围）、产物（哪些文件）与限制（能力边界、诚实边界）。

参阅：

- [SKILL.md](pretend-handwritten/references/generated-style-skill-example/SKILL.md)
- [references/style-profile.md](pretend-handwritten/references/generated-style-skill-example/references/style-profile.md)
- [references/representative-snippets.md](pretend-handwritten/references/generated-style-skill-example/references/representative-snippets.md)
- [evals/evals.json](pretend-handwritten/references/generated-style-skill-example/evals/evals.json)

如果你希望我：

- 生成或压缩当前 `references/style-profile.md` 的梗概，请回复“梗概”。
- 为此示例包生成或更新 `evals/evals.json` 测试用例，请回复“生成 evals”。

---
更新记录：2026-04-20 — 将 README 更新为新版说明，强调 feature total、频率概览、仿写决策顺序与证据优先级。
