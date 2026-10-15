# User stories and acceptance criteria

Converts the [PRD](PRD.md)'s functional requirements into testable stories, grouped by the four functional areas in PRD §6. Each story cites the trust/fact states defined in the [data and trust model](../architecture/data-and-trust.md) rather than inventing new ones. Non-goals restate the PRD §5 exclusions relevant to that area so a reviewer does not have to cross-reference while testing.

## Epic 1 — Trip and document management

### US-1.1 Create and manage a trip
As a traveller, I want to create a private trip with my arrival details and destination, so that I have one place to build my journey.

- Given no existing trip, when I start "Plan an arrival journey," then I must supply an arrival location, arrival date/time, and a precise destination address or pin before I can continue.
- Given I enter "Boxberg, Heidelberg" alone as the destination, when I try to continue, then the app explains that a precise address or pin is required for the final walking step.
- Given a trip exists, when I open "My Trips," then I see its state (setup incomplete, planned, expired) without needing to open it.
- Given a trip I own, when I delete it, then its documents and derived journey data are removed per the approved retention policy, and I see confirmation of what was deleted.

### US-1.2 Upload a booking document
As a traveller, I want to upload a ticket or itinerary file, so that I don't have to retype its details.

- Given a supported file (PDF/JPG/PNG within approved size limits), when I upload it, then it is validated, scanned, and stored privately before extraction starts.
- Given an unsupported, oversized, or corrupt file, when I upload it, then I see a specific rejection reason and a manual-entry fallback, never a silent failure.
- Given I have no ticket, when I continue without uploading, then I am told I'll receive a labelled **recommended** option instead of a booked leg.

### US-1.3 Review and correct extracted facts
As a traveller, I want to confirm or correct extracted booking details, so that an OCR mistake never becomes a silent fact.
Non-goal: the system must never auto-confirm a critical field from confidence score alone (see US-3.1).

- Given extracted fields with mixed confidence, when I view the review screen, then each field shows its status (`document_extracted`, confirmed, needs review) individually — never one merged badge.
- Given a field is ambiguous or conflicting, when I reach "Confirm plan," then I cannot proceed until that field is edited or explicitly confirmed.
- Given I correct a field, when I save it, then the correction is recorded against the fact's evidence history, not silently overwritten.

**Non-goals (Epic 1):** camera/image-matching extraction, continuous background document sync, storing a public/unauthenticated file URL for any upload.

## Epic 2 — Route planning and location resolution

### US-2.1 Resolve ambiguous locations
As a traveller, I want the app to confirm an ambiguous airport, station, or address before planning, so that my route isn't built on a wrong guess.

- Given a destination string resolves to more than one candidate, when I continue, then I must pick one from labelled candidates before route planning starts.
- Given a location cannot be resolved by an approved provider, when I continue, then the step is marked "needs confirmation," not silently dropped.

### US-2.2 Preserve a booked leg over a suggested one
As a traveller with a booked train/bus ticket, I want that leg to stay authoritative, so that the app never quietly reroutes me around something I already paid for.

- Given a confirmed ticket for a leg, when the route is built, then that leg's segment uses the ticket's service/time/seat data, labelled "From your confirmed ticket."
- Given no ticket for a leg, when the route is built, then the leg is labelled "Recommended option" with provider and retrieval time, and requires my explicit selection before it becomes the working plan.
- Given both a ticket and a provider suggestion disagree on a leg the ticket covers, when I view the plan, then the ticket wins and the disagreement is never silently resolved by the system choosing the provider's value.

### US-2.3 See and understand transfer risk
As a traveller making a connection, I want to know if a transfer is tight, so that I can plan accordingly instead of being surprised at the platform.

- Given a transfer's buffer falls below the [transfer-buffer policy](../architecture/data-and-trust.md#transfer-buffer-policy) minimum for its mode, when I view the journey, then that transfer is labelled "Tight transfer" with the buffer shown.
- Given the data needed to compute a buffer (e.g., a missing arrival or departure time) is absent, when I view the journey, then the transfer is labelled "needs confirmation" — the app never calls a connection safe without the underlying data.

**Non-goals (Epic 2):** indoor/platform-level navigation beyond an official reference, global routing outside the approved corridor, automatic rebooking around a missed connection.

## Epic 3 — Guide generation and travel mode

### US-3.1 Generate a guide the LLM cannot alter
As a traveller, I want each guide step to come from verified facts, so that the AI never invents a platform, time, or route.

- Given a reviewed, versioned journey, when the guide is generated, then every step validates against the guide schema and references only known fact/segment IDs.
- Given the generator's output references an unknown fact, changes a fact value, or omits a required warning, when it is validated, then it is rejected before the traveller ever sees it.

### US-3.2 Follow one step at a time
As a traveller in transit, I want one clear instruction at a time, so that I'm not overwhelmed while carrying luggage in an unfamiliar place.

- Given travel mode is open, when I view the current step, then I see exactly one primary action, a recognition cue, a success check, the next-step preview, and a recovery path — matching the [travel-mode step contract](../product/experience.md#travel-mode-step-contract).
- Given I tap "I cannot find this place," when the recovery sheet opens, then it explains the limitation, offers a safe next step or verified external link, and lets me return to the step — it never silently substitutes a different route.

### US-3.3 Ask the trip assistant a sourced question
As a traveller, I want to ask about my trip and get an answer tied to evidence, so that I can trust what I'm told mid-journey.

- Given a question answerable from confirmed trip facts, when I ask it, then the answer names its source (document, provider, or "your confirmed ticket").
- Given a question the assistant cannot answer from authorised trip context, when I ask it, then I get an explicit "I don't have a verified answer for that," never a plausible-sounding guess.

**Non-goals (Epic 3):** voice navigation, autonomous booking/rebooking actions, treating open web search results as an operational transport fact.

## Epic 4 — Export and refresh

### US-4.1 Export a guide that matches what I reviewed
As a traveller, I want a PDF of my reviewed guide, so that I have something readable without a live connection.

- Given a confirmed journey version, when I export it, then the PDF renders that exact version with source attribution, retrieval timestamps, and freshness warnings — never a newer, unreviewed version.
- Given the PDF generation fails, when I view the export screen, then I see a clear failure message and my reviewed journey is unaffected; I can retry or export later.

### US-4.2 Use a saved guide offline
As a traveller without a connection, I want my downloaded guide to stay readable, so that losing signal doesn't strand me.

- Given a saved guide snapshot, when I open it offline, then it displays its generation time and marks volatile data (schedules, platforms, live status) as needing a recheck.
- Given I regain connectivity, when I open the guide, then I'm offered an explicit refresh action rather than a silent background update.

**Non-goals (Epic 4):** treating an offline snapshot as proof of current live data, automatic silent re-export, ticket purchasing or payment at export time.

## Traceability

Each story maps to PRD §7 acceptance criteria 1–8 and does not introduce a requirement the PRD does not already state. Where a story needed a concrete threshold not yet in the PRD (the transfer-buffer minimum), it links to the architecture doc section defining it rather than inventing a number here.
