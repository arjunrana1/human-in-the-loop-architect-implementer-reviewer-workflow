# Human-in-the-loop architect–implementer–reviewer workflow

A reusable, model-independent method for token- and time-efficient AI development, with a human coordinating handoffs and owning product acceptance.

Use a capable model for architecture, difficult implementation and review; use an economical model for suitable routine work. Keep assignments and evidence in the repository so fresh sessions do not need the complete chat or project history. Roles are flexible: a reviewer may implement a small precise repair, and a strong model should own critical logic when delegation would create expensive repair cycles.

**Manual orchestration. No agent framework, background supervisor or automated dispatch is required.** Efficiency is measured per accepted change, not assumed from a model's token price.

## Start here

- [Detailed playbook](PLAYBOOK.md): objectives, file responsibilities, context loading, review/repair rules, record lifecycle and two flowcharts.
- [Templates](templates/README.md): small starting files to adapt, not a mandatory document bundle.
- [Worked example](examples/manual-handoff.md): a fictional owner-testing issue, direct correction and review checkpoint.
- [Changes](CHANGELOG.md): version history. Current reference: **1.0**.

## Adopt in a project

1. Read the playbook once during setup and inspect existing project instructions.
2. Preserve current records and uncommitted edits. Extract active constraints and open obligations before archiving old logs.
3. Create a short `AGENTS.md`, current-task pointer and local workflow rules; reuse existing specifications and component documentation.
4. Assign one bounded task with scope, base, relevant context, acceptance checks and stop condition.
5. Verify fresh reviewer, implementer and owner-feedback sessions find the right records.

Keep adapted working instructions locally and record the upstream version/commit you adopted. Do not fetch the entire guide each session or silently apply upstream changes. The smallest project may combine related records; create documents only when useful.

## Usual prompts

**Codex review**

> Read AGENTS.md and resume the current task as reviewer. Review the recorded submission and unresolved findings.

**GLM implementation**

> Read AGENTS.md and implement the current task assigned to GLM. Save the handback when finished.

**Your testing results**

> Read AGENTS.md and resume the current owner-validation task. Here are my results by checklist ID: …

Codex and GLM are examples; substitute the models and tools available to you. Verify how each harness discovers instructions. An explicit `AGENTS.md` prompt makes the entry procedure clear.

## Send small testing issues directly to the implementer

You do not need to report every typo or visual mismatch to the architect. Send the tested build, steps, expected/observed behavior, and a screenshot/check ID where useful. The implementer records the issue, fixes it within existing requirements, performs proportionate checks and saves a handback. The reviewer checks the accumulated delta at the next checkpoint.

**Bring these to the architect first:** lost data, permissions/lifecycle, cancellation, inconsistent state, duplicate actions/events, timing or persistence, unclear behavior, new product decisions, or a small repair that failed once. The implementer must escalate if inspection reveals such complexity. Earlier code approval does not cover unreviewed fixes.

## Core agreement

- One active writer, with the human controlling handoffs.
- Short stable instructions; one current assignment; component knowledge loaded on demand.
- Strong-model ownership of critical reasoning; reassess after one unsuccessful economical-model repair submission.
- Diff-first review with enough surrounding context for correctness.
- Honest evidence: code approval, independent review, self-verification and owner acceptance are distinct.
- Stop when the agreed work is complete. A waiting state does not authorize invented tasks.

Read the [two session flowcharts](PLAYBOOK.md#5-chart-fresh-architectreviewer-session) to see how files connect. This repository describes a workflow; it is not a tested claim of a particular percentage saving.
