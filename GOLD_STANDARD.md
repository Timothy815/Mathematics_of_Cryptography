# Module Gold Standard Checklist

This file defines the required structure and quality bar for every module in the Mathematics of Cryptography curriculum. Check every item before marking a module complete.

---

## Tutorial (`tutorial_##_<slug>_html.html`)

### Head
- [ ] `<title>` format: `"<Module Title> | Mathematics of Cryptography"`
- [ ] MathJax config block + CDN script (`cdn.jsdelivr.net/npm/mathjax@3/es5/tex-svg.js`)
- [ ] `<link rel="stylesheet" href="css/style.css">`
- [ ] Inline `<style>` for module-specific overrides (never edit `css/style.css`)

### Header
- [ ] `<header class="tutorial-header">`
- [ ] `.course-label`: `"Mathematics of Cryptography · Tutorial ##"`
- [ ] `.volume-label`: correct volume string
- [ ] `<h1>` title
- [ ] `<p class="subtitle">` — one sentence summary
- [ ] Top `<nav class="tutorial-nav no-print">` containing:
  - [ ] `← Module ##` prev link (href to previous tutorial file)
  - [ ] `🏠 Dashboard` link (href="index.html")
  - [ ] `Module ## →` next link (href to next tutorial file)
  - [ ] Print button (`onclick="window.print()"`)

### Required Sections (in order)
- [ ] `#why-this-tutorial-exists` — purpose box with `.box.purpose-box`
- [ ] `#learning-objectives` — `.box.purpose-box` with "After completing this module you will be able to" + bulleted list of 4–6 outcomes
- [ ] `#what-you-should-know-first` — prerequisites in plain English
- [ ] `#symbols-used` — table with columns: Symbol | Friendly meaning | Technical meaning
- [ ] `#big-idea` — `.box.intuition-box` leading into content
- [ ] *(content sections — module specific)*
- [ ] `#common-mistakes` — 3–5 `.box.mistake-box` blocks
- [ ] `#practice` — numbered `<ol class="practice-list">` with 5–6 problems, each wrapped in `<details class="solution"><summary>Show solution</summary>…</details>`
- [ ] `#cryptography-connection` — explains how this module feeds into AES/RSA/etc.
- [ ] `#one-page-recap` — `.box.recap-box` bullet list of key facts + summary table or examples
- [ ] `#next` — one paragraph pointing to the next module by name and number

### Interactive Widget
- [ ] At least one interactive exploration section where computationally appropriate (label with `class="no-print"` so it is hidden on print)
- [ ] Widget uses only vanilla JS (no external libraries beyond MathJax)
- [ ] Reset / preset buttons provided
- [ ] **AI Tutor escalation:** After 2+ wrong attempts on any widget check, an inline escalation card appears containing:
  - A dynamically-generated contextual prompt naming the module, topic, and specific step (include "without giving me the answer directly, ask me questions to help me figure it out")
  - A **Copy prompt** button (uses `navigator.clipboard.writeText`)
  - An **Ask AI Tutor →** link (indigo `#4338ca`) opening the module's Gemini gem in a new tab
  - CSS classes: `.tutor-escalate`, `.tutor-escalate-prompt`, `.tutor-escalate-actions`, `.tutor-esc-copy`, `.tutor-esc-link`

### Footer
- [ ] `<p class="footer-note">` attribution line
- [ ] `<nav class="bottom-nav no-print">` containing:
  - [ ] Left bundle: prev link, Dashboard link, next link
  - [ ] Right bundle: "Switch to Workbook" link

### Print / CSS
- [ ] `@media print` block hides `.no-print` and `.tutorial-nav`
- [ ] `.no-print` applied to both top and bottom navs and any interactive widget sections

---

## Practice / Workbook (`tutorial_##_<slug>_workbook_html.html`)

### Head & Header
- [ ] `<title>` format: `"Practice ##: <Module Title> | Mathematics of Cryptography"`
- [ ] `<header class="workbook-header">` — warm gold gradient: `linear-gradient(135deg, #fffdf4, #fdf3d0)`, border `#e8dbbf`
- [ ] `.course-label`: `"Mathematics of Cryptography · Practice ##"`
- [ ] `.volume-label`
- [ ] `<h1>` title
- [ ] `<p class="subtitle">` listing the four drills

