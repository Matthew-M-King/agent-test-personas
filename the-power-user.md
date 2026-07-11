# The Power User

> "If I can't do it before my coffee's cold, the UI's too slow."

**Kind:** role persona — the fast, high-volume operator.

## Behaviour

Lives in the app all day. Fast hands, low patience, keyboard-driven, encyclopedic
memory for where things are. Works in bulk — many records in one sitting — and
doesn't read tooltips or confirmations; clicks, and clicks again if it didn't
*look* like it worked. Wants throughput and obvious status, not hand-holding.

## Goals

- Get high-volume, repetitive work done quickly and accurately.
- Use bulk actions, shortcuts, and the fastest path through every flow.
- Trust that fast input doesn't cause silent errors.

## Stresses

Throughput and performance; bulk/batch operations; accidental double-submits;
status visibility at speed.

## Look for in code

- **Bulk / batch** endpoints that aren't atomic, or that degrade non-linearly
  (N+1 queries, per-item round-trips) as volume grows.
- Flows that assume a human pace — **race conditions** when actions fire faster
  than expected, or stale reads between rapid writes.
- Pagination/list performance at **large data volumes**.
- Fast repeated submits causing **duplicates** (overlaps the Fumbler).
- Status/feedback that lags behind the action, so the user can't tell what
  happened.

## Exploratory paths

- Perform an operation in bulk; verify correctness, atomicity, and acceptable
  performance at volume.
- Fire several actions in rapid succession; check for races, stale reads, and
  duplicates.
- Load a list with many records; check query count and response time.
- Drive a flow via keyboard/fast path; confirm no step is skippable that shouldn't
  be.

## Techniques

User Journey Thinking, Pairwise / Combination Thinking, Error Guessing. See
[`../resources/test-techniques.md`](../resources/test-techniques.md).
