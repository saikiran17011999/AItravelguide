# Validation and test strategy

## Purpose

Validate that the product improves real traveller understanding without presenting unverified facts as reliable guidance. This plan applies first to the document-to-guide prototype, then becomes the basis for production quality gates.

## Scenario suite

Build a consented, de-identified scenario set for the approved pilot corridor. Include:

| Scenario | What it validates |
| --- | --- |
| Clear flight/train ticket | Happy-path extraction, confirmation, routing, guide, and PDF. |
| Blurry screenshot or partial document | Low-confidence display, manual correction, and no hidden guess. |
| Similarly named stations | Location disambiguation and confirmation. |
| Separate ticket and seat reservation | Relationship between booking artifacts and guide details. |
| Tight transfer | Transfer-buffer warning and recovery language. |
| Missing platform/coach data | Correct “check live board” fallback. |
| Live feed delayed/cancelled | Clear distinction between schedule, real-time alert, and no-data. |
| Provider unavailable | Honest degraded experience and preserved confirmed booking facts. |
| No connection | Saved guide/PDF readability and freshness labels. |
| Accessibility/luggage preference | Preference handling and explicit provider limitations. |
| Conflicting sources | Conflict presentation; no silent choice by the LLM. |

## Test layers

### Data and provider integration

- Validate schemas for every provider adapter and reject malformed/unknown data.
- Record provider response timestamp, coverage, terms reference, and fact lineage for critical route fields.
- Use contract tests with saved, authorised fixtures; do not include real customer documents in source control.
- Test rate limits, timeout, retry, and provider-unavailable behaviour.

### Document extraction

- Measure field-level precision, recall, correction rate, and ambiguity rate for dates, stations, service numbers, coach/seat, and addresses.
- Require human confirmation for critical facts regardless of aggregate OCR confidence.
- Test unsupported, oversized, corrupt, and potentially malicious files.

### Guide generation and trip assistant

- Validate every output against the structured guide schema.
- Assert that every critical statement references a known fact/evidence ID.
- Seed conflicting, missing, stale, and prompt-injection content; verify the assistant asks/flags rather than invents.
- Test language simplification and translation with native-speaker or qualified-review feedback for the pilot languages.

### Experience and accessibility

- Run moderated task tests with target users on a small mobile screen and in low-attention conditions.
- Measure: Can the user state the next action, identify the recognition cue, distinguish live from scheduled information, and find recovery help?
- Test keyboard navigation, screen reader labels, text zoom, contrast, reduced motion, and non-colour status cues.

### Security and privacy

- Test authentication/authorisation for every trip, document, guide, and export.
- Test retention/deletion, access URL expiry, log redaction, consent withdrawal, and cross-user isolation.
- Perform a threat assessment for uploads, OCR/LLM providers, web/transport data, generated PDFs, and location permissions before beta.

### Operational quality

- Measure route/extraction/guide/PDF latency and cost per trip.
- Test observability: correlation IDs, safe error details, provider status, source freshness, and alert delivery.
- Define prototype baselines before setting production service-level objectives.

## Prototype exit criteria

The prototype can move to a production-MVP decision only when it demonstrates, with recorded evidence:

1. A traveller can complete the primary journey flow using the pilot corridor.
2. Critical extraction ambiguities require correction rather than becoming silent facts.
3. Every critical guide statement can be traced to a document, selected provider, or explicit user confirmation.
4. The guide remains understandable when live data is missing or stale.
5. Visual/map/PDF content used in the prototype has documented permission and attribution.
6. The identified privacy/security risks have an approved mitigation or are explicitly accepted by the decision owner.
