# AI_README.md

This repository is an AI workflow template for long-term embedded software projects.

It is designed for projects where the codebase may become large, AI sessions may not remember earlier chats, and engineering decisions must remain visible to the human owner.

Target project types include:

- robot software
- STM32 and embedded RTOS firmware
- Linux BSP and driver work
- CAN and communication stacks
- embedded C/C++
- future automotive ECU software

## How An AI Should Use This Template

Start every new session in this order:

1. Read `AGENTS.md`.
2. Read this file.
3. Read `docs/INDEX.md` if present.
4. Read the task supplied by the user, preferably based on `templates/TASK_TEMPLATE.md`.
5. Read `docs/CODING_RULES.md`.
6. Read `docs/DECISIONS.md` and `docs/ERROR_CATALOG.md` if present.
7. Read task-specific project documents.
8. Inspect the relevant source files.
9. State the pre-edit summary required by `AGENTS.md`.
10. Implement only the confirmed scope.
11. Complete `docs/REVIEW_CHECKLIST.md`.
12. Reply using the final output format required by `AGENTS.md`.

Do not use chat history as project truth. Repository files are the durable source of context.

## File Roles

`AGENTS.md` defines the AI operating procedure. It controls how every AI session should recover context, plan, ask for confirmation, edit, verify, and report.

`AI_README.md` explains how to use this template.

`README.md` is the human-facing project overview. It should eventually describe what the real project is, how to build it, and where important documents live.

`docs/INDEX.md` is the durable index for both project documents and code directories.

`templates/TASK_TEMPLATE.md` controls AI input. Use it to describe one implementation task with scope, context, risks, verification, and acceptance criteria.

`docs/CODING_RULES.md` controls AI implementation behavior. It defines what the AI must and must not do while editing code.

`docs/REVIEW_CHECKLIST.md` controls AI output quality. The AI must use it before the final response.

`docs/DECISIONS.md` records why major designs exist, so future AI sessions do not reverse them accidentally.

`docs/ERROR_CATALOG.md` records solved problems, root causes, fixes, and engineering lessons.

`docs/CONTROL_THEORY.md` is a reusable placeholder for observer, estimator, state-vector, and controller design.

## Empty Documents And How To Fill Them

Some files are intentionally empty placeholders. Fill them as the real project becomes concrete.

`docs/AI_PHILOSOPHY.md` should describe how the project owner wants AI agents to collaborate: decision authority, review expectations, communication style, and what must be escalated.

`docs/DEBUG_GUIDE.md` should describe how to debug the project: serial logs, RTOS traces, CAN tools, kernel logs, probes, crash dumps, breakpoints, hardware setup, and what logs are safe to collect.

`docs/GIT_WORKFLOW.md` should describe branch naming, commit rules, review rules, release tags, generated-file policy, and how AI agents should prepare changes.

`docs/INDEX.md` should list important source directories, generated directories, ignored directories, and task-specific document routing.

`docs/DECISIONS.md` should record decisions that affect architecture, interface, protocol, RTOS, hardware, safety, timing, memory, boot, compatibility, or control behavior.

`docs/ERROR_CATALOG.md` should record each solved issue with symptoms, root cause, fix, verification, lesson, and prevention rule.

`docs/CONTROL_THEORY.md` should collect control algorithms, observer design, state-vector definitions, tuning notes, experiments, and mode-transition rules.

`templates/ARCHITECTURE_TEMPLATE.md` should be used to document a subsystem architecture: ownership, layers, dependencies, runtime components, public interfaces, risks, and verification.

`templates/INTERFACE_TEMPLATE.md` should be used to document APIs, CAN frames, messages, sysfs nodes, IOCTLs, device tree bindings, file formats, or any cross-module contract.

`templates/RTOS_TEMPLATE.md` should be used to document RTOS tasks, priorities, queues, timers, mutexes, event groups, ISR handoff, stack assumptions, and timing budgets.

`templates/HARDWARE_TEMPLATE.md` should be used to document hardware assumptions: board, pins, clocks, power, sensors, actuators, buses, interrupts, DMA, reset behavior, and constraints.

`prompts/debug.md` should contain the standard prompt for asking AI to debug a failure without making random changes.

`prompts/review.md` should contain the standard prompt for asking AI to review code without editing files.

`prompts/new_driver.md` should contain the standard prompt for asking AI to create or modify a driver with strict architecture, interface, and verification requirements.

## Recommended Workflow

For a new feature:

1. Fill one copy of `templates/TASK_TEMPLATE.md`.
2. Point the AI to the filled task.
3. Let the AI read the required context.
4. Require confirmation before architecture, interface, or module-boundary changes.
5. Require verification and self-review before accepting the result.

For a new subsystem:

1. Create an architecture document from `templates/ARCHITECTURE_TEMPLATE.md`.
2. Create interface documents from `templates/INTERFACE_TEMPLATE.md`.
3. Add RTOS or hardware documents when relevant.
4. Then create implementation tasks from `templates/TASK_TEMPLATE.md`.

For debugging:

1. Use `prompts/debug.md`.
2. Provide logs and reproduction steps.
3. Ask the AI to separate observations from assumptions.
4. Do not allow code edits until the suspected owner and risk area are identified.
5. After the issue is fixed, add an entry to `docs/ERROR_CATALOG.md`.

For review:

1. Use `prompts/review.md`.
2. Ask for findings first.
3. Do not allow edits unless a follow-up implementation task is created.

## Decision Rule

The AI may execute implementation work.

The AI must not silently decide architecture, public interfaces, module boundaries, hardware behavior, timing behavior, protocol behavior, safety behavior, memory layout, boot behavior, or compatibility policy.

When such a decision appears, the AI must stop, explain options and trade-offs, recommend a direction if possible, and wait for confirmation.

## Minimum Viable Project Context

Before the real project grows, keep at least these documents accurate:

- `README.md`
- `AGENTS.md`
- `AI_README.md`
- `docs/CODING_RULES.md`
- `docs/REVIEW_CHECKLIST.md`
- `docs/INDEX.md`
- `docs/DECISIONS.md`
- `docs/ERROR_CATALOG.md`
- one filled task file based on `templates/TASK_TEMPLATE.md`

As the project grows, add architecture, interface, RTOS, hardware, debug, and git workflow documents. These files are what allow a future AI session to recover context without remembering previous chats.
