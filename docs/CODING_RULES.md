# CODING_RULES.md

This document controls AI implementation behavior.

Project-specific style details may be added here later. Until then, these rules are the default for embedded, robot, RTOS, Linux BSP, and ECU work.

## 1. Authority

The AI may implement the requested change.

The AI must not silently decide architecture, public interfaces, module boundaries, runtime ownership, hardware behavior, timing behavior, protocol behavior, boot behavior, memory layout, safety behavior, or compatibility policy.

If such a decision is needed, stop and ask for confirmation with options and trade-offs.

## 2. Scope Discipline

The AI must:

- modify only files required by the task
- preserve unrelated code and formatting
- avoid opportunistic cleanup
- avoid moving files or renaming symbols unless explicitly requested
- avoid editing generated files unless the task is about the generator or generated output
- update only directly relevant documents

The AI must not widen the task to make implementation easier.

## 3. Architecture Discipline

The AI must:

- keep existing layer boundaries
- respect dependency direction defined by project documents
- keep drivers free of application policy
- keep application code from reaching into private driver, BSP, RTOS, or kernel internals
- keep public interfaces stable unless the task explicitly changes them
- identify known callers before changing shared APIs

The AI must not add abstractions, callbacks, global registries, configuration switches, tasks, message types, or files unless they are required by the task and confirmed when architectural.

## 4. Embedded Runtime Rules

Default runtime rules:

- no heap allocation in deterministic runtime paths unless project documents explicitly allow it
- no recursion in embedded runtime code
- no blocking calls in ISR context
- no logging, printf, sleep, allocation, or heavy parsing in ISR context
- no unbounded loops in control, ISR, driver, or communication paths
- no hidden state changes during initialization
- no unchecked buffer length, index, message length, or frame length
- no silent error handling
- no compatibility break without explicit approval

If a project document provides a tighter rule, follow the tighter rule.

## 5. RTOS Rules

When touching RTOS code, the AI must check:

- task ownership
- priority impact
- stack impact
- blocking behavior
- queue, semaphore, mutex, timer, or event-group ownership
- ISR-to-task handoff
- initialization order
- watchdog and fault behavior

Do not introduce busy waits, priority inversions, unbounded blocking, or task creation as a side effect.

## 6. Driver And BSP Rules

When touching drivers or BSP code, the AI must check:

- hardware ownership
- register or device tree source of truth
- initialization and deinitialization order
- interrupt and DMA lifetime
- buffer ownership
- error paths
- power, clock, and reset behavior
- public API or userspace ABI impact

Do not mix control policy into drivers. Drivers expose capability and state; higher layers decide policy.

## 7. Communication Rules

When touching communication code, the AI must check:

- message ID or endpoint ownership
- frame length
- byte order
- scaling and units
- timeout and retry behavior
- error state behavior
- compatibility with existing senders and receivers
- bus load or scheduling impact

Do not invent protocol fields, IDs, message formats, or diagnostic behavior.

## 8. Robot And Control Rules

When touching robot or control code, the AI must check:

- control-loop frequency
- actuator command authority
- mode transition behavior
- fail-safe behavior
- estimator or sensor timing
- command saturation and limits
- communication loss behavior

Do not change physical behavior as a side effect of a software cleanup.

## 9. Automotive ECU Rules

When touching ECU-like code, the AI must check:

- deterministic behavior
- diagnostics and fault handling
- persistent data compatibility
- calibration data impact
- network signal compatibility
- boot, update, and rollback behavior
- traceability to the task requirement

Do not weaken safety or diagnostic behavior without explicit approval.

## 10. Error Handling

The AI must:

- preserve existing error conventions
- return or propagate errors where the surrounding code expects it
- avoid swallowing failures
- keep fallback behavior explicit
- avoid changing reset, watchdog, degraded-mode, or fault behavior unless required

## 11. Debug Code

Temporary debug code must be removed before final response.

Permanent debug hooks are allowed only when requested or already part of the module design. They must be controlled, documented, and safe for the runtime path.

## 12. Verification

The AI must run the narrowest meaningful available check.

If no executable check exists, the AI must perform manual diff review and say that executable verification was not available.

The AI must never claim a build, test, static analysis, bench check, HIL, SIL, or hardware check passed unless it was actually run.
