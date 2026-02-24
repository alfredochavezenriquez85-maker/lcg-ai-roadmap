# CLAUDE.md — LCG AI Roadmap

This file provides context for AI assistants working on the `lcg-ai-roadmap` repository.

## Project Overview

A self-contained, single-file interactive HTML presentation built for **London Consulting Group (LCG)**. It visualizes an AI adoption roadmap for enterprise clients, covering digital maturity levels, AI automation layers, and concrete use cases for Finance & Administration teams migrating to Microsoft Business Central.

- **Language**: Spanish (es)
- **Audience**: C-level and non-technical decision makers
- **Client context**: IGSA — a company implementing Business Central with LCG guidance
- **Branding**: LCG Digital · 2026

---

## Repository Structure

```
lcg-ai-roadmap/
├── index.html      # The entire application — HTML + CSS + JS in one file (~2026 lines)
└── CLAUDE.md       # This file
```

There are **no build tools, package managers, frameworks, or external dependencies** beyond Google Fonts loaded via CDN. Everything is vanilla HTML, CSS, and JavaScript.

---

## Application Architecture

### Single-File Design

The entire application lives in `index.html`. It is divided into three logical sections:

1. `<style>` block (lines 8–948) — All CSS with custom properties
2. `<body>` content (lines 950–2013) — Markup for all three pages
3. `<script>` block (lines 2015–2023) — Minimal JS for page navigation

### Pages and Navigation

The app has **three pages** toggled via a sticky navigation bar. Only one page is visible at a time (CSS class `active`):

| Tab | Page ID | Title |
|-----|---------|-------|
| 01 | `page-roadmap` | AI Roadmap — Automatización de Procesos y Decisiones |
| 02 | `page-ai101` | ¿Qué es la IA? (AI 101 for non-technical audiences) |
| 03 | `page-igsa` | IGSA — Use Cases IA en Finanzas y Administración |

Navigation is handled by a single JS function:

```js
// index.html:2016
function showPage(pageId, btn) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.querySelectorAll('.nav-tab').forEach(t => t.classList.remove('active'));
  document.getElementById('page-' + pageId).classList.add('active');
  btn.classList.add('active');
  window.scrollTo({ top: 0, behavior: 'smooth' });
}
```

---

## CSS Design System

### Custom Properties (CSS Variables)

Defined in `:root` (line 9):

```css
--bg: #0a0a0f          /* Near-black page background */
--surface: #13131a     /* Card/cell backgrounds */
--surface2: #1a1a24    /* Slightly lighter surface */
--border: #2a2a3a      /* Borders and dividers */
--text: #e8e8f0        /* Primary text */
--text-dim: #8888a0    /* Secondary/muted text */

/* Accent palette */
--accent-orange: #ff6b2b   /* Primary brand accent, CTAs */
--accent-amber: #ffb547    /* Copilot AI badge, warnings */
--accent-cyan: #00d4ff     /* Section titles, digital maturity */
--accent-green: #34d399    /* Positive states, N3 level */
--accent-purple: #a78bfa   /* Multi-agent, N4 level */
--accent-pink: #f472b6     /* Optimization AI, localización fiscal */

/* Level background variables */
--n0 through --n4          /* Per-level color schemes */
```

### Typography

- **Headings**: `'Outfit'` (Google Fonts) — weights 300, 400, 600, 700, 800, 900
- **Monospace / labels**: `'Space Mono'` (Google Fonts) — weights 400, 700
- **Viewport**: Fixed at `width=1600` (designed for large screens / presentations)

### Key Component Classes

| Class | Purpose |
|-------|---------|
| `.page` | Full page section; add `.active` to show |
| `.nav-bar` | Sticky top navigation |
| `.nav-tab` | Tab button; `.active` highlights current page |
| `.hero` | Page hero section with large heading |
| `.badge` | Pill label with border |
| `.insight-box` | Highlighted callout box with gradient border |
| `.matrix` | Main AI maturity matrix (Page 1) |
| `.matrix-row` | Single row in the matrix grid |
| `.matrix-cell` | Individual cell in the matrix |
| `.level-badge` | Vertical sidebar level label (N0–N4) |
| `.uc-area-section` | Use case group (Page 3, IGSA) |
| `.uc-card` | Collapsible use case card (click to expand) |
| `.uc-ai-badge` | AI type tag: `.copilot`, `.agentic`, `.multi` |
| `.tool-tag` | Technology tag chip |

### Maturity Level Color Coding

| Level | Theme | Color |
|-------|-------|-------|
| N0 — Papel + Excel | Dark blue-grey | `#6b7280` |
| N1 — Repositorios digitales | Olive/yellow | `#a3a33a` |
| N2 — (Integrated systems) | Blue | `#60a5fa` |
| N3 — (Process automation) | Green | `#34d399` |
| N4 — (Full orchestration) | Purple | `#a78bfa` |

---

## Page Content Reference

### Page 1 — AI Roadmap (`page-roadmap`)

