# EGM Dining

EGM Dining adds a restaurant decision workflow to the Elephant-Goldfish Model.
The Elephant holds the diners' stated constraints, searches Google Maps through
Maps Experience agent tools, and proposes one place plus a backup. Fresh
Goldfish reviewers challenge hours, source-backed risks, hard vetoes, and
logistics.

## Connect Google Maps

EGM Dining uses Google's Maps Experience agent tools MCP server. This is the
Google Maps integration designed to ground LLM applications and return
attributed place summaries; do not send raw Places API responses into an LLM.

1. Create or choose a Google Cloud project, enable billing, and enable the
   **Maps Experience agent tools API**.
2. Create an API key restricted to the Maps Experience agent tools API, or set
   up OAuth with the `maps-platform.mapstools` scope.
3. In the MCP settings for your coding agent, add the remote HTTP endpoint
   `https://mapstools.googleapis.com/mcp` with the authentication header
   `X-Goog-Api-Key` (or OAuth) and name it
   `maps-experience-agent-tools-mcp`.
4. Confirm the host lists the `search_places` tool before running
   `egm-dining-scout`.

Never commit or paste an API key in chat, project files, a shell command saved
to history, or a public client. Restrict the key and review the project's Maps
usage and billing reports. Google's MCP setup guide documents the endpoint,
authentication methods, and supported tools.

## Search and billing

Call `search_places` with a specific text query such as "quiet Thai date-night
restaurants in Madison, Wisconsin." Provide `location_bias` only when the
diners supplied coordinates. Essentials requests return up to five places; the
scout defaults to five or fewer and does not request extended details.

Extended review insights and more than five results use the Pro SKU. Pro
features are in restricted availability and require the project to be allowlisted.
Use them only when a user requests deeper review context and the operator
accepts the billing. Google bills each search or route tool request. Check the
current [Maps Experience agent tools guide](https://developers.google.com/maps/ai/maps-experience-agent-tools),
[MCP reference](https://developers.google.com/maps/ai/maps-experience-agent-tools/reference/mcp),
and [pricing and quotas](https://developers.google.com/maps/ai/usage-and-billing)
before enabling optional Pro calls.

## Sources, model use, and storage

Keep every generated Maps summary with the source citations it returned. Put
Google Maps source links immediately after the claims they support. For place
summaries, use the returned `googleMapsLinks.placeUrl`; for review insights,
use `googleMapsLinks.reviewsUrl`. Do not separate place facts from their
sources, copy review text into a file, or claim a small summary is a complete
review audit.

Use only a model whose terms and settings do not cache or store Maps content or
use it for model training or improvement. The current Google terms restrict
storage and creating content from Places API data, with an exception for
grounded output produced through Maps Experience agent tools when source links
are included and the other terms are followed. For that reason, this workflow
keeps its Maps-based proposal and Goldfish audit in the live user conversation;
it does not write `dining_spec.md`, review excerpts, or raw Maps data into the
project. User-entered preferences may be saved separately only when the user
asks.

The tool's `openNow` field describes search time, not future arrival. Posted
business hours do not prove kitchen hours, availability, or a wait. Missing
parking, menu prices, reservations, and accessibility data must be reported as
unknown. The comedy belongs in the tie-breaker, not in invented restaurant
facts.

See Google's [Places API policies and attribution requirements](https://developers.google.com/maps/documentation/places/web-service/policies)
and [Maps Experience agent tools policies](https://developers.google.com/maps/ai/maps-experience-agent-tools#policies_and_terms_of_service).

## Workflow

Run `egm-dining-scout` to gather constraints and query `search_places`. Run
`egm-dining-audit` to dispatch `egm-hungry-goldfish` and
`egm-logistics-critic` in fresh contexts. Give reviewers only the proposal and
grounded summary with its Maps sources. If isolated subagents are unavailable,
mark those audits as not run. The Elephant adjudicates evidence-backed
findings and gives the couple one recommendation plus one backup.
