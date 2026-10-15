# Open questions and decision log

## Decisions needed before application implementation

The pilot corridor, private-release goal, English-first language strategy, user-controlled deletion direction, schedule-only MVP, and visual direction are approved in [DEC-001](../decisions/DEC-001-frankfurt-pilot-baseline.md).

| Priority | Decision | Why it changes the design | Suggested owner |
| --- | --- | --- | --- |
| P0 | What exact arrival time and precise Boxberg accommodation test address/pin will be used in the representative scenario? | Determines whether the final local connection and walking flow can be tested honestly. | Product owner |
| P0 | Which provider combination passes coverage, licence, PDF/export, cost, and fallback checks for Frankfurt → Heidelberg → Boxberg? | Selects the actual technical path without over-promising data coverage. | Product + technical owner — a draft recommendation exists in [provider-recommendation.md](../research/provider-recommendation.md), not yet approved; needs real test calls and a billing account the product owner creates. |
| P0 | What exact promise may we make about live information after provider evaluation? | The baseline is schedule-only; any live claim must match coverage, latency, and escalation capability. | Product + technical owner |
| P0 | What ticket data may be stored, for how long, and in which region? | Governs storage, OCR vendor, logging, deletion, consent, and data-residency choices. User-controlled deletion is approved; a proposed privacy-first default (7 days raw file / 90 days whole trip, see [frankfurt-pilot.md](../architecture/frankfurt-pilot.md#data-minimisation-and-retention-design)) exists but is not confirmed, and the storage region is undecided. | Product + legal/privacy owner |
| P0 | Which source licence permits the planned in-app map, visual reference, attribution, caching, and PDF use? | Affects the viability of core visual/export features. | Product + legal/commercial owner |
| P1 | What quality bar and rollout order should apply to Japanese and German after English? | Affects OCR quality, translations, UI layout, terminology, and user research. | Product owner |
| P1 | Must the guide work only as a downloaded PDF, as an offline PWA page, or both? | Changes storage, caching, security, and UX complexity. | Product + technical owner |
| P1 | Which accessibility needs are launch-critical? | Affects route constraints, provider choice, content, and testing. | Product owner |
| P1 | Is user location needed during travel mode? | Changes consent, privacy, battery use, and recovery design. | Product + privacy owner |
| P1 | Who will operate customer support and provider/service incidents? | Determines escalation UX, audit logs, and service-level expectations. | Product owner |

## Questions that should not be postponed

1. What representative arrival date/time and precise Boxberg accommodation address/pin may we use for a simulated scenario?
2. May the prototype process any real ticket, or must it use simulated/de-identified documents only?
3. What is the automatic retention/backup-expiry duration for original ticket files after a trip ends?
4. Which provider combination passes the documented licence, cost, and coverage evaluation?
5. At what evidence threshold, if any, should a later phase add live transport monitoring?

## Assumptions currently used

- The MVP begins with the approved Frankfurt Airport → Heidelberg Hbf → Boxberg corridor, not global travel support.
- The traveller is required to review critical extracted facts before guidance is generated.
- External navigation applications may be opened for detailed map navigation.
- Live monitoring is a later capability unless the approved pilot provider proves suitable coverage.
- No real customer data or paid provider account will be used until the data, provider, and prototype gates are approved.

## Decision record format

When an answer is approved, replace the question with a dated decision entry:

```md
### DEC-001 — Pilot corridor
- Date:
- Decision owner:
- Decision:
- Evidence considered:
- Alternatives rejected:
- Consequences and follow-up:
```
