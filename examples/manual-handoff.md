# Worked example: add an Unread filter to a reading list

This example follows one feature from assignment to owner acceptance. It shows what each agent reads, what it writes, and how the owner sends a small testing issue directly to the implementer.

**All files, commands, test counts and results below are fictional examples, not evidence from a real app.** `BASE`, `A` and `B` stand for exact Git commit hashes. Use actual hashes and evidence paths in a real task.

## Who does what?

- **Maya, the owner**, chooses the behavior, starts model sessions and tests the experience.
- **The senior model** scopes the feature and reviews the result. It also implements difficult logic when needed.
- **The cheaper implementer** builds this feature because the app already has a tested `selectUnreadBooks` helper. No storage or synchronization changes are needed.

The feature adds All/Unread controls, a count and two different empty states. Those interacting behaviors justify a written assignment and review. A standalone typo would use the [lighter process](../PLAYBOOK.md#choose-the-smallest-useful-process).

## 1. The senior writes the assignment

Maya asks for an Unread filter. The senior inspects the existing screen, selector and product requirement, then creates `coordination/tasks/UNREAD-01/TASK.md`:

```markdown
# UNREAD-01 — filter a collection to unread books

Implementer: cheaper model; reuse the tested selectUnreadBooks helper.
Base commit: BASE; clean working tree.

## Scope and acceptance
- Add All/Unread controls. Start with All selected.
- Unread shows only unread books and their count.
- Empty collection: show "No books yet" and the existing Add book action.
- Collection with all books read: show "You're all caught up" and
  View all books, which switches the filter to All.
- Reset to All when the user changes collections.

## Keep these constraints
- Do not change saved read status or book order.
- Use the existing book-opening callback.
- Keep controls readable and usable at supported text sizes.

## Read for this task
- docs/components/collection-screen.md
- docs/product.md, section "Collection filters"
- src/collections/selectUnreadBooks.ts and its tests

## Likely edits
- src/collections/CollectionScreen.tsx
- src/collections/CollectionToolbar.tsx
- src/collections/CollectionScreen.test.tsx

## Checks
Run the screen tests and typecheck. Cover mixed books, an empty collection,
all books read, returning to All, and changing collections.
Owner must test the experience, including enlarged text.

## Boundary
Storage, synchronization, search and dependencies are out of scope.
Report before changing data behavior. Stop after checks and handback.
```

The senior updates `coordination/CURRENT.md`:

```markdown
Active task: tasks/UNREAD-01/TASK.md
State: ready
Next actor: implementer — build the recorded assignment from BASE.
```

Maya opens the cheaper model in the repository:

> Read AGENTS.md and implement the current assignment. Save the handback when finished.

## 2. The implementer builds and hands back submission A

The implementer reads `AGENTS.md`, the local workflow, `CURRENT.md` and the linked task. It follows the task's screen/selector pointers. It has no reason to read old task folders or the synchronization engine.

Before editing, it updates `CURRENT.md`:

```markdown
Active task: tasks/UNREAD-01/TASK.md
State: implementing
Next actor: implementer — finish the assigned feature and checks.
```

It implements the feature and commits the code as `A`. A **submission** is a particular version of the code offered for review. The handback names that version so the reviewer knows exactly what to inspect.

It writes `coordination/tasks/UNREAD-01/HANDBACK.md`:

```markdown
# UNREAD-01 — submission A

Base: BASE
Code commit: A
Status: ready for review

## Changes
Added All/Unread controls, filtered count and both empty states.
Reused the selector and existing book-opening callback.
Added screen tests for the assigned behavior.

## Checks actually run
- npm test -- CollectionScreen.test.tsx: 12 passed, 0 failed.
  Evidence: evidence/A-screen-tests.txt (relative to this task folder).
- npm run typecheck: passed.
  Evidence: evidence/A-typecheck.txt (relative to this task folder).

## Not verified
Actual device layout and enlarged-text usability need owner testing.
Storage, synchronization and dependencies were not changed.
```

It updates `CURRENT.md` and stops:

```markdown
Active task: tasks/UNREAD-01/TASK.md
State: ready_for_review
Submission: A; see tasks/UNREAD-01/HANDBACK.md
Next actor: reviewer — review BASE..A against TASK.md.
```

Maya starts the reviewer session. The implementer does not launch it automatically.

## 3. The reviewer checks A; Maya tests the experience

The reviewer reads the task, handback and `BASE..A` diff. It checks the selector and book-opening callback because the feature depends on them. It does not re-audit unrelated storage code.

It writes `REVIEW.md` in the task folder:

```markdown
# UNREAD-01 — review of A

Comparison: BASE..A
Code verdict: PASS for A; no blocking findings.

Reviewed the filter, empty states, collection-change reset, callback usage
and test assertions. Inspected the implementer's recorded check output.
No tests were rerun by the reviewer; these are implementer-run results.

Owner acceptance: pending FILTER-01 through FILTER-03 in OWNER-CHECKS.md.
```

It also prepares `OWNER-CHECKS.md`:

| ID | Setup and action | Expected result | Result |
|---|---|---|---|
| FILTER-01 | Open a mixed collection; switch Unread/All and open a book | Correct books/count; correct book opens | Pending |
| FILTER-02 | Try an empty collection, then one with all books read; use each empty-state action | Correct message; Add opens the existing flow; View all books returns to All | Pending |
| FILTER-03 | Repeat with supported enlarged text | Labels remain readable and controls usable | Pending |

`CURRENT.md` now says:

```markdown
Active task: tasks/UNREAD-01/TASK.md
State: awaiting_owner
Code verdict: PASS for A; see tasks/UNREAD-01/REVIEW.md
Next actor: Maya — test A using OWNER-CHECKS.md.
```

Maya reports FILTER-01 and FILTER-02 pass on A. FILTER-03 fails: “View all books” clips at enlarged text. Code review passed, but owner acceptance is still incomplete.

## 4. Maya sends the small correction directly to the implementer

She does not need another architect session:

> On build A, FILTER-03 fails. Open a collection where every book is read, select Unread, and enlarge text to the supported maximum. “View all books” clips. Make the label readable while keeping the existing behavior. Follow the direct-correction rules in AGENTS.md.

The implementer records the report in `OWNER-CHECKS.md` and inspects the cause. A fixed button height causes the clipping, so this is a local layout repair within the existing requirement.

It updates `CURRENT.md`:

```markdown
Active task: tasks/UNREAD-01/TASK.md
State: implementing
Next actor: implementer — fix FILTER-03 within existing layout requirements.
Code status: A passed review; the new edits have not been reviewed.
```

It preserves A's handback in Git **before replacing it**, fixes the layout and commits code B. The latest `HANDBACK.md` becomes:

```markdown
# UNREAD-01 — submission B

Base: A
Code commit: B
Status: ready for review

## Change
Let the empty-state button grow when its label wraps; fixes FILTER-03.
No filter, navigation or storage logic changed.

## Checks actually run
- npm test -- CollectionScreen.test.tsx: 12 passed, 0 failed.
  Evidence: evidence/B-screen-tests.txt.
- npm run typecheck: passed. Evidence: evidence/B-typecheck.txt.

## Owner retest needed
FILTER-03: enlarged-text layout still needs device confirmation.
FILTER-02: check the corrected button's action still works.
```

`CURRENT.md` becomes:

```markdown
Active task: tasks/UNREAD-01/TASK.md
State: ready_for_review
Submission: B; see tasks/UNREAD-01/HANDBACK.md
Next actor: reviewer — review A..B, focusing on FILTER-03 and its action.
Code status: PASS applies to A only; B is pending review.
```

Maya may retest B while waiting for review. The reviewer inspects `A..B`, confirms the fix and records PASS for B. It preserves A's review before replacing the current verdict. If Maya has not reported back yet, `CURRENT.md` says:

```markdown
Active task: tasks/UNREAD-01/TASK.md
State: awaiting_owner
Code verdict: PASS for B; see tasks/UNREAD-01/REVIEW.md
Next actor: Maya — report FILTER-02 and FILTER-03 on B.
```

Maya reports both checks pass on B. The agent records her results with their build attribution. FILTER-01 remains a pass **on A**, with a note that B did not change that path; nobody claims Maya reran it on B.

### What if the cause had been complex?

Suppose Maya instead reported that books changed read status after restarting the app. The implementer would report the persistence concern before editing that logic. The senior would diagnose and implement the critical repair.

Known cancellation, concurrency, persistence-ordering and tricky state-machine work goes to the senior **upfront**. It does not need a failed cheaper-model attempt first. If a cheaper-model repair has already been submitted and the same defect remains, reassess who should fix it before assigning another attempt.

## 5. Close the task and leave a useful starting point

The reviewer records that B passed code review and the required owner results are complete, with the original build attribution retained. `CURRENT.md` becomes:

```markdown
Active task: none
State: closed
Last task: tasks/UNREAD-01/TASK.md
Closure: B passed review; required owner checks accepted.
Next actor: Maya — choose the next task. No implementation is queued.
```

The task folder stays in the repository as history. The lasting rule—distinguish “no books” from “no unread books,” with the correct action for each—belongs in the screen contract, linked to the relevant code and tests. The clipping-repair narrative stays in the task history.

The next session reads the entry instructions and current pointer, then the context needed for its new assignment. It does not reread this closed task by default.

**For a standalone typo:** send the direct request, check the result, and record it in an existing task or commit description. Use the full sequence above when uncertainty, interacting behavior or the project's review policy warrants it.
