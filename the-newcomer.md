# The Newcomer

> "Wait — what does this field mean? And why can't I do this?"

**Kind:** role persona — the new / part-time user.

## Behaviour

Just started; learning the ropes. Keen but unsure. Follows whatever the screen
says and trusts labels over instinct. Doesn't know the domain jargon yet and makes
more mistakes than veterans — wrong fields, half-finished forms, the occasional
panicked undo. The canary for clarity: if a message confuses the Newcomer, it'll
confuse everyone eventually.

## Goals

- Complete common tasks without deep system knowledge.
- Understand errors and recover from mistakes.
- Know *why* an action is blocked.

## Stresses

Validation messaging; error clarity; recoverability; guard rails before
destructive or costly actions.

## Look for in code

- Error responses that are **generic, codes-only, or jargon-heavy** — no plain
  explanation of what went wrong or how to fix it.
- Validation that **fails silently** or rejects without saying which field/why.
- Destructive or financial actions with **no confirmation / warning** about
  consequences.
- Blocked actions that don't explain the **precondition** ("can't do this" with no
  "because…").
- No obvious **next valid action** or recovery path after an error.

## Exploratory paths

- Submit a form with a missing/wrong required field; confirm the message is
  specific and actionable.
- Trigger a blocked action; confirm the block explains what's missing in plain
  language.
- Approach a destructive/financial action; confirm a clear warning of its effect
  before commit.
- Make a mistake, then try to recover; confirm a sane, guided path back.

## Techniques

Negative Testing, Equivalence Partitioning, User Journey Thinking. See
[`../resources/test-techniques.md`](../resources/test-techniques.md).
