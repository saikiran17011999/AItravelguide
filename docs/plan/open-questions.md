# Open questions and decision log

## Decisions needed before application implementation

| Priority | Decision | Why it changes the design | Suggested owner |
| --- | --- | --- | --- |
| P0 | What country/city and airport/station-to-destination corridor launches first? | Determines route, operator, map, language, legal, and live-data providers. | Product owner |
| P0 | Is the first release a private prototype, closed beta, or public service? | Changes authentication, compliance, support, scale, and monitoring obligations. | Product owner |
| P0 | What exact promise may we make about live information? | Must match actual feed coverage, latency, and escalation capability. | Product + technical owner |
| P0 | What ticket data may be stored, for how long, and in which region? | Governs storage, OCR vendor, logging, deletion, consent, and data-residency choices. | Product + legal/privacy owner |
| P0 | Which source licence permits the planned in-app map, visual reference, attribution, caching, and PDF use? | Affects the viability of core visual/export features. | Product + legal/commercial owner |
| P1 | Which languages are required for the pilot? | Affects OCR quality, translations, UI layout, terminology, and user research. | Product owner |
| P1 | Must the guide work only as a downloaded PDF, as an offline PWA page, or both? | Changes storage, caching, security, and UX complexity. | Product + technical owner |
| P1 | Which accessibility needs are launch-critical? | Affects route constraints, provider choice, content, and testing. | Product owner |
| P1 | Is user location needed during travel mode? | Changes consent, privacy, battery use, and recovery design. | Product + privacy owner |
| P1 | Who will operate customer support and provider/service incidents? | Determines escalation UX, audit logs, and service-level expectations. | Product owner |

## Questions that should not be postponed

1. Which initial corridor do you want to serve first?
2. Do you want the first goal to be a private clickable prototype, a working prototype for invited testers, or a public MVP?
3. Should ticket files be deleted immediately after extraction/confirmation, retained until the trip ends, or kept until the user deletes them?
4. Which languages must a first-time traveller be able to use on day one?
5. Do you want a guide that is only downloadable/offline, or should it also monitor the trip in real time when data allows?

## Assumptions currently used

- The MVP will begin with one restricted geography, not global travel support.
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
