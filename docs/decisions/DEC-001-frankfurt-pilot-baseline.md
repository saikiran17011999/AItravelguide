# DEC-001 — Frankfurt Airport to Heidelberg / Boxberg pilot baseline

- **Date:** 2026-10-15
- **Decision owner:** Product owner
- **Status:** Approved design baseline; provider and stack selection remain open

## Decision

The first experience is a **private, personal-testing prototype** for a traveller arriving at Frankfurt Airport and continuing to accommodation in Boxberg, Heidelberg.

The intended journey shape is:

```text
Arrival at Frankfurt Airport
→ find Frankfurt Airport long-distance rail station (Fernbahnhof)
→ rail journey to Heidelberg Hbf
→ local public-transport connection toward Boxberg
→ final walking step to a verified accommodation entrance
```

This is a scenario shape, not a pre-booked or live operational itinerary. Train number, train time, platform, local-bus line, stop, walking path, and accommodation entrance must be derived from the traveller's confirmed inputs and approved sources at planning time.

## Product decisions

| Topic | Decision |
| --- | --- |
| Pilot geography | Frankfurt Airport, Heidelberg Hbf, and a final destination in Boxberg, Heidelberg. |
| Release | Private prototype for personal testing; no public launch infrastructure or broad live-monitoring promise. |
| Interface and guide language | English first. Preserve original German names/signage next to the English explanation. Design content/schema for future German and Japanese. |
| Inputs | Arrival airport/location, arrival date and time, final accommodation address/pin, traveller preferences, uploaded booking documents, and optional intermediate tickets/reservations. |
| Intermediate travel | If a traveller supplies a booked train/bus ticket, preserve it as booking evidence. If not, propose source-labelled route options only; the proposal is not a booking and must be explicitly distinguished. |
| Live data | MVP uses verified scheduled information, map/deep links, and PDF/offline snapshots. Real-time updates are an optional adapter after a provider-specific proof. |
| Documents | Private processing, minimal retention, user-initiated deletion for original documents and derived trip data. A privacy-first default auto-expiry is proposed in [frankfurt-pilot.md](../architecture/frankfurt-pilot.md#data-minimisation-and-retention-design) (7 days post-travel for the raw file, 90 days for the whole trip); the final duration and storage region remain an approval item. |
| Brand | Temporary name “AI Travel Companion”; calm light-neutral surfaces, dark navy text, restrained blue accents, instruction-first rather than chatbot-first UI. |

## Assumptions recorded

1. The traveller knows their arrival date/time and can provide a precise accommodation address or map pin. “Boxberg” alone is not enough to create a reliable final walking step.
2. The prototype uses clearly marked simulated tickets and sample times unless the product owner supplies consented test documents and approved providers return current results.
3. The rail leg may be direct or may require a connection depending on the travel date/time. The prototype must not hard-code a train service or platform.
4. A local bus/tram leg toward Boxberg is a route-provider result, not an assumption. The guide must show “needs confirmation” if the source cannot provide the stop or service detail.
5. Official Fraport wayfinding material is a research candidate for the Fernbahnhof step, but any embedded/map/PDF use still needs source-specific permission and attribution review.

## Consequences

- The main flow starts with arrival time/location and precise destination collection, not with a generic chatbot prompt.
- The plan must have a separate state for user-confirmed booked legs versus recommended legs.
- The initial prototype should prefer external navigation links and a small set of manually reviewed/authorised references over automatic web-image retrieval.
- Production concerns such as broad-scale notifications, always-on location tracking, universal journey planning, and payment/rebooking are intentionally deferred.

## Remaining approval items

- Exact accommodation test address or representative test pin.
- Original document retention/auto-deletion duration and any backup policy (a proposed default exists; it is not yet confirmed).
- Selected route/location/map/OCR/LLM/PDF providers after technical and licence evaluation.
- Whether the private prototype will process real personal tickets or simulated/de-identified test documents only.
