# Technology options and cost comparison — private prototype

**Snapshot date:** 2026-10-15. Prices and terms change; confirm them in the provider console and contract before any purchase. No option is selected by this document.

## Decision criteria

The pilot needs one legally usable, reliable path from Frankfurt Airport to a precise Boxberg address. Evaluate each option for:

- scheduled public-transport routing across the airport, long-distance rail, Heidelberg, and local connection;
- location resolution and external navigation links;
- source/freshness/attribution and PDF-use permissions;
- prototype cost, implementation effort, privacy, and fallback behaviour;
- ability to keep route, map, OCR, and LLM providers replaceable.

## Route, location, and map options

| Option | Strengths for this pilot | Cost / operational model | Important limits | Prototype assessment |
| --- | --- | --- | --- | --- |
| Google Maps Platform (Routes, Geocoding, map/deep links) | One commercial platform with transit routing, location resolution, walking segments, and familiar map interactions. Google documents transit route details and preferences including fewer transfers/less walking. | Pay-as-you-go. At this snapshot, Routes Compute Routes Essentials lists 10,000 no-cost monthly events then US$5 per 1,000; Pro lists 5,000 then US$10 per 1,000. Geocoding Essentials lists 10,000 then US$5 per 1,000. Billing account and quotas are required. | Transit requests have documented limits; coverage and data freshness vary. Google terms/attribution/caching restrictions require review, especially for embedded map/image/PDF content. | Strong integration candidate for a small private proof, if terms permit the exact display/export pattern. Start with external links and minimal stored map content. |
| Official/regional transport sources (VRN Open Data / EFA JSON, operator material) | VRN publishes open-data resources and EFA JSON material; an official Fraport reference is a candidate for Fernbahnhof wayfinding. Gives a path to local terminology and official evidence. | Potentially low API cost, but licence, coverage, uptime, API limits, support, and cross-network functionality must be confirmed individually. | A regional source may cover the Heidelberg/Boxberg leg but not the entire Frankfurt-airport/long-distance rail journey. Combining providers increases normalisation and failure complexity. | Research/validation candidate for the final local leg and curated references; do not assume end-to-end coverage. |
| Open-source routing/map stack (OpenTripPlanner + licensed GTFS + MapLibre/hosted tiles) | Maximum control, provider independence, and custom evidence model. Can be adapted to selected feeds. | Software licence cost can be low, but engineering, feed maintenance, tile hosting, routing operations, monitoring, and legal review are real costs. | Requires authorised/complete GTFS feeds across the route. Public OSM tile servers are not a production map-hosting plan. | Not recommended for the first private vertical slice unless the selected regional data proves easy to operate. Keep as a later control/cost option. |
| External navigation handoff only | Lowest implementation and legal surface for early testing; user opens supported map/navigation app. | Usually no in-app map-rendering cost, but link terms must still be checked. | Does not provide the differentiating explanation, station visual, or route evidence by itself. | Use as a fallback in every option and as the first prototype's map behaviour. |

## OCR and ticket-extraction options

| Option | Cost model | Benefits | Risks / recommendation |
| --- | --- | --- | --- |
| Native PDF text extraction + manual confirmation | No external per-page API cost; normal app compute/storage cost only. | Best first path for born-digital tickets; keeps the workflow demonstrable with fewer vendors. | Does not handle scanned/image tickets alone. Keep manual entry and review mandatory. |
| Local OCR engine | No per-page API bill, but local/server compute and quality evaluation are required. | Private prototype option for images and an offline-friendly experiment. | Quality/language/layout performance must be benchmarked against real ticket samples; never treat output as fact. |
| Managed OCR / Document AI | Google lists Enterprise Document OCR at US$1.50 per 1,000 pages at the listed volume tier; layout/form extraction can cost more. | Faster time to a capable multi-format OCR pipeline, with operational quotas/support. | Creates a data-processing vendor relationship and requires storage region, privacy, and retention approval. Compare a small test corpus before committing. |

## LLM and guide-generation options

The guide generator is not a route provider. It receives only approved structured facts and emits schema-validated English instructions. Its cost should be estimated from actual input/output token measurements on the pilot scenario—not from chat-subscription pricing.

