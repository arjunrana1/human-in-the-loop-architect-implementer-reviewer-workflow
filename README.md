# human-in-the-loop-architect-implementer-reviewer-workflow
A reusable, model-independent workflow

Your usual prompts would be:
Codex review
Read AGENTS.md and resume the current task as reviewer. Review the recorded submission and unresolved findings.

GLM implementation
Read AGENTS.md and implement the current task assigned to GLM. Save the handback when finished.

Your testing results
Read AGENTS.md and resume the current owner-validation task. Here are my results by checklist ID: …


Send directly to GLM
Examples:
- Incorrect text, spacing, alignment, or an icon.
- A straightforward visual mismatch with the agreed design.
- A small correction whose expected behavior is already specified.
Give it the reproduction, expected result, and a screenshot if useful.
Bring to Codex first
Issues involving:
- Lost data, permissions, cancellation, lifecycle, or inconsistent state.
- Duplicate actions/events, timing, or persistence.
- Unclear expected behavior or a new product decision.
- A supposedly small fix that failed once.
Small-looking symptoms can have complex causes. GLM should inspect the issue and escalate if the fix crosses these boundaries.
