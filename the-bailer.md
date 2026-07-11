# The Bailer

> "Actually, never mind." *closes tab*

**Kind:** behaviour persona — the abandoner.

## Behaviour

Means well but gets pulled away mid-task, every time. Starts a multi-step flow and
leaves it half-done. Opens a checkout, then closes the tab when the price gives
pause. Refreshes the page mid-save "just to check." Not malicious or clumsy — just
*interrupted* — which is exactly what exposes whether the system handles partial,
abandoned, and resumable state, or quietly corrupts it.

## Stresses

Partial / abandoned state handling; cleanup; resumability.

## Look for in code

- Multi-step flows (wizards, checkouts, builders) where **intermediate state is
  persisted** but has no defined "incomplete" status or cleanup.
- Operations that write **part of a set** then assume the rest will follow (loops
  that can be interrupted mid-way, non-atomic multi-record writes).
- External sessions (payment, upload, OAuth) **started but never completed** — no
  expiry, no cleanup, no resume.
- A page refresh or back-navigation mid-save creating **duplicate or partial**
  records.
- No way to **resume** a half-finished task; or resuming silently restarts/loses
  progress.

## Exploratory paths

- Start a multi-step flow, complete some steps, navigate away, return; verify state
  is consistent and resumable.
- Refresh mid-save; verify no duplicate or partial record is created.
- Begin a checkout / external session, abandon it; verify no value is granted and
  no dangling state leaks.
- Interrupt a batch operation partway; verify all-or-nothing, or a clearly defined
  partial state.

## Techniques

State Transition Testing, Reliability / Resilience Testing, User Journey Thinking.
See [`../resources/test-techniques.md`](../resources/test-techniques.md).
