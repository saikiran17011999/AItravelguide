# Provider recommendation — draft, pending product-owner approval

**Status: proposal, not a decision.** This is not an approved provider selection. [CLAUDE.md](../../CLAUDE.md) and the [roadmap](../plan/roadmap.md) require written approval, with licence/cost/fallback evidence, before any provider is treated as selected — nothing here authorises creating a billing account, generating an API key, or writing code against these services. It reasons from the existing research in [provider-evaluation.md](provider-evaluation.md) and [options-and-costs.md](options-and-costs.md) to give the product owner something concrete to approve, reject, or amend, per [DEC-001](../decisions/DEC-001-frankfurt-pilot-baseline.md)'s remaining approval item on provider selection.

## Recommendation

**Start the first vertical slice on Candidate A (Google Maps Platform: Routes + Geocoding) for all three legs, scoped narrowly — deep-links and text routing only, no cached map imagery — and treat VRN open data as a fast-follow comparison for the local Heidelberg → Boxberg leg only, not a day-one dependency.**

Reasoning, against the roadmap's own stated priority (*"prioritise demonstrating the entire end-to-end workflow... do not implement unnecessary production infrastructure until the core experience has been validated"*):

| Factor | Candidate A (Google Maps Platform) | Candidate B (VRN + separate rail source) |
| --- | --- | --- |
| Integration effort for a 1-person private prototype | One vendor, one adapter, transit routing covers airport walk + ICE + local bus in the same API shape. | At minimum two providers (VRN for the local leg, something else for Frankfurt Airport → Heidelberg Hbf rail) — [options-and-costs.md](options-and-costs.md) itself flags this as "increases normalisation and failure complexity." |
| Coverage confidence for the exact corridor | Google's transit routing already indexes German regional GTFS feeds broadly, so the Heidelberg-area local bus leg is plausibly covered — **not yet verified**, see "What must happen before this is a decision" below. | VRN is the actual regional authority for the Rhein-Neckar area including Boxberg, so official coverage is more certain for that one leg — but it does not cover the Frankfurt Airport/long-distance rail leg at all. |
| Cost at prototype volume | Essentially free — Routes Essentials' no-cost monthly tier (10,000 events) and Geocoding's (10,000 events) comfortably cover weeks of single-person testing. | Likely low cost, but "licence, coverage, uptime, API limits, support... must be confirmed individually" per the existing research — unquantified. |
| Licence/export risk | Real, but narrow and known: Google restricts caching/extracting Maps *content* (tiles, imagery) outside the service. The architecture already states a preference for external navigation handoff over cached map images ([DEC-001](../decisions/DEC-001-frankfurt-pilot-baseline.md) consequences), so this recommendation scopes Candidate A to **route/location data plus deep-links only** — never caching a map image into the PDF/offline snapshot. That keeps the plan inside Google's terms without a separate legal review being a blocker for the first slice. | Open data generally licenses more permissively for caching/reuse, which is actually an argument *for* VRN specifically for the local leg once the first slice works — this isn't a reason to start there. |
| Official station/wayfinding reference | The Fraport PDF reference candidate is independent of this choice either way — it's a separate, manually curated asset regardless of route provider. | Same — independent of this choice. |

**OCR:** start with native PDF text extraction + manual confirmation only (matches the [simulated fixtures](../../fixtures/tickets/README.md), which are born-digital text). Do not add a managed OCR vendor (e.g., Document AI) until testing shows the fixtures or real scans actually need it — this avoids a second data-processing vendor relationship before it's proven necessary.

**LLM:** keep this decision independent of the maps/routing choice — the architecture already requires the guide generator to sit behind a provider adapter ([overview.md](../architecture/overview.md)), so using Google for routing does not imply using Google for the LLM. Recommend deferring the specific LLM vendor pick until the route/location adapter is working, since it doesn't block that work and the cost difference between reasonable hosted options is immaterial at this volume.

## What must happen before this becomes an approved decision

Per the [provider-evaluation.md](provider-evaluation.md) evaluation protocol — none of this has been done yet, and I can't do it from here (it needs a real account and real test calls):

1. Create a Google Cloud billing account (your action, not mine — this is a real account/cost-bearing step) and set a hard budget alert before any key is generated.
2. Run the 10–20 realistic test scenarios from provider-evaluation.md against the actual Frankfurt Airport → Heidelberg Hbf → Boxberg corridor, including an evening arrival and a no-live-data case, and record real responses.
3. Confirm in writing (or at minimum, by re-reading the current Maps Platform service terms at selection time, since terms change) that deep-link-only usage with no cached imagery needs no further permission.
4. Decide, from real test results, whether the Heidelberg → Boxberg leg's Google-returned coverage is good enough, or whether to swap in VRN for that leg specifically.

## If you'd rather not use Google at all

The honest alternative is Candidate B in full (VRN + a separate long-distance-rail source), accepting the higher integration effort up front in exchange for not depending on Google for anything. I didn't recommend it as the starting point only because it's more engineering for a private, single-user prototype whose stated priority is proving the workflow quickly — not because Candidate A is clearly the right production choice. That's a legitimate call for you to make differently if you have a standing preference against Google dependencies.
