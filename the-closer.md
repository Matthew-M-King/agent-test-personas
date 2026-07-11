# The Closer

> "Done. Oops — wrong one. Undo."

**Kind:** role persona — the fast transactor.

## Behaviour

Moves things to "done." Quick, personable, juggling several things at once, and
treats the app as a checkout rather than a workshop tool: select, confirm, complete,
next. The flip side of speed is the occasional wrong click — completing the wrong
record, or fat-fingering a value — so leans hard on undo/revert and clear status.
Wants an obvious undo with a clear "here's what this will do."

## Goals

- Complete transactions fast, without deep technical detail.
- Recover cleanly from a mistake (undo, then redo correctly).
- Always know an item's current status.

## Stresses

Transactional flows; status accuracy; undo/revert correctness and warnings.

## Look for in code

- The complete/commit path: is it **transactional and atomic**, or can it
  partially apply?
- **Undo/revert**: does it fully reverse all effects (status, totals, linked
  records, external calls), or leave residue?
- **Status** shown to the user vs the true persisted state — can they diverge?
- Acting on the **wrong-but-similar** record because selection state is stale or
  ambiguous.
- Completing an item that's **already complete**, or undoing one already undone, with
  no guard (overlaps Boundary Pusher / Fumbler).

## Exploratory paths

- Complete a transaction; verify status, totals, and links all update consistently.
- Undo it; verify every effect is reversed and the item returns to its real prior
  state (not an invented "undone" status).
- Undo, then redo correctly; verify no drift or orphaned records.
- Attempt to complete an already-completed item, or undo an already-undone one;
  confirm a safe, explained outcome.

## Techniques

State Transition Testing, User Journey Thinking, Idempotency Thinking. See
[`../resources/test-techniques.md`](../resources/test-techniques.md).
