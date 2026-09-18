# Worked example: a fictional reading-list app

All task IDs and revisions below are illustrative placeholders. This is not project evidence.

## 1. Assignment

The owner wants an existing collection editor to show a useful empty state. The architect records `COLLECTION-EMPTY-01/TASK.md`: scope is text/layout and an existing Add action; storage and navigation behavior are unchanged. Relevant pointers are the collection UI contract, the design specification and existing screen tests. `CURRENT.md` points to this task, says ready, and names the economical implementer as next actor.

The owner opens that implementer in the same repository:

> Read AGENTS.md and implement the current assignment. Save the handback when finished.

The implementer follows the task links, changes the screen, runs proportionate checks and records submission A in HANDBACK. It updates CURRENT to ready_for_review and stops. It does not launch the reviewer.

## 2. Review and owner testing

The owner opens the reviewer. It reads the entry instructions, CURRENT, TASK, HANDBACK and the scoped diff. It checks the affected Add callback rather than re-auditing the storage layer. It records code PASS for A and creates stable owner check `EMPTY-01`: open an empty collection, confirm copy is visible and use Add. CURRENT becomes awaiting_owner.

The owner observes that the subtitle clips at a supported display size and sends that clear visual defect directly to the implementer. No architect round-trip is required. The implementer records the report in the active task and inspects the cause.

## 3. Direct correction

The defect is a fixed height that contradicts the existing layout requirement. The implementer corrects it, performs the relevant check and records submission B plus the affected `EMPTY-01` retest. It preserves submission A's record in Git before replacement. CURRENT says ready_for_review; PASS for A is not transferred to B.

The owner can retest while the reviewer later reviews A-to-B as one bounded delta. The owner reports EMPTY-01 pass on B. The reviewer verifies the correction, records PASS for B and closes the task once required acceptance evidence is complete.

## 4. If the apparently small issue was complex

Suppose Add sometimes creates duplicate collections after screen recreation. The implementer stops the simple visual-correction path and reports a state/persistence concern. The architect diagnoses it and assigns the critical logic to the stronger model before another economical-model implementation cycle. A previously submitted economical repair that failed once also triggers reassessment.

The strong implementer runs appropriate non-device checks. Its own verification is labeled accordingly; a consequential change can receive a separate focused review. The human still owns experience acceptance.

## 5. Next task

The completed task folder remains as history. Any newly established lasting UI constraint is promoted into the collection UI contract. CURRENT moves to the next authorized task. The next session does not read the previous task's full conversation or all closed task folders.
