# Data Readiness Canvas

A lightweight, self-serve toolkit that helps a company figure out **which parts of the business actually need a Data Analyst — and which don't.**

It started as a workshop exercise for a talk on data-driven decision making, built to answer one practical question that keeps coming up whenever "should we hire a Data Analyst?" is discussed:

> Is hiring a Data Analyst a cost, or is *not* having one the real cost?

Instead of leaving that as an abstract debate, this toolkit turns it into a 10-minute, fill-in-the-boxes exercise that produces a personalized, evidence-based read on a company's data maturity.

---

## What's in here

| File | What it is |
|---|---|
| `Data_Needs_Canvas.docx` | A one-page, checkbox-only self-assessment (a stripped-down Business Model Canvas, but focused on data). |
| `result_card_tool.html` | A single-file, offline, in-browser tool that reads the filled-in canvas and generates a personalized result card. |

No installation, no backend, no data leaving the browser — everything runs client-side.

---

## How it works

**1. Fill out the canvas**

The canvas covers 6 business functions — Marketing, Sales, Product, Finance, Operations, Management. For each one, you tick two boxes:

- **Current state** — are decisions here made from data, a mix of data and gut feeling, or mostly guesswork?
- **Importance** — how much does this area affect business growth right now (Low / Medium / High)?

That's it. No typing required, no jargon, written so that someone without a technical background (e.g. an HR or business generalist) can fill it out unassisted.

**2. Upload it to the result tool**

Open `result_card_tool.html` in any browser (or host it as a static page) and upload the completed `.docx`. It's parsed entirely client-side — nothing is uploaded to a server.

**3. Get a personalized result card**

The tool scores every function as *(data gap) × (importance)*, and generates:

- The **single business area** most in need of better data support, with a short, concrete example of what tends to go wrong there and what improves once it's fixed.
- A **Data Capability Maturity level (1–4)**, from "your current setup is fine" to "this needs a dedicated data team," with a recommended next move — *Upskill*, *Start Small*, *Hire*, or *Scale*.
- A **cost vs. impact comparison**, if the company chooses to go deeper: rough monthly cost of a Data Analyst vs. self-estimated monthly impact of solving the priority gap.
- A map of all 6 areas side by side, so the takeaway isn't just "your worst area," but the full picture.

Every submission gets the same structure and depth of insight, regardless of company size or whether it's reviewed live by anyone — it's meant to work as a standalone artifact, not just a workshop prop.

---

## Design principles

- **Position-based scoring, not keyword-matching.** The scoring logic reads *which checkbox* was ticked (1st, 2nd, or 3rd option), never the wording of the option itself. This was a deliberate choice: keyword-matching against phrases like "assumption-based" or "gut feeling" is fragile, easy to break when copy changes, and easy to (accidentally or not) tilt toward a predetermined conclusion. Reading position instead of wording keeps the result honest and reproducible.
- **No inflated defaults.** If an answer can't be confidently parsed, the tool skips it rather than assuming the worst case just to push a stronger recommendation.
- **Plain language over jargon.** The canvas avoids technical terms (no "CTR," "churn," "pipeline," etc.) so it's usable by non-technical stakeholders, not just data people.
- **Self-contained.** The result tool is a single HTML file with no server dependency — easy to host anywhere or even open locally.

---

## Tech notes

- The canvas uses native Word checkbox content controls (`w:sdt` / `w14:checkbox`), which some naive `.docx`-to-text libraries fail to read correctly (they only see the surrounding text, not the checkbox glyph itself). `result_card_tool.html` reads the raw `word/document.xml` inside the `.docx` archive directly (via [JSZip](https://github.com/Stuk/jszip) + `DOMParser`) to avoid that failure mode.
- No build step, no dependencies beyond a CDN-loaded JSZip. Everything else is vanilla HTML/CSS/JS.

---

## Status / disclaimer

This is a **practical decision-support tool, not a scientific ROI calculator.** It's meant to turn a vague "do we need a Data Analyst?" conversation into a structured, evidence-based one — not to produce a definitive financial verdict. Treat the output as a starting point for discussion, not a final answer.

Built for an internal use case and open-sourced in a generalized form. Contributions, forks, and adaptations for other contexts (e.g. different function names, different maturity frameworks) are welcome.

---

## License

MIT — use it, adapt it, ship it.
