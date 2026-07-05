# AI Embedded Workflow Template

这是一个可复用的嵌入式项目 AI 工作流模板。它的目标不是堆很多文档，而是让 AI 每次接手任务时都按固定工程流程恢复上下文、确认边界、执行修改、完成自检。

## 适用场景

- MCU / BSP / 驱动 / RTOS / 控制算法等嵌入式项目。
- 多轮 AI 协作，需要避免遗忘历史决策、误改接口、破坏分层。
- 需要长期沉淀调试经验、设计决策和任务记录的项目。

## 推荐目录

```text
project/
├── README.md
├── AGENTS.md
├── AI_README.md
├── docs/
│   ├── INDEX.md
│   ├── ARCHITECTURE.md
│   ├── INTERFACE.md
│   ├── CODING_RULES.md
│   ├── DEBUG_GUIDE.md
│   ├── DECISIONS.md
│   ├── ERROR_CATALOG.md
│   └── CONTROL_THEORY.md
├── tasks/
│   └── TASK_TEMPLATE.md
├── templates/
└── prompts/
```

## 使用方式

1. 把本模板复制到真实项目根目录。
2. 根据项目实际情况填写 `docs/` 下的核心文档。
3. 让 AI 修改代码前，先要求它读取 `AI_README.md`、`AGENTS.md` 和任务相关文档。
4. 大任务使用 `tasks/TASK_TEMPLATE.md` 建立任务记录。
5. 任务完成后，把设计决策写入 `docs/DECISIONS.md`，把问题经验写入 `docs/ERROR_CATALOG.md`。

## 首次启动提示词

```text
This project uses an AI embedded engineering workflow.
Before doing anything:
1. Read AI_README.md
2. Read AGENTS.md
3. Read docs/INDEX.md
4. Read docs/CODING_RULES.md
5. Read task-related docs and source files

Then summarize:
- project context
- constraints
- files in scope
- files out of scope
- risks
- verification plan

Wait for confirmation before non-trivial edits.
```

## 核心规则

- AI 不能直接开始写代码，必须先确认目标、范围、风险和验证方式。
- 一次任务尽量局部化，避免跨层大改。
- 架构、接口、硬件语义、协议、RTOS 行为和安全策略的变化必须记录。
- 已解决的问题必须沉淀到 `ERROR_CATALOG.md`，避免重复踩坑。
- 重要设计原因必须沉淀到 `DECISIONS.md`，避免后续 AI 推翻历史结论。

## 最小工作流

```text
读取规则 -> 读取任务 -> 确认范围 -> 修改 -> 构建/测试 -> 自检 -> 更新文档 -> 总结
```

这个模板只提供流程骨架。真正的项目事实应写入当前项目自己的 `docs/`、`tasks/` 和源码注释中。