**Main Matrix** — 5 columns × 5 rows:
- Column 1: Nivel (level badge N0–N4)
- Column 2: Madurez Digital (systems & data infrastructure)
- Column 3: Nivel de Automatización (how processes run)
- Column 4: IA Aplicada / Copilots (assists & generates)
- Column 5: Agentic AI (plans & executes)
- Column 6: Multi-Agente (agents collaborate)

**Key insight framing**: AI is not "the next level" — it is a horizontal layer that applies at every maturity level, including N0 (100% manual, on-premise).

**Levels**:
- N0: Paper + Excel, 100% manual
- N1: Digital repositories (Drive, SharePoint, OCR)
- N2: (Connected ERP/databases)
- N3: (Process automation with APIs)
- N4: (Full orchestration, event-driven)

### Page 2 — AI 101 (`page-ai101`)

Non-technical guide for decision makers. Covers:
1. What is AI (simple definition + analogy)
2. Why it matters now (3 shifts: accessible, natural language, agentic action)
3. 5 types of AI with enterprise use cases:
   - Generativa & Conversacional
   - Predictiva
   - Visión
   - Agentic AI
   - Optimización
4. 5 key trends 2025–2026
5. 10 key AI concepts (LLM, Prompt, RAG, Tokens, Fine-tuning, Agentic AI, MCP, Hallucination, Guardrails, Multimodal)

### Page 3 — IGSA Use Cases (`page-igsa`)

AI use case catalog for IGSA's Business Central implementation:

**Summary**: 7 areas, 20 use cases, 12 Copilot, 8 Agentic AI

| Area | Count | Color |
|------|-------|-------|
| Cuentas por Pagar | 4 | Orange |
| Cuentas por Cobrar | 4 | Cyan |
| Tesorería | 2 | Green |
| Activos Fijos | 2 | Purple |
| Facturación | 2 | Amber |
| Localización Fiscal | 3 | Pink |
| Contabilidad | 3 | Cyan |

Each use case card (`.uc-card`) is **click-to-expand** (toggles `.open` class) and shows:
- Process number (P01, C01, T01, etc.)
- Process name + subtitle
- AI type badge (COPILOT / AGENTE)
- AS IS (current pain), TO BE (BC improvement), AI Opportunity (specific implementation)
- Tool tags and impact metrics

---

## Development Conventions

### Making Changes

Since this is a single-file application, all edits go directly into `index.html`. There is no compilation step.

**Adding a new use case card** — follow the existing `.uc-card` pattern:
```html
<div class="uc-card" onclick="this.classList.toggle('open')">
  <div class="uc-card-header">
    <div class="uc-process-num" style="color: var(--accent-COLOR);">X00</div>
    <div class="uc-process-name">Process Name<div class="uc-sub">Subtitle</div></div>
    <div class="uc-ai-badges"><span class="uc-ai-badge copilot">COPILOT</span></div>
  </div>
  <div class="uc-card-body">
    <div class="uc-grid">
      <div class="uc-block as-is">...</div>
      <div class="uc-block to-be">...</div>
      <div class="uc-block ai-opp">...</div>
    </div>
  </div>
</div>
```

**Adding a new page**:
1. Add a button to `.nav-tabs`: `<button class="nav-tab" onclick="showPage('PAGEID', this)">...</button>`
2. Add a `<div id="page-PAGEID" class="page">` block inside `.container`

**Adding a new matrix row** — follow the `.matrix-row` pattern with the same 6-column grid:
```
grid-template-columns: 64px 220px 240px 1fr 1fr 1fr
```

### Style Conventions

- Use CSS variables (`var(--accent-orange)`) instead of hardcoded colors
- Add `animation-delay` to new `.matrix-row` elements to stagger entrance animations
- Section headers follow the pattern:
  ```html
  <div class="section-title">NN — Label</div>
  <div class="section-heading">Main Heading</div>
  <div class="section-sub">Descriptive subtitle text.</div>
  ```
- Content is in **Spanish**; maintain Spanish for all user-facing text

### Viewport and Display

The page is set to `width=1600` viewport — optimized for full-screen presentations and large monitors, not for mobile. Do not add responsive breakpoints without explicit instruction.

---

## External Resources

| Resource | URL | Purpose |
|----------|-----|---------|
| Google Fonts | `fonts.googleapis.com` | Space Mono + Outfit typefaces |
| LCG Logo | `londoncg.com/hs-fs/hubfs/...` | Navigation and footer logo |

No other external dependencies. No npm packages, no CDN JS libraries.

---

## Git Workflow

- **Main branch**: `main` (production)
- **Development branch**: `claude/add-claude-documentation-3BuB3`
- Commit messages should be clear and descriptive
- Push with: `git push -u origin <branch-name>`

---

## Key Business Context

- **LCG** = London Consulting Group — management consulting firm
- **IGSA** = Client company implementing Microsoft Business Central (ERP)
- **BC** = Business Central (Microsoft ERP)
- **SAT** = Mexican tax authority (Servicio de Administración Tributaria)
- **CFDI** = Mexican electronic invoice format
- **EFOS/EDOS** = SAT blacklists of tax fraud entities
- **MCP** = Model Context Protocol (Anthropic standard for AI tool connectivity)
- **Cowork** = AI automation tool mentioned for desktop/file operations
- **Computer Use** = Claude's computer control capability