### Navigation
- [ ] `<nav class="workbook-nav no-print">` with:
  - [ ] Jump links to each drill section (`#d1-sec` … `#d4-sec`)
  - [ ] `🏠 Dashboard` link (margin-left: auto to push right)
  - [ ] Print button

### Quick Reference
- [ ] `<details class="quick-ref no-print">` collapsible card
- [ ] `.qr-grid` containing 3–4 `.qr-card` blocks covering key formulas and examples

### Drill Sections (exactly 4)
Each drill section must have:
- [ ] `<section class="drill-section" id="d#-sec">`
- [ ] `<h2>Drill # — Description</h2>`
- [ ] `<div class="drill-card">` containing:
  - [ ] `<div class="drill-q" id="d#-q">Loading…</div>`
  - [ ] `<div class="drill-hint">` — one-sentence guidance
  - [ ] `.drill-row` with input or YES/NO buttons + Check + Next→ buttons
  - [ ] `<div class="drill-fb" id="d#-fb"></div>` feedback area
  - [ ] `<div class="drill-streak" id="d#-streak"></div>`

### JavaScript
- [ ] `makeDrill(cfg)` engine function present
- [ ] All questions randomly generated via `Math.random()` — infinite practice
- [ ] Correct answers show ✓ feedback + `.drill-fb.ok` (green)
- [ ] Wrong answers show ✗ feedback with explanation + `.drill-fb.err` (red)
- [ ] Input turns green/red via `.correct` / `.wrong` class
- [ ] Enter key triggers check
- [ ] MathJax call uses `typeof` guard: `if (window.MathJax && typeof MathJax.typesetPromise === 'function')` — the config object is set before the library loads, so a bare `if (window.MathJax)` check will be truthy but `typesetPromise` won't exist, throwing a TypeError that stops all subsequent drill initialization
- [ ] **AI Tutor escalation** wired into `makeDrill`:
  - `cfg.gemUrl` — URL of the module's Gemini gem
  - `cfg.topic` — plain-English description of what this drill practises (e.g. `"converting decimal numbers to 8-bit binary"`)
  - `wrongStreak` counter inside the closure, reset to 0 on `next()` and on correct answer
  - After 2 consecutive wrong answers: `buildEscalationCard()` appended to feedback innerHTML
  - Escalation card prompt template: *"I'm working through [topic] in the Mathematics of Cryptography course. I keep getting the wrong answer on this drill. Can you help me understand where my thinking is going wrong, without giving me the direct answer? Please ask me questions to help me figure it out."*
  - Global helper `window._copyEscPrompt(id)` handles clipboard copy + button label flash
  - CSS: `.drill-escalate`, `.drill-escalate-prompt`, `.drill-escalate-actions`, `.drill-esc-copy`, `.drill-esc-link`

### Bottom Nav
- [ ] Left bundle: `← Practice ##`, `🏠 Dashboard`, `Practice ## →`
- [ ] Right bundle: `Tutorial ##` link, `Worksheet` link

### Print
- [ ] `@page { margin: 0.75in; }` — must be OUTSIDE `@media print`
- [ ] `.drill-section` hidden on print; `.quick-ref` forced open on print

---

## Worksheet (`worksheet_##_<slug>_html.html`)

### Head & Header
- [ ] `<title>` format: `"Worksheet ##: <Module Title> | Mathematics of Cryptography"`
- [ ] `<header class="worksheet-header">` — green gradient: `linear-gradient(135deg, #ffffff, #e8f4ef)`, border `#b2d4c4`
- [ ] `.course-label`: `"Mathematics of Cryptography · Worksheet ##"`
- [ ] `.volume-label`
- [ ] `<h1>` title
- [ ] `<p class="subtitle">`

### Navigation & Student Info
- [ ] `<nav class="workbook-nav no-print">` with jump links to each part + Dashboard + Print
- [ ] `.student-info` with Name and Date `.field-input` fields

### Quick Reference
- [ ] Collapsible `<details>` block with key formulas for the module

