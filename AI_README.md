# AI_README.md

本仓库是长期嵌入式项目的 AI 工作流模板。

目标：让每次新 AI 会话从仓库文件恢复上下文、确认职责和边界、避免静默决策，并留下必要工程记录。

适用：机器人、STM32/MCU/RTOS、Linux BSP/Driver、CAN、嵌入式 C/C++、汽车 ECU。

## 1. 最小启动流程

1. 读 `AGENTS.md`。
2. 读本文件。
3. 读 `docs/AGENT_MODEL_ROLES.md`。
4. 读 `docs/INDEX.md`。
5. 读任务，优先使用 `templates/TASK_TEMPLATE.md`。
6. 读 `docs/CODING_RULES.md`。
7. 按任务需要读 `DECISIONS`、`ERROR_CATALOG` 和模块文档。
8. 检查相关源码。
9. 输出动手前摘要。
10. 只实现已确认范围。
11. 完成 `docs/REVIEW_CHECKLIST.md`。

聊天记录不是项目事实。仓库文件才是持久上下文。

## 2. 核心文件

- `AGENTS.md`：每次会话必须遵守的入口门禁。
- `AI_README.md`：本模板如何使用。
- `README.md`：给人看的项目概览。
- `docs/INDEX.md`：文档和代码入口索引。
- `docs/AGENT_MODEL_ROLES.md`：SOL / TERRA / LUNA 职责和模型映射。
- `docs/CODING_RULES.md`：实现行为规则。
- `docs/REVIEW_CHECKLIST.md`：最终自检清单。
- `templates/TASK_TEMPLATE.md`：任务输入模板。
- `docs/DECISIONS.md`：持久工程决策。
- `docs/ERROR_CATALOG.md`：已解决问题、根因和经验。
- `docs/CONTROL_THEORY.md`：控制算法、状态量、观测器、估计器和命令语义。

## 3. 职责选择

任务前先声明职责：

- `SOL`：架构、高风险 review、复杂调试、系统设计。
- `TERRA`：编码、bug fix、驱动、RTOS 实现。
- `LUNA`：文档、解释、简单分析、重复任务。

选择原则：

- 能用 `LUNA` 不用 `TERRA`。
- 能用 `TERRA` 不用 `SOL`。
- 涉及架构、接口、协议、模块边界、硬件行为、时序、安全或兼容性时，升级到 `SOL`。

建议任务开头：

```text
当前职责：TERRA
任务：...
范围：...
禁止：不得改接口/协议/架构
验证：...
```

## 4. 文档去向

- 小 debug 观察：放在父任务的 `Debug Short Log`。
- 已解决缺陷：写入 `docs/ERROR_CATALOG.md`。
- 已确认设计决策：写入 `docs/DECISIONS.md`。
- 需要长期保持的控制行为：写入 `docs/CONTROL_THEORY.md`。

禁止流水账、长日志、重复记录和控制算法论文。控制文档只写必要公式、变量、单位、假设、限制和验证。

## 5. 常用工作流

新功能：

1. 用 `templates/TASK_TEMPLATE.md` 写任务。
2. 默认指定 `TERRA`。
3. 架构/接口/边界变化前升级到 `SOL`。
4. 实现后验证并自检。

新子系统：

1. 先用 `SOL` 确认架构边界。
2. 填 `ARCHITECTURE_TEMPLATE` 和 `INTERFACE_TEMPLATE`。
3. 再拆成 `TERRA` 可执行任务。

调试：

1. 复杂问题先用 `SOL` 定位风险。
2. 明确修复范围后交给 `TERRA`。
3. 修复后更新 `ERROR_CATALOG`。

Review：

1. 高风险 review 用 `SOL`。
2. 低风险整理用 `LUNA`。
3. 只 review 时不得编辑文件。

## 6. 空文档用途

- `docs/AI_PHILOSOPHY.md`：AI 协作偏好和升级确认规则。
- `docs/DEBUG_GUIDE.md`：调试入口和日志规则。
- `docs/GIT_WORKFLOW.md`：分支、提交、review、tag、生成文件策略。
- `templates/ARCHITECTURE_TEMPLATE.md`：子系统架构。
- `templates/INTERFACE_TEMPLATE.md`：API、消息、CAN、sysfs、ioctl、设备树 binding 等契约。
- `templates/RTOS_TEMPLATE.md`：任务、优先级、队列、ISR 交接、栈和时序。
- `templates/HARDWARE_TEMPLATE.md`：板级、引脚、时钟、电源、总线、中断、DMA、复位。
- `prompts/debug.md`：调试提示词。
- `prompts/review.md`：review 提示词。
- `prompts/new_driver.md`：驱动提示词。

## 7. 最小可用上下文

真实项目至少维护：

- `README.md`
- `AGENTS.md`
- `AI_README.md`
- `docs/AGENT_MODEL_ROLES.md`
- `docs/INDEX.md`
- `docs/CODING_RULES.md`
- `docs/REVIEW_CHECKLIST.md`
- `docs/DECISIONS.md`
- `docs/ERROR_CATALOG.md`
- 一个基于 `templates/TASK_TEMPLATE.md` 的任务文件
