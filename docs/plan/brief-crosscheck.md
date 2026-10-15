# Product-brief cross-check

## Review result

The initial brief defines a valuable, differentiated product and appropriately warns against unsupported travel claims. It is ready to move through discovery and requirements work. It is **not** ready for application scaffolding because the launch geography, provider/licence fit, privacy policy, and live-data promise are not yet decided.

## Requirement traceability

| Brief area | Status | Current documentation | Remaining action before code |
| --- | --- | --- | --- |
| Vision, problem, and target users | Covered | [PRD](../product/PRD.md) | Validate through target-user interviews. |
| Trip creation and document upload | Covered as MVP requirement | [PRD](../product/PRD.md), [data/trust model](../architecture/data-and-trust.md) | Approve file policy, OCR vendor, retention, and consent. |
| Extraction review and ambiguity handling | Covered | [Experience](../product/experience.md), [data/trust model](../architecture/data-and-trust.md) | Test on representative, consented documents. |
| Multi-leg route planning | Covered with a narrow MVP boundary | [PRD](../product/PRD.md), [provider evaluation](../research/provider-evaluation.md) | Select and prove one corridor/provider combination. |
| Visual references and maps | Covered with licence safeguards | [PRD](../product/PRD.md), [provider evaluation](../research/provider-evaluation.md) | Obtain specific display/export/caching permission and attribution rules. |
| AI-generated instructions | Covered with fact/source constraints | [data/trust model](../architecture/data-and-trust.md) | Approve guide schema and evaluate grounded output. |
| Interactive travel mode | Covered as MVP flow | [Experience](../product/experience.md) | Wireframe and usability-test the current-step/recovery experience. |
| PDF and offline access | Covered as a versioned snapshot | [PRD](../product/PRD.md), [architecture](../architecture/overview.md) | Select renderer and define legal caching/retention rules. |
| Live monitoring and disruptions | Deferred/conditional | [PRD](../product/PRD.md), [provider evaluation](../research/provider-evaluation.md) | Enable only after specific feed coverage and alert tests. |
| Data model and provenance | Covered | [data/trust model](../architecture/data-and-trust.md) | Convert approved logical model into selected database schema. |
| Privacy, reliability, and safety | Covered at principle level | [architecture](../architecture/overview.md), [roadmap](roadmap.md) | Complete threat/privacy assessment for chosen stack/providers. |
| Measurable non-functional targets | Planned, not invented | [PRD](../product/PRD.md), [validation plan](validation-plan.md) | Baseline prototype performance before setting public SLOs. |
| Future features | Explicitly deferred | [PRD](../product/PRD.md), [roadmap](roadmap.md) | Re-prioritise only after MVP validation. |

## Critical constraints found

1. **Transport data is geographically uneven.** A standard such as GTFS-Realtime describes possible trip updates and alerts, but does not guarantee that a particular agency provides complete, timely data.
2. **Route results are not station wayfinding.** A mapping route alone cannot prove the correct entrance, indoor path, platform, or coach position. Those claims require an appropriate official source or an explicit “check on arrival” instruction.
3. **Map/image rights can block the PDF feature.** The product must review each provider's display, attribution, caching, and export rules before embedding content in an offline guide.
4. **Ticket documents contain sensitive personal and booking data.** Extraction needs private storage, minimal logging, user correction, deletion controls, and vendor/privacy review.
5. **AI increases explanation quality, not factual certainty.** Structured, versioned evidence must constrain the guide generator and trip assistant.
6. **Offline access cannot mean live data.** Guides must carry a snapshot time and direct the traveller to recheck volatile information.

## Decision checkpoints

| Checkpoint | Evidence required | Decision |
| --- | --- | --- |
| Pilot corridor | User demand, route coverage, operator sources, language/accessibility needs | Choose one geography/corridor. |
| Provider/licence fit | Sample requests, pricing, terms, attribution/export/caching review | Select or reject each provider. |
| Data/privacy design | Data inventory, retention/deletion, consent, access-control model | Approve document and location-data handling. |
| Experience viability | Wireframes and target-user comprehension sessions | Approve primary flow and recovery UX. |
| Prototype value | Test scenario results, costs, latency, correction rate, source coverage | Approve or change the production MVP plan. |

See the [roadmap](roadmap.md) for the ordered delivery plan and [open questions](open-questions.md) for the outstanding owner decisions.
