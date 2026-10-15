# Low-fidelity wireframes — Frankfurt to Boxberg pilot

These wireframes define behaviour and hierarchy, not final artwork. All travel dates, times, lines, platforms, and ticket values below are simulated examples and must be visibly marked as such in a prototype.

## 1. My Trips — mobile

```text
┌──────────────────────────────────┐
│ AI Travel Companion        [Help]│
│ Good morning                     │
│                                  │
│ [ + Plan an arrival journey ]    │
│                                  │
│ UPCOMING                          │
│ ┌──────────────────────────────┐ │
│ │ Frankfurt Airport → Boxberg  │ │
│ │ 18 Oct · arrival 15:20       │ │
│ │ Setup incomplete          ›  │ │
│ └──────────────────────────────┘ │
│                                  │
│ No journey data is shared until  │
│ you add it to a trip.            │
└──────────────────────────────────┘
```

**Primary action:** plan an arrival journey.  
**Empty-state purpose:** explain privacy and make the first action obvious.

## 2. Trip setup — required facts first

```text
┌──────────────────────────────────┐
│ ‹ Back             1 of 3        │
│ Plan your arrival                 │
│                                  │
│ Where will you arrive?            │
│ [ Frankfurt Airport            ] │
│                                  │
│ When do you expect to arrive?     │
│ [ 18 Oct 2026 ] [ 15:20 ]         │
│                                  │
│ Where are you staying?             │
│ [ Exact address or map pin      ] │
│ Boxberg, Heidelberg                │
│                                  │
│ Preferences                        │
│ [ Fewer transfers ] [ Luggage ]   │
│ [ Step-free if available ]         │
│                                  │
│                    [ Continue ]   │
└──────────────────────────────────┘
```

**Rule:** an airport, arrival time/date, and precise destination are required. “Boxberg, Heidelberg” is accepted as a search hint but cannot produce a final-door guide until resolved.

## 3. Add bookings — ticket optional, review mandatory

```text
┌──────────────────────────────────┐
│ ‹ Back             2 of 3        │
│ Add bookings                      │
│                                  │
│ ┌──────────────────────────────┐ │
│ │  Upload ticket or itinerary  │ │
│ │  PDF · JPG · PNG             │ │
│ │          [ Choose file ]     │ │
│ └──────────────────────────────┘ │
│                                  │
│ Already booked a train or bus?    │
│ Add it so we can follow its rules.│
│                                  │
│ No intermediate ticket?           │
│ We can suggest source-labelled     │
│ options after you continue.        │
│                                  │
│ [ Enter details manually ]         │
│                    [ Continue ]   │
└──────────────────────────────────┘
```

**Privacy note:** show delete controls and retention explanation beside the upload, not hidden in settings.

## 4. Document review — protect against extraction mistakes

```text
┌──────────────────────────────────┐
│ ‹ Back             Review details │
│ Check before planning              │
│                                  │
│ Arrival airport                    │
│ Frankfurt Airport       Confirmed │
│                                  │
│ Train                              │
│ ICE 1234 · 16:08                  │
│ [ From your ticket ]               │
│                                  │
│ Arrival station                    │
│ Heidelberg Hbf      Needs review › │
│                                  │
│ Coach / seat                       │
│ 22 / 134             From ticket  │
│                                  │
│ [ Edit details ]   [ Confirm plan ]│
└──────────────────────────────────┘
```

**Status language:** “From your ticket,” “Scheduled,” “Live estimate,” and “Needs review” are never merged into a single generic badge.

## 5. Journey overview — compare booked and suggested legs

```text
┌──────────────────────────────────┐
│ Frankfurt Airport → Boxberg        │
│ Last checked: 14:05 · Scheduled    │
│                                  │
│ 1  ARRIVAL                         │
│    Frankfurt Airport                │
│    Follow long-distance rail signs  │
│    [Official reference]             │
│        │ walk estimate              │
│ 2  BOOKED TRAIN                     │
│    Fernbahnhof → Heidelberg Hbf     │
│    ICE 1234 · Coach 22 · Seat 134   │
│    From your confirmed ticket       │
│        │ transfer buffer             │
│ 3  LOCAL CONNECTION                 │
│    Heidelberg Hbf → Boxberg         │
│    Route option — review details    │
│        │ final walk                  │
│ 4  DESTINATION                      │
│    Accommodation entrance            │
│    Address confirmed by you          │
│                                  │
│ [ Start travel guide ] [ Export PDF]│
└──────────────────────────────────┘
```

**Critical rule:** if the rail leg is not supplied in a ticket, label it “Recommended option,” show source/time, and require the traveller to choose it. Never label it booked.

## 6. Travel mode — current instruction first

```text
┌──────────────────────────────────┐
│ Frankfurt Airport                  │
│ Step 1 of 5                 [⋯]   │
│ ━━━━━━━━○━━━━━━━━━━━━━━━━━━━━━━  │
│                                  │
│ Find the long-distance train       │
│ station                            │
│                                  │
│ Follow signs saying                │
│ “Fernbahnhof” or                  │
│ “Long-distance trains”.            │
│                                  │
│ [ Official map / reference area ]  │
│ Caption: Look for this wording.     │
│                                  │
│ Check: find the departure board for│
│ your confirmed train.               │
│                                  │
│ Source: Fraport reference · checked│
│ 14:05 · station route may change   │
│                                  │
│ [ I found it ]                      │
│ [ I cannot find this place ]        │
│ [ View full journey ]               │
└──────────────────────────────────┘
```

The visual area can hold an authorised station diagram, map link preview, or clearly labelled illustration. It must never imply a generated image is a verified photograph.

## 7. Recovery state — no silent rerouting

