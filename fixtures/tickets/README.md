# Simulated ticket fixtures — Frankfurt pilot

**All content in this folder is fictional.** No real traveller, booking, PNR, or payment data. Names, reference codes, and seat numbers are invented for testing only. Every fixture carries a `SAMPLE / SIMULATED` banner; the application must preserve that label through extraction and review, per [design-system.md's content rules](../../docs/design/design-system.md#content-rules).

## Why these exist

[DEC-001](../../docs/decisions/DEC-001-frankfurt-pilot-baseline.md) leaves "real vs. simulated prototype data" as an open approval item, and the product owner has chosen simulated fixtures for now rather than real/de-identified tickets. These files are the resulting test corpus for document-extraction and review-flow testing, standing in for the roadmap's "collect a consented, representative test corpus" item until/unless real documents are later approved.

Each fixture is plain text representing what a born-digital PDF's text layer would contain — matching the first OCR/extraction option in [options-and-costs.md](../../docs/research/options-and-costs.md) ("native PDF text extraction + manual confirmation"). They are not rendered PDFs or images; a future prototype would still need to exercise actual file upload, scanning, and OCR against real file formats, not just this text.

## Fixtures and the scenario each exercises

| File | Scenario (from [validation-plan.md](../../docs/plan/validation-plan.md)) | What it's for |
| --- | --- | --- |
| `01-ice-ticket-clear.txt` | Clear flight/train ticket | Happy-path extraction: date, service, coach/seat, origin/destination all present and unambiguous. |
| `02-seat-reservation-companion.txt` | Separate ticket and seat reservation | A reservation issued separately from `01`, same booking reference — tests that the two are linked, not merged or duplicated. |
| `03-ice-ticket-degraded-ocr.txt` | Blurry screenshot or partial document | Simulates noisy OCR output (missing/garbled characters) on the platform and coach fields — must trigger low-confidence/needs-review, never a silent guess. |
| `04-ice-ticket-ambiguous-destination.txt` | Similarly named stations | Destination printed as plain "Heidelberg" without a station suffix — there is more than one Heidelberg stop; extraction must not silently default to Hbf. |
| `05-flight-arrival-confirmation.txt` | Clear flight/train ticket (arrival leg) | The inbound flight into Frankfurt Airport that starts the journey, feeding the arrival-time field in trip setup. |

## Using these

Treat each file's content as the "document text" a `DocumentExtractionProvider` adapter would receive — feed it to extraction-candidate logic and verify the resulting `ExtractedBooking` fields, confidence, and evidence match what the scenario calls for. Do not rename these into anything suggesting they are real, and do not substitute real ticket content into these filenames later — add new, clearly named fixtures instead.
