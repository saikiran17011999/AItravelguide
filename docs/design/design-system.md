# Design system direction — AI Travel Companion

## Brand character

Calm, precise, and reassuring. The interface should feel like a carefully prepared travel folder combined with a focused navigation aid—not a generic chatbot or a busy consumer map.

## Visual foundations

| Token | Direction | Intended use |
| --- | --- | --- |
| Canvas | `#F7F9FC` light neutral | App background; avoid pure-white glare over full screens. |
| Surface | `#FFFFFF` | Raised cards, form groups, and document review. |
| Ink | `#14263D` dark navy | Primary copy and headings. |
| Secondary ink | `#53657A` muted slate | Supporting metadata only, never critical instructions. |
| Travel blue | `#0B63CE` | Primary action, selected step, focus treatment, map/deep link. |
| Confirmed | `#087443` | Booking-confirmed/source-supported state, always paired with text/icon. |
| Caution | `#9A5B00` | Needs-checking, tight transfer, stale-data warning. |
| Alert | `#B42318` | Blocking error, conflict, or unavailable essential action. |
| Border | `#D9E1EA` | Quiet structural separation. |

Contrast must be tested against the final component states; these are starting tokens, not a substitute for WCAG 2.2 AA verification.

## Typography and spacing

- Use a highly legible sans-serif with robust Latin, German, and future Japanese fallback coverage.
- Body text defaults to at least 16 px. The current instruction uses the largest mobile text treatment and short, scannable lines.
- Use sentence case, familiar language, and local names in quotation marks: “Follow signs for ‘Fernbahnhof’.”
- Increase vertical spacing around a current action; do not compress guidance to fit more map content.
- Time, platform, line, coach, seat, and ticket values use a tabular-number style where available.

### Type scale

| Token | Size / line-height | Use |
| --- | --- | --- |
| `type-display` | 28 / 36 px | Current-step primary instruction only. |
| `type-title` | 22 / 28 px | Screen and section titles. |
| `type-body-lg` | 18 / 26 px | Default body copy, travel-mode text. |
| `type-body` | 16 / 24 px | Secondary body copy, form labels. |
| `type-meta` | 14 / 20 px | Source lines, timestamps, captions — never a critical instruction. |

### Spacing scale

4 px base unit; do not introduce arbitrary in-between values.

| Token | Value | Use |
| --- | --- | --- |
| `space-1` | 4 px | Icon-to-label gap, tight inline spacing. |
| `space-2` | 8 px | Related field grouping. |
| `space-3` | 12 px | Internal card padding on small screens. |
| `space-4` | 16 px | Standard card padding, form field spacing. |
| `space-6` | 24 px | Section separation within a screen. |
| `space-8` | 32 px | Space around the current-step primary action. |
| `space-12` | 48 px | Separation between major regions (e.g., desktop columns). |

### Radius

| Token | Value | Use |
| --- | --- | --- |
| `radius-sm` | 6 px | Inputs, chips, small badges. |
| `radius-md` | 12 px | Cards, sheets, buttons. |
| `radius-lg` | 20 px | Primary current-step card, modals. |
| `radius-pill` | 999 px | Preference toggles, status pills. |

### Elevation

Use elevation to separate layers, never to imply trust or verification state.

| Token | Shadow | Use |
| --- | --- | --- |
| `elevation-0` | none, border only | Inline content, flat sections. |
| `elevation-1` | `0 1px 2px rgba(20,38,61,0.08)` | Resting cards (journey timeline, fact rows). |
| `elevation-2` | `0 4px 12px rgba(20,38,61,0.12)` | Sheets, the active current-step card. |
| `elevation-3` | `0 8px 24px rgba(20,38,61,0.16)` | Modals, the assistant sheet, recovery overlay. |

### Breakpoints

| Token | Range | Layout |
| --- | --- | --- |
| `bp-mobile` | < 768 px | Single column, bottom-safe primary action, drawers/sheets for secondary content. |
| `bp-tablet` | 768–1199 px | Current instruction and journey timeline may sit side by side. |
| `bp-desktop` | ≥ 1200 px | Three-region workspace: trip navigation, timeline/map review, current instruction. |

No layout may require horizontal scrolling or a hover-only control at any breakpoint.

### Motion