```text
┌──────────────────────────────────┐
│ I cannot find the platform          │
│                                  │
│ First, check the live departure     │
│ board for your train number and     │
│ destination. Platform numbers can   │
│ change.                             │
│                                  │
│ Your guide has no live platform     │
│ update from an approved source.     │
│                                  │
│ [ Open station/departure link ]     │
│ [ Show ticket details ]             │
│ [ Ask travel assistant ]            │
│ [ Return to previous step ]         │
└──────────────────────────────────┘
```

## 8. Map/reference panel — recognise, don't guess

```text
┌──────────────────────────────────┐
│ ‹ Back          Reference         │
│ Fernbahnhof entrance               │
│                                  │
│ [ Authorised station diagram or   │
│   map preview, source-labelled ]  │
│                                  │
│ Caption: Look for this wording    │
│ and signage colour.                │
│                                  │
│ Source: Fraport wayfinding         │
│ reference · retrieved 14:05        │
│ Licence: attribution required      │
│                                  │
│ [ Open in external map/nav app ]   │
│ [ Close reference ]                │
└──────────────────────────────────┘
```

**Unavailable-source variant:**

```text
┌──────────────────────────────────┐
│ ‹ Back          Reference         │
│ No authorised reference             │
│                                  │
│ We do not have a permitted map,     │
│ diagram, or photo for this exact    │
│ spot yet.                           │
│                                  │
│ [ Open in external map/nav app ]    │
│ [ Close reference ]                 │
└──────────────────────────────────┘
```

**Illustrative-visual variant:** same layout, with a persistent "Illustration — not a photograph" label above the image and the caption explaining what it represents.

**Rule:** never render an image panel without one of: an authorised source line, an unavailable-source message, or an illustration label. The three states are mutually exclusive and never blended.

**Interaction:** a live map excerpt pans/zooms like a familiar map app; a diagram, photo, or illustration only pinch/tap-zooms for legibility, never pans into undrawn space — see the [design system's map interaction rules](design-system.md#map-and-reference-panel-interaction).

## 9. Trip assistant — sourced answers only

```text
┌──────────────────────────────────┐
│ ‹ Back          Trip assistant     │
│ Ask about this trip                 │
│                                  │
│ ┌──────────────────────────────┐ │
│ │ You: What platform does my    │ │
│ │ train leave from?             │ │
│ └──────────────────────────────┘ │
│ ┌──────────────────────────────┐ │
│ │ Assistant:                    │ │
│ │ Your ticket does not list a   │ │
│ │ platform. Check the departure │ │
│ │ board at Fernbahnhof for      │ │
│ │ ICE 1234 at 16:08.            │ │
│ │ Source: your confirmed ticket │ │
│ └──────────────────────────────┘ │
│                                  │
│ [ Ask a question...        ➤ ]    │
│                                  │
│ This assistant only answers from   │
│ your trip's confirmed and sourced  │
│ facts. It will say so when it       │
│ cannot answer.                      │
└──────────────────────────────────┘
```

**Essential states:** a sourced answer always names its fact/document origin; an unsupported question gets an explicit "I don't have a verified answer for that" response plus a pointer to the recovery sheet or an external official link — never a confident guess.

## 10. PDF preview / export

```text
┌──────────────────────────────────┐
│ ‹ Back          Export guide       │
│ Frankfurt Airport → Boxberg         │
│                                  │
│ Guide version: v3 · generated      │
│ 18 Oct, 14:05                      │
│                                  │
│ [ PDF preview thumbnail ]          │
│                                  │
│ Includes: journey timeline,        │
│ sources, freshness labels, and     │
│ one authorised reference image.    │
│                                  │
│ ⚠ Schedules and platforms may        │
│ change after this snapshot.        │
│ Recheck before you travel.          │
│                                  │
│ [ Download PDF ]  [ Share link ]   │
└──────────────────────────────────┘
```

**Generating / failure variants:** replace the preview with a progress indicator ("Preparing your guide…") or a failure message ("We could not generate the PDF. Your reviewed journey is unchanged — try again or export later.") The primary actions stay disabled until a valid snapshot exists.

## 11. Settings — privacy and control

```text
┌──────────────────────────────────┐
│ ‹ Back            Settings         │
│                                  │
│ LANGUAGE                            │
│ [ English ▾ ]                       │
│                                  │
│ PRIVACY AND DATA                    │
│ Retention: documents auto-delete    │
│ [ retention period — pending     ] │
│ [ Download my data ]                │
│ [ Delete this trip and documents ]  │
│                                  │
│ NOTIFICATIONS                       │
│ [ ] Trip reminders                  │
│ [ ] Live-data alerts (unavailable   │
│     until a provider is approved)   │
│                                  │
│ LOCATION                            │
│ Location access: Not requested      │
│ [ About location use ]              │
└──────────────────────────────────┘
```

**Rule:** the retention period shown here must match the approved retention decision; do not display a specific duration until that P0 decision is resolved. Deletion actions require a confirmation step and show their result (success/failure), never a silent no-op.

## 12. Desktop journey workspace

```text
┌──────────────┬──────────────────────────────┬────────────────────┐
│ My trips     │ Frankfurt Airport → Boxberg   │ Current instruction│
│              │ Timeline / map / sources      │ Find Fernbahnhof   │
│ • Trip       │                              │                     │
│ • Documents  │ [Journey timeline]            │ [Reference/map]    │
│ • Guide      │                              │ [Complete step]    │
│ • Export     │ [Open in external maps]       │ [Need help]        │
└──────────────┴──────────────────────────────┴────────────────────┘
```

Desktop aids planning and review. During travel, the responsive layout collapses to the focused current-step view.
