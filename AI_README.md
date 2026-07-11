# AI_README.md

本仓库是一个长期嵌入式项目的 AI 工作流模板。

它解决的问题不是“让 AI 多写代码”，而是让每次新的 AI 会话都能从仓库文件恢复上下文、确认边界、避免静默决策，并在完成后留下可追溯的工程记录。

适用项目：

- 机器人软件
- STM32 / MCU / RTOS 固件
- Linux BSP 和驱动
- CAN 和通信协议栈
- 嵌入式 C/C++
- 未来汽车 ECU 软件

## 1. AI 使用顺序

每次新会话按顺序执行：

1. 读取 `AGENTS.md`
2. 读取本文件
3. 读取 `docs/INDEX.md`
4. 读取用户任务，优先使用 `templates/TASK_TEMPLATE.md`
5. 读取 `docs/CODING_RULES.md`
6. 读取 `docs/DECISIONS.md` 和 `docs/ERROR_CATALOG.md`
7. 读取任务相关文档
8. 检查相关源码
9. 输出 `AGENTS.md` 要求的动手前摘要
10. 只实现已确认范围
11. 完成 `docs/REVIEW_CHECKLIST.md`
12. 按 `AGENTS.md` 的最终格式回复

聊天记录不是项目事实。仓库文件才是持久上下文。

## 2. 文件角色

`AGENTS.md`：AI 工作流程总规则。

`AI_README.md`：告诉 AI 如何使用本模板。

`README.md`：给人看的项目概览。

`docs/INDEX.md`：项目文档和代码目录索引。

`templates/TASK_TEMPLATE.md`：控制任务输入，防止任务描述失控。

`docs/CODING_RULES.md`：控制 AI 实现行为。

`docs/REVIEW_CHECKLIST.md`：控制 AI 最终自检和输出质量。

`docs/DECISIONS.md`：记录持久工程决策，防止后续 AI 推翻历史结论。

`docs/ERROR_CATALOG.md`：记录已解决问题、根因、修复和经验。

`docs/CONTROL_THEORY.md`：记录必须长期保持一致的控制算法、观测器、估计器、状态量和命令语义。

## 3. 文档简洁规则

本模板刻意防止文档膨胀。

AI 不得创建流水账。任务文档应描述目标、范围、风险和结果，不记录每条命令、每次失败尝试或重复观察。

记录去向：

- 小 debug 观察：放在父任务的 `Debug Short Log`
- 已解决缺陷：写入 `docs/ERROR_CATALOG.md`
- 已确认设计决策：写入 `docs/DECISIONS.md`
- 需要长期保持的控制行为：写入 `docs/CONTROL_THEORY.md`

控制文档必须让控制工程学生能读懂。只写必要公式、变量、单位、假设、限制和验证。除非用户明确要求，不写长推导和调参日记。

## 4. 空文档怎么用

这些文件可以先空着，等真实项目需要时再填：

`docs/AI_PHILOSOPHY.md`：记录项目主人希望 AI 如何协作，包括决策权限、review 期望、沟通风格和必须升级确认的情况。

`docs/DEBUG_GUIDE.md`：记录调试入口，包括串口、RTOS trace、CAN 工具、kernel log、探针、crash dump、硬件连接和可采集日志。

`docs/GIT_WORKFLOW.md`：记录分支、提交、review、tag、生成文件策略，以及 AI 如何准备变更。

`templates/ARCHITECTURE_TEMPLATE.md`：用于记录子系统架构。

`templates/INTERFACE_TEMPLATE.md`：用于记录 API、CAN 帧、消息、sysfs、ioctl、设备树 binding、文件格式等跨模块契约。

`templates/RTOS_TEMPLATE.md`：用于记录任务、优先级、队列、定时器、互斥锁、事件组、ISR 交接、栈和时序预算。

`templates/HARDWARE_TEMPLATE.md`：用于记录板级假设、引脚、时钟、电源、传感器、执行器、总线、中断、DMA 和复位行为。

`prompts/debug.md`：调试类提示词，要求 AI 先定位归属和风险，再改代码。

`prompts/review.md`：review 类提示词，要求 AI 只报告问题，不改文件。

`prompts/new_driver.md`：驱动类提示词，要求 AI 明确架构、接口和验证。

## 5. 推荐工作流

新功能：

1. 复制并填写 `templates/TASK_TEMPLATE.md`
2. 指定 AI 使用该任务文件
3. 让 AI 读取必要上下文
4. 架构、接口、模块边界变化前必须确认
5. 实现后要求验证和自检

新子系统：

1. 用 `templates/ARCHITECTURE_TEMPLATE.md` 建立架构文档
2. 用 `templates/INTERFACE_TEMPLATE.md` 建立接口文档
3. 需要时补充 RTOS 或硬件文档
4. 再拆分为具体任务

调试：

1. 使用 `prompts/debug.md`
2. 提供最小复现和关键日志
3. 要求 AI 区分观察和假设
4. 未识别归属和风险前，不允许随意改代码
5. 修复后写入 `docs/ERROR_CATALOG.md`
6. 小 debug 尝试不要单独建任务流水账

Review：

1. 使用 `prompts/review.md`
2. findings first
3. 不允许编辑文件
4. 需要修复时另建任务

## 6. 决策规则

AI 可以执行实现工作。

AI 不得静默决定架构、公共接口、模块边界、硬件行为、时序行为、协议行为、安全行为、内存布局、启动行为或兼容策略。

出现这类决策时，AI 必须停止，说明选项和取舍，必要时推荐方向，并等待确认。

## 7. 最小可用上下文

真实项目启动前，至少保持这些文件准确：

- `README.md`
- `AGENTS.md`
- `AI_README.md`
- `docs/INDEX.md`
- `docs/CODING_RULES.md`
- `docs/REVIEW_CHECKLIST.md`
- `docs/DECISIONS.md`
- `docs/ERROR_CATALOG.md`
- 一个基于 `templates/TASK_TEMPLATE.md` 的任务文件

项目变大后，再补充架构、接口、RTOS、硬件、调试和 Git 工作流文档。
