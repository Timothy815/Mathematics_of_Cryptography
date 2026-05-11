# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a static HTML curriculum of 76 self-contained educational modules on the mathematics of cryptography. There is no build system, package manager, or server — all files are opened directly in a browser. The curriculum spans 6 volumes, from binary foundations through lattice-based post-quantum cryptography.

## File Naming Convention

Every module follows a strict naming pattern:

- **Tutorial:** `tutorial_##_<slug>_html.html`
- **Workbook:** `tutorial_##_<slug>_workbook_html.html`

The `##` is zero-padded (e.g., `01`, `36`, `76`). The slug is a lowercased, underscore-separated description of the topic. Workbooks for some modules are not yet created — the homepage links to them when they exist.

## Architecture

```
/
├── index.html              # Homepage dashboard — module cards grid with search
├── css/
│   └── style.css           # Shared design system (CSS custom properties, layout, nav)
├── CURRICULUM.md           # Authoritative module list and volume structure
├── tutorial_##_*_html.html          # Lesson content (76 modules)
└── tutorial_##_*_workbook_html.html # Practice workbooks (most modules)
```

**There is no JavaScript framework.** Interactivity in workbooks is vanilla JS inline in `<script>` tags. Math rendering uses MathJax 3 loaded from CDN (`cdn.jsdelivr.net/npm/mathjax@3/es5/tex-svg.js`).

## CSS Design System

All modules link to `css/style.css`. The design system uses CSS custom properties defined in `:root`:

| Variable | Purpose |
|---|---|
| `--accent` | Primary blue (`#334e7d`) |
| `--bg` | Page background (`#f7f5ef`) |
| `--paper` | Card/content background (`#ffffff`) |
| `--radius` | Border radius (`18px`) |
| `--max-width` | Content width (`980px`) |
| `--gold-soft`, `--green-soft`, `--red-soft`, `--purple-soft` | Semantic box backgrounds |

Module-specific styles are always added as inline `<style>` blocks in the `<head>` of each HTML file — never by modifying `style.css` unless fixing a global issue.

## Tutorial HTML Structure

Every tutorial follows this structure:

```html
<head>
  <!-- MathJax config + CDN script -->
  <!-- <link rel="stylesheet" href="css/style.css"> -->
  <!-- Inline <style> for module-specific overrides -->
</head>
<body>
  <div class="page">
    <header class="tutorial-header">
      <!-- .course-label, .volume-label, <h1>, <p class="subtitle"> -->
      <nav class="tutorial-nav no-print">
        <!-- Top prev/next links + link back to index.html -->
      </nav>
    </header>
    <main>
      <!-- Content sections with <section id="..."> -->
      <section id="next"><!-- "What comes next" teaser --></section>
    </main>
    <nav class="bottom-nav no-print">
      <!-- Bottom prev/next navigation -->
    </nav>
  </div>
</body>
```

The `.no-print` class hides nav elements when printing. Both tutorials and workbooks include print-optimized CSS via `@media print`.

## Workbook HTML Structure

Workbooks use `<header class="workbook-header">` and include:
- `.workbook-nav` — jump-to-section navigation
- `.student-info` — name/date fill-in fields
- Problem sections with `<details class="solution"><summary>Show solution</summary>...</details>` for self-check answers

## Adding a New Module

1. Create `tutorial_##_<slug>_html.html` — copy structure from an existing tutorial at the same volume level
2. Set correct `<title>`, volume label, module number, and `<h1>`
3. Update `prevLink` href to the previous module's filename and `nextLink` href to the next
4. Update the **previous** module's `nextLink` to point to the new file
5. Add the module card to `index.html` in the correct volume section
6. Update `CURRICULUM.md` with the new module entry

## Curriculum Volumes

| Volume | Modules | Topic |
|---|---|---|
| 1 | 01–36 | Foundations, Finite Fields, AES, GCM |
| 2 | 37–55 | Hash Functions, MACs, KDFs |
| 3 | 56–62 | Public-Key Cryptography, PKI |
| 4 | 63–66 | Protocol Architecture (TLS, AEAD) |
| 5 | 67–73 | Security Analysis, Side Channels, Composition |
| 6 | 74–76+ | Post-Quantum / Lattice-Based |

`CURRICULUM.md` is the authoritative source — it tracks all 76 implemented modules and planned future modules.
