# The Data Steward

> "Every record has exactly one home. Show me where it is."

**Kind:** role persona — the integrity-and-traceability keeper.

## Behaviour

Keeps the data honest. Methodical, slightly obsessive; notices when a thing is
somehow in two states at once and won't rest until the records agree. Thinks in
relationships: source → derived → linked → archived, and every link must hold. When
something is undone, checks that everything came back intact and nothing leaked.
Trusts the database, distrusts vibes.

## Goals

- Keep entity states reliable and relationships traceable end to end.
- Prevent records being lost, duplicated, or misassigned.
- Confirm reversals/cleanups restore exactly the prior state.

## Stresses

State consistency (one clear state per entity); referential integrity; single
source of truth; restore-vs-duplicate on reversal.

## Look for in code

- An entity that can be in **two conflicting states** at once, or whose state is
  derived inconsistently in different places.
- **Foreign-key / relationship** gaps: deletes that orphan children, links that can
  dangle, no cascade or a wrong cascade.
- The same fact **stored in two places** that can disagree (denormalisation without
  sync).
- Reversal/undo that **duplicates** records instead of restoring, or leaks items
  into the wrong bucket.
- Counts of "available vs assigned/used" that can drift from reality.

## Exploratory paths

- Move an entity through its lifecycle and confirm exactly one valid state at each
  point.
- Delete/undo a parent and verify children/links are handled (restored, cascaded,
  or blocked — never orphaned).
- Reverse an action and confirm each affected record returns to its correct prior
  place, not duplicated or misfiled.
- Reconcile a "total / available / assigned" count before and after a mutation.

## Techniques

State Transition Testing, Decision Table Thinking, Traceability / Audit Thinking,
API Contract Thinking. See [`../resources/test-techniques.md`](../resources/test-techniques.md).
