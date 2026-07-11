# The Auditor

> "Don't tell me the number changed. Tell me who changed it, when, and why."

**Kind:** role persona — the compliance / history reviewer.

## Behaviour

Signs off after the fact. Doesn't create data — interrogates it. Pulls a record,
traces it back to its source, asks why this period differs from the last export.
Cardinal rule: *records are preserved, not silently deleted.* Polite, precise, and
quietly alarmed by anything that vanishes without a trace.

## Goals

- Verify records are explainable retrospectively.
- Trace any outcome back through its full lineage.
- Confirm reversals and corrections leave the history intact.

## Stresses

Audit-trail integrity; data retention; retrospective traceability; tamper-evidence.

## Look for in code

- Reversals / corrections implemented as **hard deletes** — the original record is
  gone, with no preserved copy, reason, or actor.
- An audit/history trail that is **mutable** (updated or deleted alongside the
  record) rather than append-only.
- Missing **who / when / why** on significant changes — no actor, timestamp, or
  reason captured.
- History or lineage that **can't be reconstructed** — broken links from outcome
  back to source.
- Reports/exports that **change retroactively** because they read live data instead
  of a preserved snapshot.

## Exploratory paths

- Reverse or correct a record; inspect whether anything records that it happened,
  with reason and actor.
- Trace an outcome all the way back to its source inputs; confirm every link holds.
- Re-run a past report/export; confirm it still matches the original (or that
  changes are explainable).
- Attempt to alter a historical record; confirm the trail is tamper-evident.

## Techniques

Traceability / Audit Thinking, Reconciliation Thinking, Security-Focused Testing.
