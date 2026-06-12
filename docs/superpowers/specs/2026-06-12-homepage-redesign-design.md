# Homepage Redesign Design Spec

**Date:** 2026-06-12  
**Author:** Xuemeng Yang  
**Status:** Approved

---

## Goal

Rebuild the personal homepage (`jokester-zzz.github.io`) to look premium and polished, inspired by Anthropic's homepage aesthetic. The result should be easy to maintain (add new papers/news via markdown) while having a visually distinctive, high-quality design.

---

## Decisions

| Dimension | Decision |
|-----------|----------|
| Visual style | Minimal, beige/cream color scheme |
| Tech approach | Custom Jekyll layout template — override al-folio's `about` layout; keep Jekyll data pipeline for content |
| Animation level | Static (pure CSS), no JavaScript animations in v1 |
| Hero layout | Split: text left, photo right |
| Page type | Single scrolling page (immersive) |

---

## Color Palette

| Token | Value | Use |
|-------|-------|-----|
| `--bg` | `#f5f0e8` | Page background |
| `--bg-alt` | `#ede7d9` | Hero right panel, footer, paper card hover |
| `--bg-grid` | `#e8e0d4` | Grid lines between paper cards |
| `--text-primary` | `#1a1208` | Headings, name |
| `--text-body` | `#3a2a1e` | Body copy |
| `--text-muted` | `#5a4a3a` | Descriptions, secondary text |
| `--text-subtle` | `#9a7a5a` | Labels, nav links, author names |
| `--accent` | `#c8a97e` | Divider lines, link dots, venue badge bg |
| `--accent-dark` | `#9a7a5a` | Venue badge text, eyebrow text |
| `--border` | `#e8e0d4` | Section dividers, card borders |

---

## Typography

- **Headings / Name:** Georgia serif (`font-family: Georgia, 'Times New Roman', serif`)
- **Body / UI:** System sans-serif (`-apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif`)
- **Name size:** 58px, font-weight 400, letter-spacing -0.02em
- **Section titles:** 30px serif, font-weight 400
- **Body:** 13–14px, line-height 1.8–1.85
- **Labels/eyebrows:** 9–10px, uppercase, letter-spacing 0.18–0.20em, font-weight 600–700

---

## Page Structure

### 1. Navbar
- **Left:** `Xuemeng Yang` in Georgia serif
- **Right:** text links — Research · Publications · CV · Contact
- Sticky, `border-bottom: 1px solid var(--border)`
- Background: `var(--bg)`

### 2. Hero (full-viewport height)
Two-column grid, separated by a 1px border:

**Left column** (flex, center-aligned vertically):
- Eyebrow: `—— Shanghai AI Lab · ADLab` (small caps, accent color, with short horizontal rule)
- Name: `Xuemeng / Yang` in 58px Georgia, two lines
- Description: 2–3 sentence research summary, 14px, max-width 340px
- Social links row: `● Google Scholar · ● GitHub · ● Email` (dot + uppercase label)

**Right column** (background `var(--bg-alt)`):
- Circular avatar photo (`yxm.jpeg`, 160px diameter, 3px accent-colored border)
- Name in Chinese + English: `Xuemeng Yang · 杨雪梦`
- Pill buttons: Scholar · GitHub · Email · CV PDF

### 3. Research Focus
- Section label: `RESEARCH FOCUS` (eyebrow style)
- Tagline: one sentence, 30px serif (e.g., *"Building agents that learn, act, and evolve in the real world."*)
- Paragraph: 2–3 sentences covering current + previous research areas
- Tag chips: LLM Agent Frameworks · Tool Use · Industrial Software AI · Continuous Learning · Agentic Search · Autonomous Driving

### 4. Selected Publications
- Section label above the grid
- 3-column grid of paper cards, separated by 1px `var(--bg-grid)` gutters
- Each card:
  - Venue badge (filled pill, `var(--accent-dark)` bg, white text)
  - Paper title (13px Georgia)
  - Authors (10px, muted)
  - `arXiv →` link
- Papers to include (6 cards, newest first):
  1. DriveArena — ICCV 2025
  2. Trainee Bench — ACL 2026 Findings
  3. O²-Searcher — TMLR 2026
  4. MUSE — ACL 2026 Findings
  5. EvolveR — ICML 2025
  6. LeapAD — NeurIPS 2024

### 5. Recent News
- Section label
- Timeline list: date + text, separated by `var(--border)` lines
- Pull from existing `_news/` markdown files via Jekyll Liquid

### 6. Footer
- Left: `Xuemeng Yang · 杨雪梦` (Georgia)
- Right: `yangxuemeng@pjlab.org.cn`
- Background: `var(--bg-alt)`

---

## Implementation Plan (high-level)

1. Create `_layouts/home-custom.html` — full custom HTML layout using above spec
2. Create `_sass/home-custom.scss` — all styles scoped to this layout
3. Update `_pages/about.md` front matter: `layout: home-custom`
4. Add `yxm.jpeg` avatar path reference
5. Add `.superpowers/` to `.gitignore`

---

## Content Sources

| Section | Source |
|---------|--------|
| Name, title, bio | `_pages/about.md` + resume |
| Papers | Hardcoded in layout (6 selected); full list stays in `_bibliography/` |
| News | Jekyll loop over `_news/` collection |
| Avatar | `assets/img/yxm.jpeg` |
| Social links | `_config.yml` social settings |

---

## Out of Scope (v1)

- Scroll animations / IntersectionObserver
- Dark mode toggle
- Mobile responsive breakpoints (addressed in v2)
- Full publications page redesign
