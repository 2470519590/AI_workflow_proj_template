# AGENTS.md

This file defines the AI operating procedure for a large embedded repository.

Assume:

- the codebase may exceed 300,000 lines
- every AI session starts with no memory of previous sessions
- chat history is not a source of truth
- repository documents and source code are the only durable context

Do not store project architecture, coding style, board details, pin maps, register values, protocol definitions, safety goals, or hardware assumptions in this file. This file defines how to recover and use that information.

## Prime Directive

Do not modify code until project context has been recovered from repository files.

Before editing, the AI must know:

- what product, target, subsystem, or module is being touched
- which layer owns the behavior
- which interfaces and generated artifacts are involved
- which files are in scope
- which files are out of scope
- which verification path applies
- which embedded risks are present

If this cannot be determined from repository context, stop and ask.

## Engineering Decision Authority

AI may implement approved engineering decisions. AI must not silently make them.

Stop and ask for confirmation before proceeding when a change may affect:

- architecture or layer boundaries
- public interfaces or cross-module contracts
- module ownership or dependency direction
- runtime task structure, scheduling, or communication paths
- hardware behavior, boot behavior, memory layout, timing, safety behavior, or external protocols
- compatibility with existing tools, tests, calibration data, logs, or deployed systems

When stopping for confirmation, provide:

- the decision that must be made
- viable options
- trade-offs of each option
- recommended option, if one is clearly better
- files and interfaces likely to be affected
- verification required after the decision

Do not proceed until the user confirms the direction.

## Context Recovery Order

At the start of every implementation session, read context in this order:

1. `AGENTS.md`
2. repository entry document, usually `README.md`
3. project context index, usually `docs/INDEX.md` or `docs/PROJECT_CONTEXT.md`
4. architecture map
5. module ownership or subsystem map
6. interface or protocol registry
7. build, flash, test, and debug instructions
8. known risks, decisions, limitations, and issue logs, especially `docs/DECISIONS.md` and `docs/ERROR_CATALOG.md` when present
9. task-specific module documents
10. task-specific source files

Read only the documents needed for the task. Do not scan the entire repository unless the task requires it.

If a context document does not exist, say so in the pre-edit summary. Use source code as fallback only after checking for documents.

## Required Repository Context Files

Large embedded projects should maintain durable context files. Names may differ, but the information must exist somewhere:

- project overview: product purpose, targets, major software domains
- architecture map: layers, dependency direction, runtime boundaries
- module ownership map: which subsystem owns which files and behavior
- interface registry: public APIs, messages, CAN frames, IOCTLs, sysfs nodes, device tree bindings, shared data contracts
- build matrix: supported targets, toolchains, generated outputs
- verification matrix: build, unit, integration, HIL, SIL, bench, static analysis, smoke tests
- debug guide: logging, tracing, probes, crash dumps, serial ports, kernel logs, RTOS traces
- risk register: timing, safety, boot, memory, concurrency, protocol, hardware, and integration risks
- decision log: important design decisions and rejected alternatives
- error catalog: solved problems, root causes, fixes, verification, lessons, and prevention rules
- control theory document when the project includes observers, estimators, controllers, or actuator command policies
- change log or session notes: recent architectural or integration changes

If these files are missing, do not invent their contents. Mention the gap and proceed only when the task is still local and low risk.

## Pre-Edit Gate

Before editing any file, output this compact summary:

- `Task`: one sentence
- `Context read`: documents and source files read
- `Subsystem`: robot, RTOS, BSP, driver, ECU, middleware, application, tooling, or unknown
- `Owner`: module or layer that owns the behavior
- `Interfaces`: APIs, messages, buses, device tree nodes, tasks, queues, files, or generated artifacts affected
- `In scope`: files or behavior to change
- `Out of scope`: files or behavior that must not change
- `Decision needed`: `none`, or the architecture/interface/boundary decision that requires confirmation
- `Risks`: timing, ISR, DMA, memory, boot, protocol, safety, Linux boundary, RTOS scheduling, or none known
- `Plan`: 2 to 5 concrete steps
- `Verification`: exact check planned

If `Subsystem`, `Owner`, or `Interfaces` is unknown for a non-trivial code change, do not edit. If `Decision needed` is not `none`, do not edit until the user confirms the decision.

## Task Routing

Classify the task before editing.

Robot software:

- identify control loop, estimation, actuator, referee, vision, chassis, gimbal, shooter, communication, or supervision boundary
- check timing, command authority, fail-safe behavior, bus load, and mode transitions

Embedded RTOS:

- identify task, ISR, queue, timer, mutex, DMA, memory ownership, and priority impact
- check blocking behavior, stack usage, initialization order, and ISR-to-task handoff

Linux BSP or driver:

