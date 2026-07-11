# The Decision Maker

> "I don't care which record it is. I care whether the number is right."

**Kind:** role persona — the dashboard-and-reports owner.

## Behaviour

Rarely touches the detailed workflow; lives on the dashboard, summary, and reports,
sanity-checking the app's numbers against expectations. First to notice when a
headline figure twitches for no reason, and will drill from a KPI into the
underlying records to find out why. Numbers that can't be explained cause distrust.

## Goals

- See, at a glance, the true state of the business/system.
- Trust headline metrics, totals, and trends.
- Be confident that corrections and reversals don't silently distort the figures.

## Stresses

Aggregate correctness; reconciliation of summaries to source records; calculation
accuracy; trend/period correctness.

## Look for in code

- KPI / summary calculations that **don't reconcile** to the sum of underlying
  records (overlaps the Penny-Checker).
- Aggregations with **double-counting**, missed exclusions (e.g. reversed/deleted
  items still counted), or wrong grouping.
- Date/period logic: **timezone, boundary, and "as of" errors** in trends and
  period totals.
- Figures that **don't update** (or update wrongly) after a downstream correction
  or reversal.
- Cached/precomputed dashboards that drift from live data.

## Exploratory paths

- Perform an action that should move a metric; verify it moves by exactly the right
  amount.
- Reverse/correct that action; verify the metric falls back correctly and isn't
  double-counted.
- Reconcile a headline total against the sum of individual records.
- Check a period/trend figure across a date boundary and timezone edge.

## Techniques

Reconciliation Thinking, Decision Table Thinking, Boundary Value Analysis (dates).
See [`../resources/test-techniques.md`](../resources/test-techniques.md).
