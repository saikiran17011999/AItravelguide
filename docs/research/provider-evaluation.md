# Provider and market evaluation

**Status:** Preliminary research, last reviewed 2026-10-15.
**Decision:** No provider is selected. This document identifies what must be proven for the launch corridor; it is not legal advice.

The approved pilot corridor is Frankfurt Airport → Heidelberg Hbf → Boxberg. See [technology options and cost comparison](options-and-costs.md) for a provider-neutral shortlist, current public price references, and selection protocol.

## Market cross-check

Google Maps, Citymapper, and Moovit already provide core trip-planning, transit, and live-direction capabilities in supported areas. Google Maps exposes transit departures that may be real-time or scheduled; Moovit describes routes with walking/stop details and, where available, live directions; Citymapper describes live route planning and step-by-step journey assistance. The product should not compete by duplicating their generic map UI.

The defensible opportunity is a **provenance-first document-to-guide workflow**:

1. Start with the traveller's own ticket/itinerary.
2. Ask the traveller to correct ambiguous extraction before relying on it.
3. Combine confirmed booking facts with selected, lawful transport/location sources.
4. Explain the physical journey in simple, local-language-aware steps, with visual references where authorised.
5. Make source, freshness, uncertainty, and recovery guidance visible in the guide and PDF.

## Evidence reviewed

| Topic | Finding relevant to the product | Product implication |
| --- | --- | --- |
| Google transit routing | Google Routes API documents public-transport routes with walking segments, stop/timing/line details and transit preferences such as fewer transfers or less walking. It also documents limitations, including no intermediate waypoints on transit requests and constrained future/past time windows. | A useful candidate for a limited prototype, not proof of universal indoor/platform coverage or long-range timetable reliability. |
| Google Maps content terms | Google requires attribution and limits extraction, scraping, caching, and use of Maps content outside the service. Rules differ by product and region. | Do not assume route/map/image content can be copied into storage or PDF exports. Obtain product-specific legal/commercial review before use. |
| GTFS and GTFS-Realtime | GTFS-Realtime can describe trip updates, vehicle positions, and service alerts, but each feed is tied to underlying scheduled data. Absence of a trip update does not mean a service is on time. | Live monitoring is location- and provider-specific. Show the live-feed source, freshness, and no-data state; never imply full coverage. |
| Existing transit apps | Google Maps, Moovit, and Citymapper offer route choice, departures, walking/transit guidance, alerts, and varying live data in supported locations. | The MVP needs to differentiate through booking ingestion, explicit verification, operationally useful station guidance, and offline-ready guide snapshots. |
| OCR/document AI | Managed document-processing systems can extract text/structure from PDFs and images, but extraction remains a candidate pipeline rather than a trusted booking source. | Build a review-and-confirmation step; retain field/page evidence and manual entry fallback. |

## Candidate categories and decision criteria

| Capability | Evaluate | Minimum proof before selection |
| --- | --- | --- |
| Geocoding/location resolution | Ambiguity handling, canonical IDs, language support, coverage, caching/attribution terms | Resolve pilot airport, stations, stops, and destination addresses reproducibly. |
| Route planning | Walking + public transit, arrival/departure time, alternatives, preferences, deep links, response limits | Reproduce the pilot corridor across representative times and disruption scenarios. |
| Live service data | Scheduled vs real-time distinction, alert and platform coverage, update frequency, licence | Show exactly which pilot journeys receive updates; present a no-live-data fallback. |
| Operator/station references | Official station maps, entrance directories, signage, accessibility data | Legally permitted, current references for every claimed guidance detail. |
| Maps and imagery | Display, PDF/export, caching, attribution, geographic coverage, price | Written approval that planned in-app and export use is permitted. |
| OCR/extraction | Supported file types/languages, field evidence, latency, privacy/data residency, accuracy | Test with a diverse, consented ticket corpus; measure field correction rates. |
| LLM | Structured output, multilingual quality, privacy, cost, tool governance | Constrain generation to the guide schema and verify it cannot alter input facts. |
| PDF/offline | Accessible mobile layout, hyperlinks, local persistence, sensitive-data handling | Render/inspect a guide that exactly matches a versioned journey snapshot. |

## Launch geography selection scorecard

Select a single airport/station-to-destination corridor only after scoring each candidate 1–5 and recording evidence.

| Criterion | Weight | Why it matters |
| --- | ---: | --- |
| Authorised scheduled route data | 20% | The core journey must be complete and reproducible. |
| Lawful, usable real-time/alert data | 15% | Determines whether live monitoring can be promised. |
| Official station/wayfinding references | 15% | The product’s physical-navigation advantage depends on these. |
| Map/imagery/PDF licence fit | 15% | Prevents a prototype that cannot be launched lawfully. |
| Typical international-arrival demand | 10% | Ensures meaningful user research and realistic journeys. |
| Accessibility/luggage route information | 10% | Supports core user needs. |
| Cost and reliability at prototype volume | 10% | Avoids provider lock-in before value is proven. |
| Available support and clear terms | 5% | Makes operational issues resolvable. |

Do not select a geography only because a map application looks good there. The final choice needs provider terms, sample responses, user demand, and operational-source checks.

## Evaluation protocol

For each candidate corridor, run the following with authorised test data:

1. Create 10–20 realistic arrival-to-destination scenarios, including evening arrival, luggage, limited walking, transfer, missed connection, and no-live-data cases.
2. Evaluate document extraction independently from routing; record field-level correction and ambiguity rates.
3. Compare provider responses with official operator information at the time of test. Record source, timestamp, coverage, gaps, and discrepancies.
4. Verify visual-reference licensing, attribution, caching, and PDF/export permissions before displaying assets.
5. Test the guide with target travellers. Measure whether they can explain the next action, recognition cue, and recovery action without help.
6. Test unavailable provider, stale update, delayed export, bad upload, and offline-guide scenarios.
7. Record per-trip/provider cost, latency, availability, and integration effort.

## Reference sources

- [Google Routes API — transit routes](https://developers.google.com/maps/documentation/routes/transit-route)
- [Google Maps Platform service-specific terms](https://cloud.google.com/maps-platform/terms/maps-service-terms)
- [GTFS Realtime reference](https://gtfs.org/documentation/realtime/reference/)
- [GTFS-Realtime service-alert guidance](https://gtfs.org/resources/mobilitydata-recommendations/gtfs-realtime-service-alerts/intro/)
- [Google Maps — public-transport departures](https://support.google.com/maps/answer/6142130)
- [Moovit — trip planning and live directions](https://support.moovitapp.com/hc/en-us/articles/212011605-Plan-a-Trip-Get-Directions)
- [Citymapper — step-by-step journey assistance](https://citymapper.com/news/517/go-your-personal-trip-assistant)
- [Google Document AI OCR overview](https://codelabs.developers.google.com/codelabs/docai-ocr-python)

Provider terms and capability documents change. Recheck them at procurement and before each new geography.
