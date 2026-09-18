# Local manual workflow

Adopted playbook version/commit:
Local adaptations and reason:
Role-to-model mapping:

## Ownership

- Human starts sessions and owns product decisions/experience acceptance. One active writer.
- Economical model: routine work against established patterns.
- Capable model: architecture and critical cancellation/concurrency/persistence/state reasoning; may implement efficient localized repairs.
- After one unsuccessful economical-model repair submission on a finding, reassess ownership before another assignment. Do not reset the count by renaming the task.

## Direct human corrections

Small, clear issues within existing requirements may go directly to the implementer. Record build, reproduction, expected/observed behavior and affected checks. Escalate critical or ambiguous issues before editing. Save handback and mark changed code pending review. Owner may continue testing; review the accumulated delta at the next checkpoint.

## Evidence and stopping

Implementer runs proportionate authorized checks. Diff-first review includes necessary dependencies; re-review starts from prior findings and repair delta. Separate blockers from optional improvements. Do not weaken tests or repeat green suites without cause. Label self-verification and independent review honestly.

Record code verdict separately from human acceptance and unverified items. Phase clearance needs required evidence; do not start the next phase without clearance. Device/production operations follow the project's explicit authorization boundary.

## Records

TASK owns assignment; HANDBACK owns submission evidence; REVIEW owns verdict/findings; OWNER-CHECKS owns human results; CURRENT owns the active pointer. Preserve prior evidence in Git or an explicit submission snapshot before replacement. Promote lasting constraints to component contracts; archive narrative outside startup reading. Provide a short next-role prompt to the human.
