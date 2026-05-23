# Mathematics of Cryptography — Agent Context File

This file is the authoritative context document for all AI agents (Claude Code, Gemini, Codex, and others) working in this repository. Read it before making any changes.

---

## What This Project Is

A static HTML curriculum of **76 self-contained educational modules** on the mathematics of cryptography — from binary foundations through lattice-based post-quantum cryptography. There is no build system, no package manager, no server. All files open directly in a browser and are deployed via GitHub Pages.

**Live site:** served from `main` branch via GitHub Pages.
**Repository owner:** Timothy815

---

## File Naming Convention

| File type | Pattern | Example |
|---|---|---|
| Tutorial | `tutorial_##_<slug>_html.html` | `tutorial_12_multiplication_in_gf_2_8_html.html` |
| Practice (workbook) | `tutorial_##_<slug>_workbook_html.html` | `tutorial_12_multiplication_in_gf_2_8_workbook_html.html` |
| Worksheet | `worksheet_##_<slug>_html.html` | `worksheet_12_multiplication_in_gf_2_8_html.html` |
| Notebook | `notebook_##_<slug>.ipynb` | `notebook_12_multiplication_in_gf_2_8.ipynb` |
| Infographic | `tutorial##.png` | `tutorial12.png` |
| Slides | `tutorial##.pdf` | `tutorial12.pdf` |
| Podcast | `tutorial##.m4a` | `tutorial12.m4a` |
| Video | `tutorial##.mp4` | `tutorial12.mp4` |

`##` is always zero-padded (01, 09, 12, 76). The slug is lowercase with underscores.

---

## Architecture

```
/
├── index.html              # Dashboard — module card grid with search
├── css/style.css           # Shared design system (CSS custom properties)
├── CURRICULUM.md           # Authoritative 76-module list and volume structure
├── GOLD_STANDARD.md        # Per-file quality checklist + completion tracker
├── CLAUDE.md               # Claude Code specific instructions
├── GEMINI.md               # This file — shared agent context
└── tutorial_##_*           # 76 tutorials, practices, worksheets, notebooks
```

**No JavaScript framework.** All interactivity is vanilla JS inline in `<script>` tags. Math rendering uses MathJax 3 from CDN.

---

## Current Project Status — as of 2026-05-23

### Gold Standard Completion

Modules **01–14 are fully at gold standard**. See `GOLD_STANDARD.md` for the precise checklist and completion tracker.

**Next work focus: Module 15 and beyond.**

The pattern for bringing a module to gold standard is:
1. Bring tutorial to gold standard structure (nav, learning objectives, interactive widget, infographic section)
2. Rewrite practice/workbook to `makeDrill()` gold standard
3. Ensure infographic is featured in at least one content file (not just dashboard card)
4. Verify all dashboard card buttons are present

### Module 02 Practice — Justified Exception
Module 02's practice uses a custom bit-flipper widget rather than the `makeDrill()` engine. This is intentional — the interactive bit-level visualisation is pedagogically superior to a text-input drill for teaching XOR/AND/OR/shifts. Do not "fix" this.

### Module 03 Notebook — Intentional Omission
Module 03 (Functions as Machines) has no notebook. The topic does not benefit from computational exploration. Do not create one.

---

## Gold Standard Definitions

### Tutorial (`tutorial_##_<slug>_html.html`)
- Top nav: `← Module N`, `🏠 Dashboard`, `Module N →`, Print button
- Required sections in order: `#why-this-tutorial-exists`, `#learning-objectives`, `#what-you-should-know-first`, `#symbols-used`, `#big-idea`, *(content)*, `#common-mistakes`, `#practice`, `#cryptography-connection`, `#one-page-recap`, `#infographic`, `#next`
- At least one interactive widget (vanilla JS, `class="no-print"`)
- Bottom nav: prev / Dashboard / next + "Switch to Workbook"