### Parts
- [ ] Parts A–H (or as many as content warrants), each with `id="part-#"`
- [ ] Short answers use `<input class="ans-input">` inline
- [ ] Working space uses `<div class="work-space">`
- [ ] Written responses use `<div class="write-wrap"><textarea class="written-area"></textarea><span class="write-lines">…</span></div>`

### Check / Score / Regenerate (browser mode)
- [ ] CSS block includes `.ws-score-bar`, `.ws-btn-check/regen/reset`, `.ans-input.ws-correct/wrong` rules
- [ ] Score bar `<div class="ws-score-bar no-print" id="ws-score-bar">` inserted before first `<section>` in `<main>`
- [ ] Score bar contains: descriptive `<p>`, `<span id="ws-score-display">`, Check / Regenerate / Reset `<button>` elements
- [ ] Every fill-in `<input class="ans-input">` carries `data-answer="val1|val2"` (pipe-separated for alternate formats)
- [ ] `wsCheckAll()` function: reads all `[data-answer]` inputs, normalizes, marks `.ws-correct` / `.ws-wrong`, updates score display
- [ ] `wsRegenerate()` function: generates new random values, updates question HTML, updates `data-answer` attributes
- [ ] `wsReset()` function: clears inputs, removes `.ws-correct`/`.ws-wrong`, clears score display, removes all `.ws-escalate` cards
- [ ] Open-ended `<textarea class="written-area">` elements are NOT scored (excluded from `wsCheckAll`)
- [ ] `.ws-score-bar` hidden on print via `@media print`
- [ ] **AI Tutor escalation (per section):**
  - Each scorable `<section>` in `<main>` carries `data-topic="..."` — a plain-English phrase describing what that section tests (e.g. `"running the Euclidean algorithm step by step"`)
  - Script declares `var WS_GEM_URL = 'https://gemini.google.com/gem/...'` at top of the scoring IIFE
  - After `wsCheckAll()` scores, for each section with ≥1 `.ws-wrong` input: append a `.ws-escalate` card (if not already present) at the bottom of that section
  - Escalation card prompt template: *"I'm working on [section topic] in the [Module Title] worksheet (Module ##, Mathematics of Cryptography). I've checked my answers and some are wrong. Can you help me understand where my reasoning is breaking down, without giving me the answers directly? Please ask me guiding questions."*
  - Card contains: prompt text div, Copy prompt button, Ask AI Tutor link to `WS_GEM_URL`
  - `wsReset()` removes all `.ws-escalate` cards
  - CSS: `.ws-escalate`, `.ws-escalate-prompt`, `.ws-escalate-actions`, `.ws-esc-copy`, `.ws-esc-link` — hidden on print

### Answer Key
- [ ] `<section id="answer-key" class="answer-key">` at the bottom
- [ ] Complete answers for every question using `.answer-step` divs

### Bottom Nav
- [ ] Left bundle: `← Worksheet ##`, `🏠 Dashboard`, `Worksheet ## →`
- [ ] Right bundle: `Tutorial ##` link, `Practice ##` link

### Print
- [ ] `@page { margin: 0.75in; }` OUTSIDE `@media print` (not inside it)
- [ ] `.written-area` hidden on print; `.write-lines` displayed on print
- [ ] `.wl` spans render as ruled lines (`height: 1.9em; border-bottom: 1px solid #888`)
- [ ] `.ans-input` renders as underline only (no background, no border-radius) on print
- [ ] JavaScript generates `.wl` spans inside each `.write-lines` container

---

## Notebook (`notebook_##_<slug>.ipynb`)

- [ ] Filename: `notebook_##_<slug>.ipynb` (NOT `tutorial_##_…_notebook.ipynb`)
- [ ] ~10 cells/sections
- [ ] Section 1: markdown intro with module title, volume, and section list
- [ ] Sections 2–9: alternating markdown explanations + runnable Python code cells
- [ ] Pure Python — no pip installs, no external dependencies beyond stdlib
- [ ] At least one interactive exploration function (e.g. an explorer that accepts arguments)
- [ ] Verification cell: proves a key property holds for all inputs (e.g. all 256 bytes)
- [ ] Section 10: summary table (markdown) + bridge to next module