- identify kernel, device tree, bootloader, rootfs, userspace API, sysfs, ioctl, probe/remove, power management, or interrupt path
- check ABI compatibility, device tree binding, concurrency, lifetime, and error paths

Automotive ECU:

- identify network signal, diagnostic path, state machine, nonvolatile data, calibration, safety mechanism, or boot/update path
- check deterministic behavior, compatibility, fault handling, timing, and traceability

If the task crosses domains, name each domain and keep the change split by boundary.

## Scope Rules

Allowed changes:

- files directly required by the task
- tests or documentation directly required by the task
- build or configuration files only when required for integration

Forbidden without explicit approval:

- unrelated refactoring
- broad formatting
- renaming public symbols or files
- moving directories
- replacing an established mechanism with a preferred one
- editing generated files instead of their source
- changing public interfaces without identifying all known users
- changing startup, linker, memory layout, task priority, ISR behavior, DMA behavior, protocol format, persistent storage, device tree binding, boot flow, or safety behavior as a side effect

When a broader change is required, stop and explain the required boundary expansion, options, trade-offs, and recommended direction.

## Architecture Rules

Preserve existing boundaries.

Before changing cross-module behavior, identify:

- dependency direction
- public interface
- private implementation files
- runtime owner
- build target impact
- test impact

Do not add new abstractions, callbacks, globals, tasks, configuration switches, message types, files, or layers unless the task requires them and the existing design cannot solve the problem cleanly.

If the implementation may change architecture, interfaces, ownership, or dependency direction, stop before editing. Explain the trade-offs and ask for confirmation.

Prefer a small local fix over a new framework.

## Context Size Control

Avoid context explosion.

Use this order:

1. read durable context documents
2. inspect module entry points
3. inspect direct dependencies
4. inspect callers and users of changed interfaces
5. inspect tests and build files

Do not read unrelated subsystems. Do not summarize the whole project. Summarize only what affects the task.

## Implementation Rules

During implementation:

- change one boundary at a time
- keep public behavior unchanged unless the task requires change
- keep temporary debug code out of the final diff
- update directly affected context documents when behavior, interface, build, verification, or risk changes
- update the decision log when a design reason is confirmed or changed
- update the error catalog after completing a debugging or defect-fix task
- do not use chat history as justification
- do not claim compatibility without checking known users or documents

## Logs And Debugging

For logs, traces, CAN frames, serial output, RTOS traces, kernel logs, crash dumps, or debugger output:

- keep only relevant excerpts
- preserve timestamps, IDs, addresses, error codes, frame IDs, state transitions, and task or CPU context when important
- separate observed facts from assumptions
- do not treat one log line as proof
- remove temporary instrumentation unless explicitly kept
- document permanent debug hooks and how they are enabled

## Verification Rules

Run the narrowest meaningful verification available:

- compile affected target
- run unit or module tests
- run static analysis if available for the touched area
- run integration, SIL, HIL, bench, or smoke test when required by the risk
- inspect generated output if generators are involved
- perform manual diff review if no executable check exists

Never say verification passed unless it was run. If verification is not possible, state the exact reason.

## Missing Information

If information is missing:

1. search repository documents
2. search source files and nearby module docs
3. inspect tests and build scripts
4. state what is still unknown
5. proceed only if the unknown is low risk
6. ask the user if the unknown affects architecture, safety, timing, hardware behavior, boot, memory, RTOS scheduling, interrupts, DMA, external protocols, or persistent data

Do not invent facts to continue.

Do not resolve missing architecture or interface information by making a design choice silently.

## Self-Review Gate

Before final response, review the diff and answer:

- Which files changed?
- Why did each file change?
- Did the change stay inside the stated scope?
- Did I make any engineering decision that should have required confirmation?
- Did any public interface or generated artifact change?
- Did any high-risk embedded area change?
- Did architecture boundaries remain intact?
- Were unnecessary abstractions, globals, tasks, callbacks, configs, or files added?
- Could the implementation be simpler?
- What verification passed?
- What was not verified?
- What risk remains?
- What context document should be updated next?
- Did this task require a `docs/DECISIONS.md` or `docs/ERROR_CATALOG.md` update?

Fix issues found during self-review before responding unless user approval is required.

## Final Response Format

Use this format after implementation:

- `Summary`: what changed
- `Files changed`: each file and why
- `Context used`: key documents or source areas used
- `Verification`: checks run and result
- `Assumptions`: explicit assumptions or `none`
- `Risks`: remaining risks or `none known`
- `Next`: next useful engineering step

Keep the response short and specific.

## Review-Only Requests

If the user asks for review only, do not edit files.

Report:

- findings first, ordered by severity
- file and line references when possible
- affected boundary or risk area
- missing verification
- open questions

If there are no findings, say so directly and mention remaining test gaps.
