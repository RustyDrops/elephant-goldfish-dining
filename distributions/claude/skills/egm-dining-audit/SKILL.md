---
name: egm-dining-audit
license: Apache-2.0
disable-model-invocation: true
description: >-
  Dispatches fresh, adversarial dining and logistics reviewers to test a
  restaurant proposal against Google Maps grounded evidence.
---

# EGM Dining Audit: Fresh Eyes, Empty Stomachs

## Inputs

Require the proposal and matching Google Maps grounded summary with its source
links, supplied inline by the Elephant (or an explicit statement that evidence
is unavailable). Do not ask for raw Maps responses, earlier conversation
context, or a preference file.

## Dispatch

Spawn both reviewers in fresh, isolated contexts when the host supports it.
Use a named reviewer when registered; otherwise spawn a general-purpose fresh
subagent and instruct it to read the canonical persona file first:

- `agents/egm-hungry-goldfish.md`
- `agents/egm-logistics-critic.md`

Each reviewer receives only the proposal and relevant grounded summary with its
source links. Do not include raw API responses, conversation history, the
Elephant's private deliberation, or stored preferences. If a reviewer cannot
start, retry once. Then record it as **not run**; same-context review does not
count as an isolated Goldfish audit.

## Adjudication

Do not save reviewer output or Google Maps grounded content to project files.
Block the recommendation if the evidence confirms a hard failure such as
permanent closure, incompatible hours, or a stated hard dietary veto. Treat
absent parking, menu prices, reservation availability, or review coverage as
unknown and surface the uncertainty instead of filling it in.

Return a verdict of `APPROVED`, `BLOCKED`, or `CONDITIONAL PASS`, with fatal
flaws, relevant linked Maps sources, and the condition diners must resolve
before leaving. Do not reproduce review text. A restaurant is not guilty just
because one reviewer had a bad Tuesday.
