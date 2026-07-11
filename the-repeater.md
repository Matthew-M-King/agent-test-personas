# The Repeater

> "It spun for ages, so I hit it again. And again."

**Kind:** behaviour persona — the flaky-network retrier.

## Behaviour

Works on bad signal. Requests stall, time out, and "fail" that actually succeeded
on the server — so they retry, two or three times, sometimes from a tab that
reloaded itself. The **server-side twin of the Fumbler**: where the Fumbler
double-*clicks* (a frontend guard can catch that), the Repeater's duplicates are
genuine, independent requests that all reach the API. If idempotency lives only in
the browser, the Repeater breaks it.

## Stresses

Server-side idempotency, independent of any UI submit-once guard; retry/replay
safety.

## Look for in code

- Mutating endpoints with **no idempotency key** and no natural unique constraint —
  a replayed request creates a second effect.
- Idempotency enforced **only in the client** (disabled button, dedupe in JS) with
  the server unprotected.
- Non-idempotent **external calls** (charge, email, webhook) with no
  dedupe/replay protection.
- Retries that **stack** — connection leaks, queued duplicates, compounding work.
- "At-least-once" delivery (webhooks, queues, callbacks) consumed as if
  **exactly-once**.

## Exploratory paths

- Replay an identical create/submit/charge request 2–3× at the API (bypassing the
  UI); confirm a single logical effect.
- Fire a request and its retry **concurrently**, then **sequentially**; confirm one
  effect either way.
- Simulate a timeout-then-retry where the first call actually committed; confirm no
  duplicate.
- Deliver the same webhook/callback twice; confirm idempotent handling.

## Techniques

Idempotency Thinking, Reliability / Resilience Testing, API Contract Thinking,
Error Guessing. See [`../resources/test-techniques.md`](../resources/test-techniques.md).
