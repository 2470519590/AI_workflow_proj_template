# review.md

请按本项目 AI 工作流进行 review。

要求：

- 只做 review，不修改文件。
- 先读取 `AGENTS.md`、`AI_README.md`、`docs/AGENT_MODEL_ROLES.md`、`docs/CODING_RULES.md`、`docs/REVIEW_CHECKLIST.md`。
- 高风险 review 使用 SOL；低风险文档整理可用 LUNA。
- findings first，按严重程度排序。
- 重点检查 bug、行为回归、架构边界、接口兼容、RTOS/ISR/DMA 风险、验证缺口。
- 不要写泛泛建议。

请输出：

- Findings
- Open questions
- Missing verification
- Residual risks

如果没有发现问题，直接说明，并指出剩余测试缺口。
