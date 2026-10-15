# Product requirements document

## 1. Product summary

**Working name:** AI Travel Companion
**Vision:** Help a traveller confidently complete an unfamiliar journey by converting their confirmed booking information and trustworthy location/transport data into a verified, visual, step-by-step guide.

The product is not another generic map or route search engine. Its differentiator is the bridge between a traveller's booking and the real-world actions required to execute it: finding the correct entrance, reading a departure board, identifying a vehicle, changing at a station, and recovering when information changes.

## 2. Problem and opportunity

First-time international travellers can receive technically valid route results but still not know what to do in a large airport, station, or transit network. Relevant facts are fragmented across ticket PDFs, operator sites, maps, signs, accommodation messages, and changing service notices. The product reduces this interpretation burden without claiming more certainty than its sources justify.

## 3. Target users and jobs

| User | Context | Primary job |
| --- | --- | --- |
| International student | Arriving alone in a new country with luggage and time pressure | Get from arrival point to accommodation without misunderstanding the transport system. |
| First-time international traveller | Unfamiliar language, signage, ticket rules, and transfers | Know what to look for and which action to take next. |
| Tourist using public transport | Needs simple guidance, not timetable interpretation | Follow a reliable plan and recover when a step goes wrong. |
| Accessibility- or luggage-conscious traveller | Walking, stairs, and transfer buffers matter | Choose and understand a route compatible with stated needs. |

**Primary job to be done:** “When I have a booking and need to travel through an unfamiliar place, help me understand exactly what to do next and how to tell that I am in the right place.”

## 4. Product principles

1. **Facts before fluency.** Structured, sourced journey facts drive instructions; AI makes them understandable.
2. **Confirm ambiguity.** Do not guess when a document contains an ambiguous station, date, airport, passenger route, or destination.
3. **State uncertainty.** Booking-confirmed, scheduled, live-estimated, unverified, conflicting, and expired information must look different.
4. **One action at a time.** Travel mode focuses on a single current step while preserving access to the full plan.
5. **Useful without a connection.** A downloaded guide remains readable, but clearly labels information that needs a live recheck.
6. **Respect the traveller.** Minimise data collection, do not overstate reliability, and make source attribution visible.

## 5. MVP boundary

### In scope

- One approved launch geography and one representative airport/station-to-destination corridor.
- Account creation and private trip management.
- PDF, JPEG, and PNG ticket/itinerary upload subject to approved file limits and processing capability; manual entry as a fallback.
- OCR/extraction candidate display, confidence cues, and mandatory user correction/confirmation of important journey facts.
- One final destination address and a multi-leg public-transport route from the confirmed arrival/departure point.
- Journey overview plus a mobile-first, step-by-step guide.
- Authorised map links and a limited set of authorised, attributed visual references or official diagrams.
- Source, verification, and freshness labels for important facts.
- A mobile-readable PDF export and an offline-accessible saved guide snapshot.
- Honest empty, error, unavailable-data, and “I cannot find this place” recovery states.

### Explicitly out of scope for MVP

- Global transport coverage or a promise of indoor guidance at every station.
- Guaranteed live monitoring, automatic rebooking, ticket purchasing, payments, or autonomous travel actions.
- Continuous background location tracking, voice navigation, camera/image matching, or computer-vision wayfinding.
- Unlicensed map imagery, scraped provider content, or generated visuals presented as real-world photographs.
- Advice that replaces emergency services, transport staff, immigration requirements, or ticket-provider support.

## 6. Core functional requirements

### Trip and document management

- Create, edit, duplicate, and delete a trip.
- Upload supported documents through a private, validated pipeline and retain a document provenance record.
- Extract candidate fields: date/time, origin/destination, service number, reservation/coach/seat, and booking reference only when required.
- Highlight conflicts and low-confidence/ambiguous values; let the traveller edit and confirm them.
- Support several documents and preserve the relationship between a ticket and a separate seat reservation.

### Route planning and location resolution

- Resolve exact airports, stations, stops, terminal/entrance references, and destination addresses using approved provider IDs.
- Build an ordered itinerary of walking and transport segments from confirmed data plus selected provider results.
- Respect stated preferences such as walking tolerance, accessibility requirements, luggage, budget, and fewer transfers where provider data supports them.
- Preserve ticket-bound legs and expose recommended alternatives separately.
- Warn about tight connections using documented buffer assumptions; do not call a connection safe when necessary data is absent.

### Guide generation and travel mode

- Generate brief, language-appropriate steps from a versioned, verified journey model.
- For each step: state the starting point, action, recognisable sign/landmark/vehicle, duration where available, success check, next action, and fact status.
- Offer a full timeline, step-by-step mode, map/deep links, ticket details, progress controls, and a lost/recovery path.
- Answer trip-specific questions only from authorised trip context and approved sources; provide a clear limitation when information is unavailable.

### Export and refresh

- Render the approved journey version into a mobile-friendly PDF with source attribution, retrieval timestamps, map links, and data-freshness warnings.
- Preserve a downloadable guide snapshot for offline reading and provide an explicit refresh action before travel.

## 7. Initial acceptance criteria

An MVP prototype is ready for user validation when a test traveller can:

1. Upload a representative ticket or manually enter the same details.
2. Correct/confirm every critical extracted field before route planning.
3. See the route as distinct, sourced journey segments rather than free-form AI text.
4. Follow each instruction and identify the source and freshness of important facts.
5. Open an authorised external map/navigation link when desired.
6. Export a PDF that matches the reviewed journey version and labels volatile data.
7. Understand what to do when a platform, live time, photo, or route result is unavailable.
8. Delete the test trip and its uploaded document according to the approved retention policy.

## 8. Success measures to baseline during prototype

Do not publish target numbers before a pilot establishes a baseline. Measure:

- Completion rate for a scripted document-to-guide journey.
- Critical extraction correction rate, by field and document quality.
- Correct source/provenance attachment rate for critical instructions.
- Guide comprehension and confidence in moderated usability sessions.
- Provider failure rate, route response latency, guide/PDF generation latency, and per-trip cost.
- Accessibility defects and offline-guide availability in realistic low-connectivity tests.

## 9. Assumptions requiring validation

- A launch geography exists with lawful route, map, visual-reference, and at least scheduled transit data.
- Users will review extracted booking details before relying on the guide.
- The selected provider licence permits the intended in-app and PDF use, attribution, caching, and retention.
- Visual content can be supplied lawfully and accurately enough to add value beyond a map link.
