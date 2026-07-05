# REVIEW_CHECKLIST.md

This checklist controls AI self-review output.

The AI must complete this review before final response.

## 1. Scope

- [ ] I changed only files allowed by the task.
- [ ] I avoided unrelated refactoring, renaming, movement, and formatting.
- [ ] I did not modify generated files unless required.
- [ ] I did not leave temporary experiments or debug code.

## 2. Context

- [ ] I read `AGENTS.md`.
- [ ] I read `AI_README.md` if present.
- [ ] I read `docs/INDEX.md` if present.
- [ ] I read `docs/CODING_RULES.md`.
- [ ] I read `docs/DECISIONS.md` if present.
- [ ] I read `docs/ERROR_CATALOG.md` if present.
- [ ] I read the task-specific documents listed in the task.
- [ ] I inspected the source files before editing.
- [ ] I did not rely on chat history as project truth.

## 3. Engineering Decisions

- [ ] I did not silently make architecture, interface, or module-boundary decisions.
- [ ] If a decision was needed, I stopped and asked for confirmation.
- [ ] I documented assumptions instead of hiding them.
- [ ] I did not invent hardware, timing, protocol, safety, or compatibility facts.

## 4. Architecture

- [ ] Existing layer boundaries remain intact.
- [ ] Dependency direction remains valid.
- [ ] Drivers do not contain application policy.
- [ ] Application code does not depend on private lower-layer internals.
- [ ] Public interfaces remain unchanged unless explicitly required.
- [ ] Known users were checked before changing any shared interface.

## 5. Embedded Runtime Risk

- [ ] No unsafe heap allocation was added to deterministic runtime paths.
- [ ] No recursion was added to embedded runtime code.
- [ ] No unbounded loop was added to runtime-critical code.
- [ ] No blocking call was added to ISR or timing-critical context.
- [ ] No unsafe buffer, length, index, or frame parsing behavior was added.
- [ ] Error handling remains explicit.

## 6. RTOS, ISR, DMA

- [ ] ISR work remains minimal.
- [ ] ISR-to-task handoff remains safe.
- [ ] Task priority, blocking behavior, and stack impact were considered.
- [ ] Queue, semaphore, mutex, timer, or event-group ownership remains clear.
- [ ] DMA, cache, buffer ownership, and memory lifetime remain safe.

## 7. Driver, BSP, Linux Boundary

- [ ] Initialization and deinitialization order remain correct.
- [ ] Register, pin, clock, reset, and power behavior were not changed accidentally.
- [ ] Device tree, sysfs, ioctl, kernel ABI, or userspace ABI changes were explicit.
- [ ] Probe, remove, interrupt, and error paths remain safe where relevant.

## 8. Communication And Control

- [ ] Message IDs, frame lengths, byte order, scaling, and units remain correct.
- [ ] Timeout, retry, and error-state behavior remain intentional.
- [ ] CAN or other bus load impact was considered where relevant.
- [ ] Control-loop timing and actuator command behavior were not changed accidentally.
- [ ] Robot mode transitions and fail-safe behavior remain intentional.

## 9. ECU And Persistent Data

- [ ] Diagnostics and fault handling remain intentional.
- [ ] Persistent data, calibration, and compatibility impact were considered.
- [ ] Boot, update, rollback, or safety behavior was not changed accidentally.
- [ ] Deterministic behavior remains preserved where required.

## 10. Verification

- [ ] The narrowest meaningful build or test was run, or the reason it could not run is stated.
- [ ] Static analysis was run if available and relevant.
- [ ] Generated output was inspected if generators were involved.
- [ ] Hardware, bench, SIL, HIL, or smoke testing needs are stated when relevant.
- [ ] Remaining unverified risk is stated.
- [ ] `docs/ERROR_CATALOG.md` was updated if this task fixed a concrete problem.
- [ ] `docs/DECISIONS.md` was updated if this task confirmed or changed a design decision.
- [ ] `docs/CONTROL_THEORY.md` was updated if this task affected control, observer, estimator, or state-vector design.

## 11. Simplicity

- [ ] The solution is the smallest valid change.
- [ ] No unnecessary abstraction, callback, global, task, config switch, file, or layer was added.
- [ ] The implementation follows nearby patterns.
- [ ] A simpler option was considered.

## 12. Mandatory Final Report

The final response must include:

- `Summary`
- `Files changed`
- `Context used`
- `Verification`
- `Assumptions`
- `Risks`
- `Next`

If any checklist item is not satisfied, the final response must say why.
