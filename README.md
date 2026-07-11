# AI Embedded Workflow Template

这是一个可复用的嵌入式项目 AI 工作流模板。

目标不是堆很多文档，而是让 AI 每次接手任务时都能按固定工程流程恢复上下文、确认边界、执行修改、完成自检，并把重要经验沉淀到仓库中。

## 适用场景

- MCU、BSP、驱动、RTOS、控制算法等嵌入式项目
- RoboMaster 或其他机器人软件
- Linux BSP / Linux Driver
- CAN 通信和嵌入式 C/C++ 项目
- 需要长期保留设计决策和调试经验的项目

## 推荐目录

```text
project/
|-- README.md
|-- AGENTS.md
|-- AI_README.md
|-- docs/
|   |-- INDEX.md
|   |-- AGENT_MODEL_ROLES.md
|   |-- CODING_RULES.md
|   |-- REVIEW_CHECKLIST.md
|   |-- DEBUG_GUIDE.md
|   |-- DECISIONS.md
|   |-- ERROR_CATALOG.md
|   `-- CONTROL_THEORY.md
|-- templates/
|   |-- TASK_TEMPLATE.md
|   |-- ARCHITECTURE_TEMPLATE.md
|   |-- INTERFACE_TEMPLATE.md
|   |-- RTOS_TEMPLATE.md
|   `-- HARDWARE_TEMPLATE.md
`-- prompts/
    |-- debug.md
    |-- review.md
    `-- new_driver.md
```

## 使用方式

1. 将本模板复制到真实项目根目录。
2. 根据项目实际情况填写 `README.md` 和 `docs/INDEX.md`。
3. 让 AI 修改代码前，先读取 `AGENTS.md`、`AI_README.md`、`docs/CODING_RULES.md` 和任务相关文档。
4. 大任务使用 `templates/TASK_TEMPLATE.md` 建立任务输入。
5. 任务完成后，必要时更新 `docs/DECISIONS.md`、`docs/ERROR_CATALOG.md` 或 `docs/CONTROL_THEORY.md`。

## 核心原则

- AI 不得跳过上下文恢复直接写代码。
- 输入任务前先确认当前职责：SOL / TERRA / LUNA。
- AI 不得静默做架构、接口或模块边界决策。
- 小 debug 不写流水账，只保留短记录。
- 长期文档只记录会影响未来工程判断的信息。
- 控制算法文档只保留必要公式、变量、单位、假设、限制和验证。

## 首次启动提示词

```text
本项目使用嵌入式 AI 工程工作流。

开始前请读取：
1. AGENTS.md
2. AI_README.md
3. docs/INDEX.md
4. docs/CODING_RULES.md
5. 当前任务相关文档和源码

然后输出：
- 项目上下文
- 修改范围
- 禁止修改范围
- 风险
- 验证计划

非平凡修改前等待确认。
```
