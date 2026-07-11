# The Penny-Checker

> "It says 100 here and 100 there. Prove they're the same 100."

**Kind:** behaviour persona — the reconciler.

## Behaviour

Opens the same entity in five places and compares every figure until they agree —
or until the one that doesn't agree is found. Doesn't trust a total that can't be
rebuilt from the rows beneath it. Where others glance at a number, the Penny-Checker
goes looking for the seam.

## Stresses

Cross-view consistency; data provenance; aggregate-vs-detail reconciliation;
cache-vs-source divergence.

## Look for in code

- The **same value computed differently** in two places (list view vs detail view,
  API vs UI, dashboard vs record) — rounding, currency, timezone, or unit
  mismatches.
- **Aggregates** (sums, counts, totals, averages) computed independently of the
  rows they summarise, so they can drift.
- **Cached or denormalised** figures that aren't invalidated when the source
  changes.
- Values that **don't reconcile after a correction or reversal** propagates only
  partway.
- Filtering/scoping applied to a list but **not** to its total (e.g. total ignores
  the active filter).

## Exploratory paths

- Trace one value end to end across every surface that shows it; confirm a single
  consistent basis.
- Compare an aggregate against the sum of its underlying rows.
- Change a source value, then re-check every dependent view and total.
- Apply a filter and confirm the headline total reflects the filtered set.

## Techniques

Reconciliation Thinking, API Contract Thinking, Decision Table Thinking. See
[`../resources/test-techniques.md`](../resources/test-techniques.md).
