# Entalpa Requirement Writing Style

Use this reference when creating, rewriting, or reviewing requirement text.

## Requirement Statement

Write one testable obligation per requirement. Prefer:

- "The system shall ..."
- "The API shall ..."
- "The operator shall be able to ..."

Avoid vague verbs such as "handle", "support", "improve", or "optimize" unless acceptance criteria make them measurable.

## Acceptance Criteria

Acceptance criteria should make verification obvious. Include:

- Observable condition.
- Input or precondition.
- Expected output or state change.
- Boundary, timing, or error behavior when relevant.

Do not use acceptance criteria as implementation notes. Put implementation ideas in `guidance` or `implementation_notes`.

## Rationale

Explain why the requirement matters. Tie it to:

- A story or stakeholder need.
- A safety, compliance, reliability, cost, or usability concern.
- A project assessment gap.

## Risk

State the consequence of missing the requirement. Good risk text names what can fail and who is affected.

## Category and Component

Use existing project vocabulary when visible. If none is visible:

- `functional`: user-visible behavior or business workflow.
- `nonFunctional`: performance, reliability, scalability, availability.
- `constraint`: technology, regulatory, deployment, compatibility, or process constraint.
- `interface`: data, trigger, or state behavior across a boundary.
- `process`: workflow, procedure, or operational process expectation.
- `usability`: interaction quality and accessibility.
- `human`: an actor's expected behavior or operational responsibility.

Set `component` to the subsystem, module, UI, API, workflow, or operational area affected by the requirement.

## Priority

Use the project's existing priority vocabulary if present. Otherwise prefer `must`, `should`, `could`, or `would`.

## Anti-Patterns

Avoid:

- Combining unrelated obligations in one requirement.
- Creating requirements with no acceptance criteria.
- Losing traceability to source stories.
- Rewriting stable wording only for style when the user asked for a narrow change.
- Inventing stakeholders, subsystems, or interface contracts without signaling assumptions.
