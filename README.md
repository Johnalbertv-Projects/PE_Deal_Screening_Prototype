# PE Deal Screening Prototype

**Live site:** https://johnalbertv-projects.github.io/PE_Deal_Screening_Prototype/

A browser-based prototype for preliminary private-equity deal screening. Upload a text-based deal PDF; the page extracts key facts, lets you review and correct them, and screens them against six investment criteria.

> Independent synthetic learning prototype. No real company or client data. Results support preliminary screening only; investment decisions remain with human investors.

## How it works

1. **Upload:** Drop a PDF. It is read entirely in your browser with Mozilla PDF.js and is never uploaded.
2. **Extract:** Simple, explainable text patterns identify company, sector, geography, revenue, EBITDA, and ownership language, each linked to the page and sentence it came from.
3. **Review:** Correct any extracted value. Corrections are marked and exist only in your browser tab.
4. **Screen:** Deterministic rules rate each criterion **Met**, **Not met**, or **Insufficient information**.
5. **Human review:** Missing or unclear facts become diligence questions, never failures.

## Screening criteria

| Criterion | Standard |
|---|---|
| Sector | Business-to-business software and technology-enabled business services |
| Geography | Primarily United States and Canada |
| Annual revenue | $20 million to $80 million |
| Profitability | Positive EBITDA |
| Growth | At least 10% year-over-year revenue growth |
| Ownership | A controlling or majority investment must be possible |

## Design principles

- **Missing ≠ Not met.** If a fact is missing or ambiguous, the result is Insufficient information.
- **Traceable.** Every extracted value shows its source text and page.
- **No overall verdict.** Each criterion is reported separately; there is no score or recommendation.
- **Private by design.** No backend, no API, no data storage. The only external resource is the PDF.js library from jsDelivr.

## Limitations

Supports text-based PDFs only (scanned PDFs would need OCR). Extraction uses pattern matching, not general AI document understanding, so review every value.

## Tech

Single static `index.html` (HTML, CSS, vanilla JavaScript) hosted on GitHub Pages.
