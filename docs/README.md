# AI Travel Companion documentation

## Status

**Phase:** Discovery, requirements, and low-fidelity experience design.
**Implementation status:** No application code or provider has been approved.

This set translates the initial product brief into a reviewable, implementation-ready plan. It deliberately preserves decisions that require product, commercial, legal, or user approval.

## Reading order

1. [Product requirements](product/PRD.md) — the problem, users, scope, and MVP.
2. [User stories](product/user-stories.md) — testable stories, acceptance criteria, and non-goals per functional area.
3. [Experience specification](product/experience.md) — journey flow, information architecture, screens, and trust cues.
4. [Architecture overview](architecture/overview.md) — boundaries, flows, provider adapters, and security.
5. [Data and trust model](architecture/data-and-trust.md) — entities, evidence, verification, and AI constraints.
6. [Provider evaluation](research/provider-evaluation.md) — research findings, selection criteria, and licensing gates.
7. [Delivery roadmap](plan/roadmap.md) — staged work, approval gates, and prototype plan.
8. [Open questions](plan/open-questions.md) — decisions needed before implementation.
9. [Frankfurt pilot decision](decisions/DEC-001-frankfurt-pilot-baseline.md) — approved design baseline and assumptions.
10. [Wireframes](design/wireframes.md) and [design system](design/design-system.md) — mobile-first interface direction.
11. [Frankfurt pilot architecture](architecture/frankfurt-pilot.md) and [options/costs](research/options-and-costs.md) — vertical-slice boundary and provider comparison.
12. [Usability-test script](plan/usability-test-script.md) and [simulated ticket fixtures](../fixtures/tickets/README.md) — how to run the target-user sessions and what test data to use.

## Source-of-truth rules

- The user’s latest explicit decision overrides this documentation.
- `CLAUDE.md` and `AGENTS.md` set mandatory implementation and review rules.
- Do not claim a provider, country, live feed, image, or map capability until it is recorded as approved in a decision log with its evidence, scope, cost, licence, and fallback.
- Update the relevant document when a product or architecture decision changes; keep open questions open until the decision owner resolves them.

## Current recommendation

Build a **single-corridor, document-to-guide prototype** before a broad travel platform:

1. Let a traveller upload one flight or rail ticket and review the extracted details.
2. Plan a Frankfurt Airport → Heidelberg Hbf → Boxberg journey, using exact arrival time and a precise destination address.
3. Generate a traceable, step-by-step guide and mobile/offline-friendly PDF.
4. Make uncertainty, source, freshness, and recovery guidance visible.

Live monitoring, global transport coverage, camera recognition, voice navigation, and autonomous bookings remain later phases.
