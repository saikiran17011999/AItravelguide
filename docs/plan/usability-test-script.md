# Usability-test script — Frankfurt pilot primary flow

For the product owner (or whoever they delegate) to run the roadmap's "5–8 interviews or usability sessions with the intended travellers" item. Written against the [clickable screen mockup](../design/wireframes.md) built from the approved wireframes and design system, using the [simulated ticket fixtures](../../fixtures/tickets/README.md) for any document-upload talking points. This script produces the evidence the roadmap's Experience design gate and [validation-plan.md](validation-plan.md) ask for — it does not replace either, and sessions should still be logged against validation-plan.md's scenario suite once real sessions are run.

## Before you start

- **Share the mockup first.** The Artifact is private by default — open it, use its Share menu to give each facilitator/participant access, and reconfirm the link still opens right before the session.
- **Consent and recording.** Tell participants the session may be recorded for internal product research only, get verbal or written consent, and state how long the recording will be kept (align with whatever retention default is active when you run this — see [DEC-001](../decisions/DEC-001-frankfurt-pilot-baseline.md)).
- **This is a static-ish mockup, not a working app.** File upload, OCR, and live data are not real. Tell participants plainly: "Some things are stubbed — when I ask you to 'upload a ticket,' just describe what you'd expect to happen; the screen won't actually process a file."
- **Duration:** 30–40 minutes per session. **Target:** 5–8 participants matching the PRD's target users (international student, first-time international traveller, tourist using public transport, accessibility/luggage-conscious traveller) — try to cover at least one accessibility-conscious participant and one with low confidence in English/German signage.

## Warm-up (3–5 min)

Ask, don't lead:
1. Tell me about the last time you arrived somewhere unfamiliar by plane or train. What was confusing?
2. Have you used a transit app (Google Maps, Citymapper, Moovit, a local app) to get somewhere new? What worked, what didn't?
3. On a trip, how anxious are you about missing a connection or getting lost — low/medium/high, and why?

Record their answers; they contextualize the task results and matter more than any single task score.

## Task list

Run tasks in order. For each: read the scenario prompt aloud, then stay quiet and let them think aloud. Only intervene if they are fully stuck for >60 seconds — note that as a failure, then unstick them so the session can continue.

### Task 1 — Start a trip (My Trips → Trip setup)
**Scenario:** "You're about to fly into Frankfurt and need to get to a place you're staying in Boxberg, near Heidelberg. Set up that trip."
- **Observe:** Do they understand why an exact address/pin is required, not just "Boxberg"? Do they notice the preference chips (fewer transfers, luggage, step-free)?
- **Success:** They complete Trip setup without facilitator help and can explain *why* a precise address is needed.

### Task 2 — Add a booking (Add bookings → Document review)
**Scenario:** "You already booked a train. Add that ticket." (Show fixture `01-ice-ticket-clear.txt` content as a stand-in image/description if asked what the ticket looks like.)
- **Observe:** Do they understand the difference between "upload" and "enter manually"? On Document review, do they notice which fields say "From your ticket" vs. "Needs review," and do they understand *why* one field needs review?
- **Success:** They can state, unprompted, which field is unconfirmed and why it matters before they'd trust the plan.

### Task 3 — Read the journey overview
**Scenario:** "Here's your full journey. Walk me through what you understand about each leg."
- **Observe:** Can they distinguish the booked leg ("From your confirmed ticket") from the recommended local connection? Do they understand "Recommended — review details" is not yet a booking?
- **Success:** They correctly identify which leg is booked and which is only a suggestion, without being told.

### Task 4 — Follow a travel-mode step
**Scenario:** "You've landed. Use the guide to find your train."
- **Observe:** Do they read the recognition cue ("Follow signs saying 'Fernbahnhof'") before trying to tap past it? Do they notice the source/freshness line? What do they expect "I found it" vs. "I cannot find this place" to do?
- **Success:** They can state the next action, the recognition cue, and whether the platform info is live or scheduled — this is the core measure from [validation-plan.md](validation-plan.md#experience-and-accessibility).

### Task 5 — Recover from a problem
**Scenario:** "You get to the station and can't find the platform shown. What do you do?"
- Have them tap "I cannot find this place" themselves rather than navigating you there.
- **Observe:** Do they understand the guide is *not* claiming to know the live platform? Do they know what to do next (check the board, open the map link, ask the assistant)?
- **Success:** They do not express false confidence that the app "already knows" the platform.

### Task 6 — Export and settings
**Scenario:** "You want a copy of this guide for offline use, and you want to check what happens to your data afterward."
- **Observe:** Do they notice the "recheck before you travel" warning on the PDF screen? In Settings, do they understand that the retention period shown is not finalized yet, and can they find delete controls?
- **Success:** They do not assume the PDF guarantees current live information.

## Debrief (5 min)

1. On a scale of 1–5, how confident would you feel actually doing this journey using only this guide?
2. Was there any point you felt unsure whether something was a fact or a guess?
3. What's missing that you'd want before you'd actually rely on this?
4. (If applicable) Anything about screen reader / keyboard / text-size use you want to flag?

## What to measure and log per session

Match these directly to the [validation-plan.md](validation-plan.md) and roadmap exit criteria — don't invent new metrics:

- Can they state the next action at each travel-mode step? (yes/no per task)
- Can they identify the recognition cue? (yes/no)
- Can they distinguish live/scheduled/booking-confirmed/needs-review states from each other? (yes/no, note which pair was confused if any)
- Can they find the recovery path unaided? (yes/no, time-to-recover if measured)
- Confidence rating (debrief Q1, 1–5)
- Any moment of false confidence (believing stale/illustrative content was live/verified) — log verbatim quote
- Accessibility defects observed (contrast, focus order, text size, screen-reader label gaps) — log against the specific screen

## After the sessions

Compile findings against validation-plan.md's scenario suite and prototype exit criteria before deciding whether to proceed to visual polish or the prototype build (roadmap Phase E). Do not average confidence scores across fewer than 5 participants into a headline number — report them individually with the context from the warm-up questions, consistent with the PRD's "do not publish target numbers before a pilot establishes a baseline."