| Option | Cost / privacy model | Appropriate use | Recommendation |
| --- | --- | --- | --- |
| Hosted LLM API with structured output | Token-based variable cost. Evaluate provider data policy, region, structured-output quality, latency, and cost using the same test prompts. | Guide wording, translations later, clarification, and structured extraction candidates. | Best initial quality/effort balance if ticket privacy terms are approved. Keep a provider adapter and budget cap. |
| Gemini Developer API | Google publishes free/paid tiers; the published Gemini 3.8 Flash rate in this snapshot is US$0.75/M input and US$3.75/M output through 2026, with separate charges for search/maps grounding after shared free allowances. | Potentially convenient for a Google-based prototype. | Do not use built-in web/maps grounding as the authoritative transport source; it does not replace route/provider evidence. |
| Local/open-weight model | No per-token vendor bill, but hardware, deployment, quality evaluation, maintenance, and energy cost remain. | Privacy-sensitive experiments or later controlled offline inference. | Not a shortcut to live travel data. Defer until the hosted baseline demonstrates a meaningful privacy/cost need. |

## PDF, storage, and hosting

| Capability | Prototype approach | Cost / constraint |
| --- | --- | --- |
| PDF | Server-render a versioned HTML guide; test mobile readability and retain source/attribution labels. | Rendering compute is generally low; provider-map/image export rights are the significant risk. |
| Storage | Private object storage for documents/exports plus relational storage for trip facts/evidence. | Cost is low at prototype volume; deletion, backup expiry, encryption, and access URLs matter more than price. |
| Authentication | Keep private prototype access limited to the owner/tester. | Avoid enterprise identity/admin infrastructure until beta scope is approved. |
| Monitoring | Structured application logs with redaction; provider request metrics and source-freshness events. | Start with low-cost hosted observability or platform-native logs; never store raw tickets in logs. |

## Cost-control policy for the prototype

1. Use simulated/de-identified tickets and a fixed scenario set for early design validation.
2. Add hard per-service quota/budget alerts before enabling any paid API.
3. Cache only information permitted by its provider terms; do not cache maps/images simply to lower cost.
4. Fetch route data only after user confirmation of core inputs; avoid speculative map/search calls while typing.
5. Generate one guide version per reviewed journey version; make refresh explicit.
6. Record cost per successful test journey by provider and operation.

## Recommendation before stack approval

For a private prototype, compare two vertical-slice candidates using the same simulated scenarios:

- **Candidate A — managed integration:** a commercial route/location provider with external navigation handoff, native PDF text extraction plus manual review, and a hosted structured-output LLM.
- **Candidate B — mixed official/open data:** a verified official/regional source for the Heidelberg/Boxberg leg plus a separate approved source for the airport/rail leg, external navigation handoff, and the same extraction/LLM constraints.

Choose only after testing coverage, source attribution, route correctness, unavailable-data handling, PDF permissions, latency, and per-journey cost. Do not choose a paid provider based only on a map demo.

## Sources to recheck at selection time

- [Google Routes transit documentation](https://developers.google.com/maps/documentation/routes/transit-route)
- [Google Routes usage and billing](https://developers.google.com/maps/documentation/routes/usage-and-billing)
- [Google Maps Platform global pricing](https://developers.google.com/maps/billing-and-pricing/pricing)
- [Google Maps service-specific terms](https://cloud.google.com/maps-platform/terms/maps-service-terms)
- [VRN Open Data](https://opendata.vrn.de/)
- [VRN EFA JSON API training material](https://opendata.vrn.de/sites/default/files/2023-11/EFA_JSON_API_Training_EN_2.1.pdf)
- [OpenStreetMap tile policy](https://operations.osmfoundation.org/policies/tiles/)
- [Google Document AI pricing](https://cloud.google.com/products/document-ai/pricing)
- [Gemini Developer API pricing](https://ai.google.dev/gemini-api/docs/pricing)
- [Fraport wayfinding reference candidate](https://www.fraport.com/content/dam/fraport-company/documents/newsroom/medien/hinweise-fuer-pressevertreter/how-to-find.pdf/_jcr_content/renditions/original./how-to-find.pdf)
