# new_driver.md

请按本项目 AI 工作流创建或修改驱动。

要求：

- 先读取 `AGENTS.md`、`AI_README.md`、`docs/AGENT_MODEL_ROLES.md`、`docs/INDEX.md`、`docs/CODING_RULES.md`。
- 驱动实现默认使用 TERRA；涉及接口、设备树、ABI、中断、DMA 或硬件行为决策时升级到 SOL。
- 读取相关硬件、接口、RTOS、BSP、调试文档。
- 未确认硬件事实、接口契约和归属模块前，不要写代码。
- 驱动只暴露能力和状态，不承载应用控制策略。
- 涉及公共接口、设备树、ABI、中断、DMA、时序或硬件行为变化时，先请求确认。

动手前请输出：

- 目标硬件
- 驱动归属
- 公共接口
- 中断 / DMA / buffer 归属
- 初始化和错误路径
- 风险
- 验证计划
