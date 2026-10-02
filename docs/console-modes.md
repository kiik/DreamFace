# Console modes

The four modes are a proposed control surface for the agentic loop. The key distinction is the amount of planning, user verification, and delegated execution—not the agent's underlying capabilities.

| Mode | Planning and execution | User checkpoints | Intended use |
| --- | --- | --- | --- |
| **Plan** | Inspect and structure the request; emit assumptions, dependencies, risks, and proposed work items. Do not mutate the project or invoke effectful tools. | User decides whether and how to proceed. | Dry prework and scope negotiation. |
| **Build** | Execute bounded increments from an agreed plan. | Pause at defined verification points, especially before scope changes or consequential mutations. | Collaborative implementation and learning. |
| **Auto** | Execute the agreed scope end-to-end, making routine local decisions and reporting them. | No routine pause; surface blockers, unexpected scope changes, and decisions outside the agreed bounds. | Delegated execution within explicit constraints. |
| **Horde** | Decompose work into a work-item tree, identify independent branches, and coordinate multiple agents where available. | Report decomposition and integrate/review branch results; escalation rules remain configurable. | Parallel research or implementation with explicit ownership and dependencies. |

## Work decomposition

Represent the initial request as a root node and classify each bounded item as primarily delegative, procedural, or imperative. Items may receive stable hierarchical identifiers such as `DF-1`, `DF-1.1`, and `DF-1.1.1`; a draft record format exists as [work-item.schema.json](../schema/work-item.schema.json). Preserve explicit dependencies and cross-links; sequence labels should not imply that all work is serial.

Each work item should be small enough to describe with an outcome, owner/actor, inputs, completion condition, and verification evidence. New chat turns may:

- **deepen** the graph by adding constraints, evidence, or relations to existing work; or
- **widen** it by introducing independent work items that may be parallelized or moved to separate contexts.

The system should retain a link to the originating request and clarify when a new task changes scope.

## Shared invariants to test

- Users can inspect the plan and current mode.
- Mode changes and execution boundaries are visible.
- Work items can be traced to request context and completion evidence.
- Parallel branches have defined ownership and integration checks.
- A mode label alone does not imply a security guarantee; concrete tool permissions and confirmation behavior need separate specification.

These definitions are proposals. RFCs should describe observable behavior and tests before a mode is presented as implemented.

## Native alignment

Layer 0 already provides hooks for the control surface: OpenCode records a per-turn `mode` on assistant messages, `subtask` is the native delegation primitive that Horde-style decomposition would build on, and `step-start`/`step-finish` parts bound the steps whose visibility mode policies would govern. See the [context ontology](context-ontology.md).
