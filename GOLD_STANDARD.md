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
- [ ] `<header class="workbook-header">` — warm gold gradient: `linear-gradient(135deg, #ffffff, #fff8e6)`, border `#e8dbbf`
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
- [ ] `wsReset()` function: clears inputs, removes `.ws-correct`/`.ws-wrong`, clears score display
- [ ] Open-ended `<textarea class="written-area">` elements are NOT scored (excluded from `wsCheckAll`)
- [ ] `.ws-score-bar` hidden on print via `@media print`

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

---

## Known Issues — Modules 01–09 (as of 2026-05-18)

| # | File | Issue | Status |
|---|---|---|---|
| 01 | workbook | Header uses blue `#eef3ff` gradient instead of warm gold `#fff8e6` | Open |
| 02 | tutorial | No interactive widget | Open |
| 03 | tutorial | No interactive widget | Open |
| 03 | — | No notebook | Open |
| 05 | tutorial | No interactive widget | Open |
| 06 | tutorial | No interactive widget | Open |
| 07 | tutorial | No interactive widget | Open |
| 06 | tutorial | Learning objectives missing | **Fixed 2026-05-18** |
| 07 | tutorial | Learning objectives missing | **Fixed 2026-05-18** |
| 09 | tutorial | Learning objectives missing | **Fixed 2026-05-18** |
| 06–09 | worksheets | Used `workbook-header` class instead of `worksheet-header` (wrong color scheme) | **Fixed 2026-05-18** |

---

## Module Completion Tracker

| Module | Tutorial | Practice | Worksheet | Notebook | Slides | Podcast | Video | Infographic |
|---|---|---|---|---|---|---|---|---|
| 01 | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 02 | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 03 | ✓ | ✓ | ✓ | ✗ | ✓ | ✓ | ✓ | ✓ |
| 04 | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 05 | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 06 | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 07 | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 08 | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 09 | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| 10–76 | ✓ | old | ✗ | ✗ | ✗ | ✗ | ✗ | ✗ |
