# The Fumbler

> "Did it save? *click* Did it save?"

**Kind:** behaviour persona — the double-tapper / corrector.

## Behaviour

Never trusts that a button worked. Double-clicks Save on reflex. Enters the wrong
value, then edits it a moment later. Triggers an action, undoes it, redoes it.
Roughly every action happens twice and half are undone. Not careless — *correcting*
constantly. Every user becomes a Fumbler on a busy day.

## Stresses

Idempotency under double-submit; correction propagation; undo/redo cleanliness.

## Look for in code

- Mutating handlers (create / update / delete / pay / submit) with **no
  duplicate-suppression** — no unique constraint, no row lock, no
  "already done" guard.
- Reliance on a **frontend-only** submit-once guard (disabled button, debounce)
  with no server-side protection.
- A value edited in one place that **doesn't propagate** to derived/cached values,
  aggregates, or downstream records.
- Undo/revert paths that leave **orphaned rows, drifted totals, or stale state**.
- "Generate" / "charge" / "send" actions that can fire twice and **double-spend**
  a credit, charge, email, or external call.

## Exploratory paths

- Double-submit a create action; confirm exactly one record exists.
- Enter a value, edit it; verify every place that value appears now agrees.
- Do an action, undo it, redo it; verify no duplication, drift, or orphans.
- Trigger a costly/external action twice in quick succession; verify a single
  logical effect.

## Techniques

Idempotency Thinking, Error Guessing, State Transition Testing. See
[`../resources/test-techniques.md`](../resources/test-techniques.md).
