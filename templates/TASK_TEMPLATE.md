# TASK_TEMPLATE.md

Use this file to describe one AI implementation task.

This template controls the AI input. Fill it before asking an AI agent to modify code.

## 1. Task

Title:

One-sentence goal:

## 2. Target Area

Project/domain:

Target board or platform:

Subsystem:

Layer:

Owner module:

## 3. Context The AI Must Read

Required documents:

- `AGENTS.md`
- `AI_README.md`
- `docs/INDEX.md`
- `docs/CODING_RULES.md`
- `docs/REVIEW_CHECKLIST.md`
- `docs/DECISIONS.md`
- `docs/ERROR_CATALOG.md`

Task-specific documents:

- 

Source files to inspect before editing:

- 

## 4. Strict Scope

Files or directories allowed to change:

- 

Files, directories, interfaces, or behavior that must not change:

- 

Non-goals:

- 

## 5. Functional Requirements

The implementation must:

- 

The implementation must not:

- 

## 6. Interfaces And Contracts

Public APIs affected:

- none

Messages, CAN frames, IOCTLs, sysfs nodes, device tree nodes, files, or external contracts affected:

- none

Generated files affected:

- none

Backward compatibility requirement:

- unchanged unless explicitly approved

## 7. Engineering Decisions

May the AI make architecture, interface, or module-boundary decisions?

- No. The AI must stop, explain options and trade-offs, and ask for confirmation.

Known decision already approved for this task:

- none

## 8. Embedded Risk Areas

Mark all that apply:

- [ ] ISR or interrupt behavior
- [ ] RTOS task, priority, queue, timer, mutex, or blocking behavior
- [ ] DMA, cache, memory lifetime, or buffer ownership
- [ ] startup, bootloader, linker, memory map, or initialization order
- [ ] hardware register, pin, clock, or power behavior
- [ ] CAN, UART, SPI, I2C, Ethernet, USB, or other protocol behavior
- [ ] Linux kernel, BSP, device tree, sysfs, ioctl, or userspace ABI
- [ ] persistent storage, calibration, diagnostics, or compatibility data
- [ ] safety, fail-safe, watchdog, fault handling, or degraded mode
- [ ] timing, control loop, actuator command, or robot mode transition
- [ ] none known

Risk notes:

- 

## 9. Constraints

Implementation constraints:

- Follow `docs/CODING_RULES.md`.
- Do not perform unrelated refactoring.
- Do not modify files outside the strict scope.
- Do not introduce temporary debug code into the final diff.
- Do not change public interfaces unless explicitly listed in this task.

Task-specific constraints:

- 

## 10. Verification

Required verification:

- build:
- test:
- static analysis:
- manual inspection:
- hardware, bench, SIL, HIL, or smoke test:

If a check cannot be run, the AI must state why.

## 11. Acceptance Criteria

The task is complete only when:

- 

## 12. Required Final Output

The AI final response must include:

- `Summary`
- `Files changed`
- `Context used`
- `Verification`
- `Assumptions`
- `Risks`
- `Next`

The AI must complete `docs/REVIEW_CHECKLIST.md` before final response.

## 13. Long-Term Records

Update `docs/ERROR_CATALOG.md` if this task fixes a concrete failure, bug, regression, communication issue, hardware bring-up issue, or debugging problem.

Update `docs/DECISIONS.md` if this task confirms or changes an engineering decision.

Update `docs/CONTROL_THEORY.md` if this task affects observer, estimator, controller, state-vector, tuning, saturation, mode switching, or actuator command behavior.