---

## Dashboard Card (`index.html`)

For a fully produced module the card should contain, in this order:

- [ ] `<a class="card-img-link" href="tutorial_##_…_html.html"><img class="card-img" src="tutorial##.png" alt="Module ## infographic" /></a>` — infographic as clickable image (add only when file exists)
- [ ] Module number + title `<div>`
- [ ] `<div class="module-links">` containing (in order, add only when file exists):
  - [ ] Tutorial button — `btn-tutorial` (blue)
  - [ ] Practice button — `btn-workbook` (gold)
  - [ ] Worksheet button — `btn-worksheet` (dark green `#2a6049`)
  - [ ] Slides button — `btn-slides` (purple `#614b82`), `target="_blank"`
  - [ ] Podcast button — `btn-podcast` (rust `#b5451b`), `target="_blank"`
  - [ ] Video button — `btn-video` (dark navy `#1a1a2e`), `target="_blank"`
  - [ ] Notebook button — `btn-notebook` (teal `#0d6e6e`), `download` attribute
  - [ ] AI Tutor button — `btn-gem` (indigo `#4338ca`), `target="_blank"`, links to module's Gemini Gem

---

## Known Issues — Open as of 2026-05-23

| # | File | Issue | Status |
|---|---|---|---|
| 02 | tutorial | No step-through interactive widget (only bit-flipper in workbook) | Open — low priority |
| 03 | — | No notebook | **Intentional** — topic does not benefit from computation |
| 03 | tutorial | No interactive widget | Open — low priority |
| 05 | tutorial | No interactive widget | Open — low priority |
| 06 | tutorial | No interactive widget | Open — low priority |
| 07 | tutorial | No interactive widget | Open — low priority |
| 15+ | all | Not yet brought to gold standard | **Next focus** |

### Recently Fixed (2026-05-23)
- All workbook header gradients updated to `#fffdf4, #fdf3d0` (Modules 01–11)
- Course labels corrected to "Practice N" (Modules 01–04)
- All workbook aria-labels standardised to "Practice navigation" (Modules 01–10)
- Top nav prev/next links added to Modules 01–05, 09
- Print button added to Module 12 top nav
- Broken Practice 15 link fixed in Module 14 workbook
- Infographic sections added to Module 13 and 14 tutorials
- Module 08 AES connection section: added 6-module road map table and `0x57 × 0x83 = 0xC1` payoff preview
- Module 09: added AddRoundKey concrete example and multiplication-degree teaser in "What comes next"

---

## Module Completion Tracker — as of 2026-05-23

**Gold standard practice** = `makeDrill()` engine + gold gradient + `drill-section/card/q/fb/streak` CSS + `aria-label="Practice navigation"`
*Module 02 practice is a justified exception: uses a custom interactive bit-flipper widget that is pedagogically superior to a text-input drill for this topic.*

| Module | Tutorial | Practice | Worksheet | Notebook | Slides | Podcast | Video | Infographic |
|---|---|---|---|---|---|---|---|---|
| 01 | ✓ gold | ✓ gold | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 02 | ✓ gold | ✓ gold* | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 03 | ✓ gold | ✓ gold | ✓ | ✗ intentional | ✓ | ✓ | ✓ | ✓ |
| 04 | ✓ gold | ✓ gold | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 05 | ✓ gold | ✓ gold | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 06 | ✓ gold | ✓ gold | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 07 | ✓ gold | ✓ gold | ✓ | ✓ | ✓ | ✓ | ✓ ×2 | ✓ |
| 08 | ✓ gold | ✓ gold | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 09 | ✓ gold | ✓ gold | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 10 | ✓ gold | ✓ gold | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 11 | ✓ gold | ✓ gold | ✓ | ✓ | ✓ | ✓ | ✓ ×2 | ✓ |
| 12 | ✓ gold | ✓ gold | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 13 | ✓ gold | ✓ gold | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 14 | ✓ gold | ✓ gold | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 15 | ✓ gold | ✓ gold | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 16–76 | ✓ (varies) | old format | ✗ | ✗ | ✗ | ✗ | ✗ | varies |
