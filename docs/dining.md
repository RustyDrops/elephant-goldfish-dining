# EGM Dining

EGM Dining helps undecided diners choose one restaurant and a backup, then
asks fresh Goldfish reviewers to challenge the plan. It is designed to work
without a Google Maps MCP connection, API key, paid search service, or separate
account setup.

## Find dinner with what is already available

The dining scout uses the host's built-in web search or browser when available.
It favors restaurants' own sites for hours, menus, and reservation details,
then uses reputable public listings to fill gaps or cross-check claims. Each
important claim should have a nearby source link so diners can verify it.

If the host does not have web search or browser access, share two or three
restaurant names or links in the conversation. The scout can compare the
information available in those sources and mark anything missing as unknown.
No setup is needed from the diners.

## Evidence rules

- Do not invent hours, kitchen closing times, waits, prices, parking, access,
  reservations, or travel times.
- Treat a search-time "open now" indicator as a snapshot, not proof of future
  hours. Posted business hours do not prove kitchen hours, availability, or a
  current wait.
- Prefer first-party information for menus and hours. If sources disagree,
  show the conflict and link both sources.
- Treat review snippets as partial evidence. Do not quote review text at length
  or call a small sample a complete review audit.
- Keep location and dining history in the current conversation. Do not write
  restaurant names, addresses, ratings, or review text to project files.

The comedy belongs in the tie-breaker, not in invented restaurant facts.
Present one primary recommendation, one backup, the reason the primary wins,
and the biggest relevant uncertainty.

## Workflow

Run `egm-dining-scout` to gather constraints, search when supported, and prepare
the proposal. Run `egm-dining-audit` to dispatch `egm-hungry-goldfish` and
`egm-logistics-critic` in fresh contexts. Give reviewers only the proposal and
its linked evidence. If isolated subagents are unavailable, mark those audits
as not run.