| Token | Value | Use |
| --- | --- | --- |
| `motion-fast` | 120 ms, ease-out | Button/press feedback, toggle state. |
| `motion-standard` | 200 ms, ease-in-out | Sheet/modal open-close, step transition. |
| `motion-emphasis` | 280 ms, ease-in-out | Trust-state change (e.g., scheduled → live), used sparingly. |

When `prefers-reduced-motion` is set, replace sliding/scaling transitions with an instant or opacity-only change; never use motion as the only cue that a state changed, and never animate in a way that blocks interaction or auto-advances a step.

## Iconography

- Use a single simple, stroke-based icon style: 2 px stroke, 24 px grid, rounded joins, no fill except small status dots. Never photographic, skeuomorphic, or emoji icons.
- Draw transport-mode icons (train, bus, walk, plane) as an original, minimal set in this stroke style — do not trace or reproduce another company's icon set (e.g., Google's Material Symbols) verbatim; a recognisable third-party icon style is still that company's protected design, not a free reference.
- Keep transport-mode icons visually distinct from trust-state icons (check, calendar, pulse, warning triangle) so a traveller never confuses "which vehicle" with "how verified" at a glance.
- Every icon-only control has an accessible name (`aria-label`); a decorative icon paired with visible text is `aria-hidden`. Icons never carry meaning alone — always pair with the text/label patterns in the trust-state table below.

## Map and reference-panel interaction

The brief's "use Google Maps as a reference for familiar mapping interactions" means borrowing well-known map *gestures*, not adopting Google Maps as the visual differentiator — the step-by-step guide stays primary. The map/reference panel behaves differently depending on what it holds:

| Content | Interaction | Why |
| --- | --- | --- |
| An embedded live/external map excerpt (where licence permits) | Standard pan and pinch-zoom, like any familiar map app | Travellers already know these gestures; relearning one would slow them down mid-journey. |
| An official station diagram, signage photo, or illustrative graphic | Pinch/tap-to-zoom only, for legibility — no panning into undrawn space | It is a fixed reference image, not a navigable map; panning would falsely imply more coverage than the image has. |
| No authorised reference available | Static message, no map gesture at all | Nothing to interact with; the panel must not render an empty pannable canvas. |

Tapping the panel never silently substitutes a different location than the current step's confirmed segment.

## Trust-state system

| State | Colour role | Icon/label pattern | Example |
| --- | --- | --- | --- |
| Booking confirmed | Confirmed | Ticket/check icon + “From your confirmed ticket” | ICE number and seat. |
| Scheduled | Blue/neutral | Calendar icon + provider/timestamp | Planned departure time. |
| Live estimate | Blue/neutral with timestamp | Live indicator + “Updated 14:05” | Real-time departure, when supported. |
| Needs checking | Caution | Alert icon + explicit action | “Check the station board.” |
| Conflicting/unavailable | Alert | Alert icon + safe fallback | “We could not verify this platform.” |
| Illustrative visual | Neutral | Illustration label + source/caption | Generated diagram, not a photograph. |

Never use colour alone. Do not use a green state to mean “the journey is guaranteed.”

## Core components

| Component | Behaviour |
| --- | --- |
| Current-step card | One action, recognition cue, success check, source/freshness line, recovery action. No secondary chat input competes with it. |
| Journey timeline | Ordered segment cards with mode icon, status label, time/source, transfer risk, and expansion for details. |
| Fact-review row | Label, extracted/user/source value, confidence/state, edit action, field-level evidence. |
| Source line | Provider/source title, retrieval/check time, verification state, and link where allowed. |
| Map/reference panel | Authorised map/diagram/photo only; caption describes what to recognise and attribution remains visible. |
| Recovery sheet | Explains limitation, safe next step, verified external link if available, and return action. |
| Assistant sheet | Secondary trip-aware help. It cites the active journey and cannot replace the current instruction hierarchy. |
| Primary button | One per focused screen, e.g. “Continue,” “Confirm plan,” or “I found it.” |

## Responsive rules

Layout changes at the breakpoint tokens above. At every size: persistent journey title/progress, current instruction shown first, and no desktop-only hover interaction.

## Content rules

- Say “We could not verify the platform” rather than inventing one or using vague optimism.
- Explain local terms once: “Fernbahnhof (long-distance rail station).” Retain the sign text exactly when it matters.
- Give one instruction at a time; place contingencies in a clearly labelled warning or recovery section.
- Show simulated data with a persistent “Sample journey” label in prototype demonstrations.
- Do not describe an image as a station photograph unless the source, location, and permission have been verified.
