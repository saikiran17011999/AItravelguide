# Delivery roadmap and approval gates

## Operating principle

The project moves from evidence to prototype to implementation. A phase does not close merely because a document exists; it closes when its risks, test evidence, and unresolved choices are visible and the user approves the next gate.

## Phases

| Phase | Outcome | Required artefacts | Approval gate |
| --- | --- | --- | --- |
| 0. Foundation | Shared product and trust constraints | Current instruction files and documentation index | Complete for planning only. |
| A. Discovery | Evidence for user problem, competitors, and feasible pilot corridor | Research notes, provider scorecard, user-research plan, risks | Geography/corridor is approved in DEC-001; provider/licence proof remains open. |
| B. Requirements | Bounded MVP and testable product contract | Approved PRD, user stories, acceptance criteria, trust/freshness policy | Approve MVP scope and data/privacy boundaries. |
| C. Experience design | Testable mobile-first interaction model | Task flows, wireframes, content rules, design system direction | Approve primary flow and screen specification. |
| D. Architecture | Buildable, lawful, secure technical plan | Selected-provider decision records, schemas, threat/privacy assessment, deployment outline | Approve stack and providers before provisioning or coding. |
| E. Prototype | One end-to-end document-to-guide proof | Prototype, authorised sample data, test report, cost/latency baseline | Approve whether to build the production MVP. |
| F. MVP implementation | Production-ready narrow release | Backlog, tests, monitoring, runbooks, release plan | User review and release approval. |

## First prototype definition

Build only after phases A–D are approved. The prototype should demonstrate one traveller journey:

1. Upload a consented, representative ticket/itinerary or use clearly labelled sample data.
2. Extract and review critical facts, including an ambiguity/correction case.
3. Plan a public-transport journey within the approved pilot corridor.
4. Show a source-labelled journey timeline and at least one authorised visual/diagram fallback.
5. Generate a mobile step-by-step guide and matching PDF snapshot.
6. Demonstrate failure states: missing route data, stale live data, conflicting input, unsupported image, and offline guide access.

The prototype must not claim support for untested countries, live monitoring, platform guidance, or provider content rights.

## Initial work breakdown

### Discovery and requirements

- [ ] Choose candidate launch corridors and score them using the provider evaluation criteria.
- [ ] Conduct 5–8 interviews or usability sessions with the intended travellers; confirm language, anxiety, luggage, and offline needs.
- [ ] Collect a consented, representative test corpus of flight/train tickets and screenshots; define data-handling rules first.
- [ ] Convert PRD requirements into user stories with acceptance criteria and explicit non-goals.
- [ ] Define fact statuses, freshness rules, transfer-buffer policy, recovery language, and source-attribution requirements.

### Experience design

- [x] Produce low-fidelity mobile wireframes for all screens in the experience specification. Visually reviewed by the product owner as a clickable mockup on 2026-10-15 ([wireframes](../design/wireframes.md), [design system](../design/design-system.md)).
- [ ] Test the document-review and current-step screens with target users before visual polish.
- [ ] Define copy patterns for uncertainty, stale data, no route, conflicting data, and emergency escalation.

### Architecture and provider selection

- [ ] Evaluate two or more provider combinations against the selected corridor; record price, terms, coverage, performance, and fallback.
- [ ] Define data classification, retention/deletion policy, consent, access control, and incident/audit needs.
- [ ] Approve the data model, versioning model, tool boundaries, and generated-guide schema.
- [ ] Decide whether any local/offline model has a real product benefit; do not select it merely for novelty.

### Prototype validation

- [ ] Run scenario tests and user comprehension sessions.
- [ ] Inspect generated PDFs on mobile and verify source/visual attribution.
- [ ] Measure cost, latency, correction rate, source coverage, and guide comprehension.
- [ ] Decide whether to improve, narrow, change geography, or stop before production investment.

## Definition of readiness for application scaffolding

Do not create the app until all of the following have written approval:

1. Pilot geography/corridor and intended user segment.
2. MVP boundary and user flow.
3. Selected providers with licence, cost, and fallback review.
4. Personal-data classification, retention/deletion, and consent approach.
5. Architecture/data-model/guide-schema direction.
6. Wireframes for the primary mobile flow. — Reviewed and approved 2026-10-15; see the mockup note above.
7. Evaluation plan and minimum prototype success measures.

Items 3 and 4 remain open (see [open questions](open-questions.md)) and still block application scaffolding even though item 6 is satisfied.

The pilot geography, release type, English-first language strategy, source-labelled schedule-only MVP, and brand direction are approved in [DEC-001](../decisions/DEC-001-frankfurt-pilot-baseline.md). These approvals do not select paid services or satisfy the provider/licence/privacy gates.

## Branch and review practice

All documentation, prototype, and application work follows the repository policy: use a focused branch, push no direct changes to `main`, report the branch/commit/checks, and wait for explicit user merge approval.
