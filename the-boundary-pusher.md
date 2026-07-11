# The Boundary Pusher

> "What if I put a minus sign in front of it?"

**Kind:** behaviour persona — the fat-finger / edge-seeker.

## Behaviour

Tests the edges — sometimes by accident, sometimes out of genuine curiosity. Types
0 where a value should go, then a huge number; sets a quantity to 0, then 999;
submits empty, oversized, or wrong-type fields; repeats a terminal action (does the
already-done thing again). The human fuzzer the app didn't ask for.

## Stresses

Input validation; guard rails; repeat-action protection; error-path safety.

## Look for in code

- Numeric inputs with **no bounds** — negatives, zero, huge values, decimals where
  integers are expected, overflow.
- String inputs with **no length / format / encoding** checks — empty, oversized,
  unicode, control characters, injection payloads.
- Validation done **only client-side**, with the server trusting the payload.
- Actions on already-terminal entities (cancel an already-cancelled order, delete
  twice) with **no state guard**.
- Rejected requests that still cause **side effects** — partial writes, leaked
  state, expensive work before the validation check.

## Exploratory paths

- Submit zero, negative, and absurdly large numbers; confirm clear, specific
  rejection.
- Submit empty, oversized, and wrong-type fields; confirm structured errors and no
  partial writes.
- Repeat a terminal action (do the already-done thing again); confirm a safe,
  explained outcome.
- Bypass the UI and post a malformed payload directly; confirm the server validates
  independently.

## Techniques

Boundary Value Analysis, Equivalence Partitioning, Negative Testing, Fuzz / Abuse
Thinking, Security-Focused Testing. See
[`../resources/test-techniques.md`](../resources/test-techniques.md).