### Practice (`tutorial_##_<slug>_workbook_html.html`)
- Header: `linear-gradient(135deg, #fffdf4, #fdf3d0)`, `border: 1px solid #e8dbbf`
- Course label: `"Mathematics of Cryptography · Practice ##"`
- `aria-label="Practice navigation"` on workbook nav
- Exactly 4 drills using `makeDrill()` engine
- CSS classes: `.drill-section`, `.drill-card`, `.drill-q`, `.drill-fb`, `.drill-streak`
- Bottom nav: `← Practice N`, Dashboard, `Practice N →` + Tutorial + Worksheet links
- MathJax guard: `if (window.MathJax && typeof MathJax.typesetPromise === 'function')`

### Worksheet (`worksheet_##_<slug>_html.html`)
- Green gradient header: `linear-gradient(135deg, #1a5c2a, #2a8a4a)`
- Dynamic random problems generated on load via `generateProblems()`
- Score bar with Check / Regenerate / Reset buttons
- `data-answer` attributes on all fill-in inputs
- Answer key section at bottom

### Dashboard Card (`index.html`)
Button order: Tutorial (blue) → Practice (gold) → Worksheet (dark green) → Slides (purple) → Podcast (rust) → Video (navy) → Notebook (teal)

---

## CSS Design System

All modules link to `css/style.css`. **Never edit `css/style.css` for module-specific styles** — use inline `<style>` blocks in each file's `<head>`.

Key CSS custom properties:
- `--accent`: `#334e7d` (primary blue)
- `--bg`: `#f7f5ef` (page background)
- `--paper`: `#ffffff` (card background)
- `--radius`: `18px`
- `--max-width`: `980px`
- `--gold-soft`, `--green-soft`, `--red-soft`, `--purple-soft`: semantic box backgrounds

Box classes: `.purpose-box`, `.intuition-box`, `.definition-box`, `.technical-box`, `.mistake-box`, `.recap-box`

---

## Key Technical Patterns

### GF(2⁸) Arithmetic (used in Modules 10–14)
```js
function xt(a)    { return (a << 1) & 0xFF ^ ((a & 0x80) ? 0x1B : 0); }
function gfm(a,b) { /* xtime chain */ }
function gfInv(a) { for (var b=1;b<256;b++) if (gfm(a,b)===1) return b; return 0; }
```

### AES S-box (Module 14)
- Stage 1: GF(2⁸) multiplicative inverse
- Stage 2: affine transformation `s_i = b_i ⊕ b_(i+4)%8 ⊕ b_(i+5)%8 ⊕ b_(i+6)%8 ⊕ b_(i+7)%8 ⊕ c_i`
- Constant `0x63 = [1,1,0,0,0,1,1,0]` (index 0 = LSB)

### Step-Through Bit-Grid Widget (Modules 10–14)
- 9-column grid (x⁸…x⁰), color-coded bit cells
- State variables: `giA`, `giInv`, `giChain[]`, `giStep` (prefix varies per module)
- Functions on `window`: `Start()`, `Next()`, `Reset()`, `Load(a)`
- Bit cell color semantics:
  - Orange: x⁸ being eliminated / contributing bit = 1
  - Yellow: XOR row / constant bit
  - Green: bit turned on by operation
  - Red: bit cancelled
  - Blue: unchanged 1
  - Grey: unchanged 0

### makeDrill() Engine (Practices 04–14, except 02)
```js
function makeDrill(cfg) { /* cfg: {qEl, fbEl, stEl, gen, check} */ }
```
- `gen()` returns `{html, data}` for a random question
- `check(raw, data)` returns `{ok, explanation}`
- Streak counter, Enter key listener, MathJax re-typeset on check

---

## Curriculum Volumes

| Volume | Modules | Topic |
|---|---|---|
| 1 | 01–36 | Foundations, Finite Fields, AES, GCM |
| 2 | 37–55 | Hash Functions, MACs, KDFs |
| 3 | 56–62 | Public-Key Cryptography, PKI |
| 4 | 63–66 | Protocol Architecture (TLS, AEAD) |
| 5 | 67–73 | Security Analysis, Side Channels, Composition |
| 6 | 74–76+ | Post-Quantum / Lattice-Based |

`CURRICULUM.md` is the authoritative module list. `GOLD_STANDARD.md` is the authoritative quality checklist.
