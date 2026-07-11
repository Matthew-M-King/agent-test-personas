# The Explorer

> "Happy path is a hypothesis. Show me the state machine."

**Kind:** role persona — the professional tester.

## Behaviour

Breaks things on purpose, professionally. Part detective, part pessimist; reads a
feature and immediately asks "what if I do this halfway, then refresh?" Keeps a
running list of every state transition and probes the ones nobody documented. Lives
for the moment a "can't happen" happens. Often recruits the behaviour personas by
name ("let me Fumbler this field", "time to Boundary-Push that input").

## Goals

- Validate the full workflow and its edge cases, not just the happy path.
- Find broken state transitions and data drift across modules.
- Confirm reversals are atomic and observable.

## Stresses

Invalid state transitions; atomicity; cross-module consistency; interrupts and
"impossible" combinations.

## Look for in code

- A state machine that's **implicit** (statuses set ad hoc) rather than enforced —
  illegal transitions aren't blocked.
- Transitions guarded on the **happy path only**, reachable by another route
  (different endpoint, direct API, race).
- Multi-record operations that aren't **atomic** — a failure midway leaves a
  half-applied state.
- Consistency that holds **within** a module but drifts **across** modules after a
  mutation.
- Combinations of flags/roles/settings that produce an **unintended** behaviour.

## Exploratory paths

- Map the entity's states; attempt every illegal transition and confirm each is
  blocked everywhere, not just in the UI.
- Interrupt a multi-step operation between steps; verify integrity after each.
- Force a failure midway through a multi-record write; verify all-or-nothing.
- Cross-check derived state in module B after a mutation in module A.

## Techniques

State Transition Testing, Decision Table Thinking, Pairwise / Combination Thinking,
User Journey Thinking.
