# Homepage Redesign Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Replace the al-folio about layout with a fully custom beige-themed homepage — split Hero, Research section, Publications grid, News list, Footer — while keeping all content editable via existing Markdown files.

**Architecture:** Create a standalone `_layouts/home-custom.html` (complete HTML document, no `layout: default`) and `assets/css/home-custom.css`. The layout uses Liquid to pull bio from `about.md` content, news from `site.news` collection, and config values from `_config.yml`. The 6 selected papers are hardcoded in the layout. Update `_pages/about.md` to use the new layout.

**Tech Stack:** Jekyll (Liquid templating), plain CSS (no SCSS, no frameworks), HTML5

---

## File Map

| File | Action | Purpose |
|------|--------|---------|
| `assets/css/home-custom.css` | Create | All styles for the custom homepage |
| `_layouts/home-custom.html` | Create | Full standalone HTML layout with Liquid |
| `_pages/about.md` | Modify | Change `layout: about` → `layout: home-custom` |

---

## Task 1: Create the CSS file

**Files:**
- Create: `assets/css/home-custom.css`

- [ ] **Step 1: Create `assets/css/home-custom.css` with this exact content**

```css
/* home-custom.css — standalone styles for the custom homepage */

:root {
  --bg:           #f5f0e8;
  --bg-alt:       #ede7d9;
  --bg-grid:      #e8e0d4;
  --text-primary: #1a1208;
  --text-body:    #3a2a1e;
  --text-muted:   #5a4a3a;
  --text-subtle:  #9a7a5a;
  --accent:       #c8a97e;
  --accent-dark:  #9a7a5a;
  --border:       #e8e0d4;
}

*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

body {
  background: var(--bg);
  color: var(--text-body);
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  font-size: 16px;
  line-height: 1.6;
}

a { color: inherit; text-decoration: none; }

/* ── Navbar ── */
.hc-nav {
  position: sticky;
  top: 0;
  z-index: 100;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px 64px;
  background: var(--bg);
  border-bottom: 1px solid var(--border);
}

.hc-nav__logo {
  font-family: Georgia, 'Times New Roman', serif;
  font-size: 17px;
  font-weight: 400;
  color: var(--text-primary);
  letter-spacing: 0.01em;
}

.hc-nav__links {
  display: flex;
  gap: 32px;
  list-style: none;
}

.hc-nav__links a {
  font-size: 13px;
  color: var(--text-subtle);
  letter-spacing: 0.04em;
  transition: color 0.15s;
}

.hc-nav__links a:hover { color: var(--text-primary); }

/* ── Hero ── */
.hc-hero {
  display: grid;
  grid-template-columns: 1fr 1fr;
  min-height: 92vh;
  border-bottom: 1px solid var(--border);
}

.hc-hero__left {
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 80px 64px;
  border-right: 1px solid var(--border);
}

.hc-eyebrow {
  display: flex;
  align-items: center;
  gap: 12px;
  margin-bottom: 28px;
}

.hc-eyebrow__line {
  width: 24px;
  height: 1px;
  background: var(--accent);
  flex-shrink: 0;
}

.hc-eyebrow__text {
  font-size: 10px;
  letter-spacing: 0.20em;
  text-transform: uppercase;
  color: var(--accent-dark);
  font-weight: 600;
}

.hc-hero__name {
  font-family: Georgia, 'Times New Roman', serif;
  font-size: 64px;
  font-weight: 400;
  color: var(--text-primary);
  line-height: 1.05;
  letter-spacing: -0.02em;
  margin-bottom: 32px;
}

.hc-hero__desc {
  font-size: 15px;
  color: var(--text-muted);
  line-height: 1.85;
  max-width: 380px;
  margin-bottom: 40px;
}

.hc-hero__desc p { margin: 0; }

.hc-hero__links {
  display: flex;
  gap: 20px;
  flex-wrap: wrap;
}

.hc-hero__link {
  display: flex;
  align-items: center;
  gap: 8px;
  font-size: 11px;
  color: var(--text-subtle);
  letter-spacing: 0.08em;
  text-transform: uppercase;
  font-weight: 600;
  transition: color 0.15s;
}

.hc-hero__link:hover { color: var(--text-primary); }

.hc-hero__link-dot {
  width: 5px;
  height: 5px;
  background: var(--accent);
  border-radius: 50%;
  flex-shrink: 0;
}

.hc-hero__right {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 20px;
  background: var(--bg-alt);
  padding: 64px 48px;
}

.hc-avatar {
  width: 180px;
  height: 180px;
  border-radius: 50%;
  object-fit: cover;
  border: 3px solid var(--accent);
}

.hc-hero__right-name {
  font-size: 11px;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--text-subtle);
  text-align: center;
}

.hc-social-pills {
  display: flex;
  gap: 10px;
  flex-wrap: wrap;
  justify-content: center;
}

.hc-pill {
  padding: 7px 16px;
  border: 1px solid var(--accent);
  border-radius: 24px;
  font-size: 11px;
  color: var(--accent-dark);
  letter-spacing: 0.06em;
  transition: background 0.15s, color 0.15s;
}

.hc-pill:hover { background: var(--accent); color: #fff; }

/* ── Sections ── */
.hc-section {
  padding: 80px 64px;
  border-bottom: 1px solid var(--border);
}

.hc-label {
  font-size: 10px;
  letter-spacing: 0.22em;
  text-transform: uppercase;
  color: var(--accent);
  font-weight: 700;
  margin-bottom: 18px;
}

.hc-section__title {
  font-family: Georgia, 'Times New Roman', serif;
  font-size: 32px;
  font-weight: 400;
  color: var(--text-primary);
  line-height: 1.3;
  max-width: 580px;
  margin-bottom: 20px;
}

.hc-section__body {
  font-size: 14px;
  color: var(--text-muted);
  line-height: 1.9;
  max-width: 660px;
}

/* ── Research Tags ── */
.hc-tags {
  display: flex;
  gap: 10px;
  flex-wrap: wrap;
  margin-top: 28px;
}

.hc-tag {
  padding: 6px 14px;
  background: var(--bg-alt);
  border: 1px solid var(--bg-grid);
  border-radius: 4px;
  font-size: 11px;
  color: var(--accent-dark);
  letter-spacing: 0.04em;
}

/* ── Publications ── */
.hc-pubs-header {
  padding: 56px 64px 20px;
}

.hc-pubs-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1px;
  background: var(--bg-grid);
  border-top: 1px solid var(--bg-grid);
  border-bottom: 1px solid var(--bg-grid);
}

.hc-paper {
  background: var(--bg);
  padding: 32px 28px;
  transition: background 0.15s;
}

.hc-paper:hover { background: var(--bg-alt); }

.hc-paper__venue {
  display: inline-block;
  font-size: 10px;
  letter-spacing: 0.10em;
  text-transform: uppercase;
  color: #fff;
  background: var(--accent-dark);
  padding: 3px 9px;
  border-radius: 3px;
  margin-bottom: 12px;
  font-weight: 600;
}

.hc-paper__title {
  font-family: Georgia, 'Times New Roman', serif;
  font-size: 14px;
  color: var(--text-primary);
  line-height: 1.55;
  margin-bottom: 10px;
  font-weight: 400;
}

.hc-paper__authors {
  font-size: 11px;
  color: var(--text-subtle);
  line-height: 1.5;
  margin-bottom: 12px;
}

.hc-paper__link {
  font-size: 11px;
  color: var(--accent);
  letter-spacing: 0.06em;
  text-transform: uppercase;
  font-weight: 600;
  transition: color 0.15s;
}

.hc-paper__link:hover { color: var(--text-primary); }

/* ── News ── */
.hc-news-list { max-width: 700px; }

.hc-news-item {
  display: flex;
  gap: 24px;
  padding: 18px 0;
  border-bottom: 1px solid var(--border);
  align-items: flex-start;
}

.hc-news-item:first-child { border-top: 1px solid var(--border); }

.hc-news__date {
  font-size: 11px;
  color: var(--accent);
  min-width: 72px;
  margin-top: 3px;
  letter-spacing: 0.04em;
  flex-shrink: 0;
}

.hc-news__text {
  font-size: 14px;
  color: var(--text-body);
  line-height: 1.65;
}

.hc-news__text a { color: var(--accent-dark); border-bottom: 1px solid var(--accent); }
.hc-news__text a:hover { color: var(--text-primary); }

/* ── Footer ── */
.hc-footer {
  padding: 32px 64px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: var(--bg-alt);
  border-top: 1px solid var(--border);
}

.hc-footer__name {
  font-family: Georgia, 'Times New Roman', serif;
  font-size: 15px;
  color: var(--text-subtle);
}

.hc-footer__email {
  font-size: 12px;
  color: var(--accent);
  letter-spacing: 0.04em;
}

.hc-footer__email:hover { color: var(--text-primary); }
```

- [ ] **Step 2: Commit**

```bash
git add assets/css/home-custom.css
git commit -m "feat: add home-custom.css with beige color palette and layout styles"
```

---

## Task 2: Create the layout HTML

**Files:**
- Create: `_layouts/home-custom.html`

- [ ] **Step 1: Create `_layouts/home-custom.html` with this exact content**

```html
---
---
<!DOCTYPE html>
<html lang="{{ site.lang | default: 'en' }}">
<head>
  {% include metadata.html %}
  <link rel="stylesheet" href="{{ '/assets/css/home-custom.css' | relative_url }}">
</head>
<body>

  <!-- Navbar -->
  <nav class="hc-nav">
    <a href="{{ '/' | relative_url }}" class="hc-nav__logo">
      {{ site.first_name }} {{ site.last_name }}
    </a>
    <ul class="hc-nav__links">
      <li><a href="#research">Research</a></li>
      <li><a href="#publications">Publications</a></li>
      <li><a href="{{ '/cv' | relative_url }}">CV</a></li>
      <li><a href="mailto:{{ site.email }}">Contact</a></li>
    </ul>
  </nav>

  <!-- Hero -->
  <section class="hc-hero">
    <div class="hc-hero__left">
      <div class="hc-eyebrow">
        <div class="hc-eyebrow__line"></div>
        <span class="hc-eyebrow__text">Shanghai AI Lab · ADLab</span>
      </div>
      <h1 class="hc-hero__name">{{ site.first_name }}<br>{{ site.last_name }}</h1>
      <div class="hc-hero__desc">{{ content }}</div>
      <div class="hc-hero__links">
        <a href="https://scholar.google.com/citations?user=xGuZsikAAAAJ" class="hc-hero__link" target="_blank" rel="noopener">
          <span class="hc-hero__link-dot"></span>Scholar
        </a>
        {% if site.github_username %}
        <a href="https://github.com/{{ site.github_username }}" class="hc-hero__link" target="_blank" rel="noopener">
          <span class="hc-hero__link-dot"></span>GitHub
        </a>
        {% endif %}
        {% if site.email %}
        <a href="mailto:{{ site.email }}" class="hc-hero__link">
          <span class="hc-hero__link-dot"></span>Email
        </a>
        {% endif %}
      </div>
    </div>
    <div class="hc-hero__right">
      {% if page.profile.image %}
      <img
        class="hc-avatar"
        src="{{ page.profile.image | prepend: '/assets/img/' | relative_url }}"
        alt="{{ site.first_name }} {{ site.last_name }}"
      >
      {% endif %}
      <div class="hc-hero__right-name">{{ site.first_name }} {{ site.last_name }} · 杨雪梦</div>
      <div class="hc-social-pills">
        <a href="https://scholar.google.com/citations?user=xGuZsikAAAAJ" class="hc-pill" target="_blank" rel="noopener">Scholar</a>
        {% if site.github_username %}
        <a href="https://github.com/{{ site.github_username }}" class="hc-pill" target="_blank" rel="noopener">GitHub</a>
        {% endif %}
        {% if site.email %}
        <a href="mailto:{{ site.email }}" class="hc-pill">Email</a>
        {% endif %}
      </div>
    </div>
  </section>

  <!-- Research Focus -->
  <section class="hc-section" id="research">
    <div class="hc-label">Research Focus</div>
    <h2 class="hc-section__title">Building agents that learn, act, and evolve in the real world.</h2>
    <p class="hc-section__body">
      My work spans AI agent frameworks for industrial software automation, agentic search and retrieval,
      and self-evolving agent mechanisms. Previously, I worked on autonomous driving —
      3D scene understanding, closed-loop simulation, and cognitive driving agents.
    </p>
    <div class="hc-tags">
      <span class="hc-tag">LLM Agent Frameworks</span>
      <span class="hc-tag">Tool Use</span>
      <span class="hc-tag">Industrial Software AI</span>
      <span class="hc-tag">Continuous Learning</span>
      <span class="hc-tag">Agentic Search</span>
      <span class="hc-tag">Autonomous Driving</span>
    </div>
  </section>

  <!-- Selected Publications -->
  <div class="hc-pubs-header" id="publications">
    <div class="hc-label">Selected Publications</div>
  </div>
  <div class="hc-pubs-grid">

    <div class="hc-paper">
      <span class="hc-paper__venue">ICCV 2025</span>
      <p class="hc-paper__title">DriveArena: A Closed-Loop Generative Simulation Platform for Autonomous Driving</p>
      <p class="hc-paper__authors">Yang X*, Wen L*, Wei T*, et al.</p>
      <a href="https://arxiv.org/pdf/2408.00415" class="hc-paper__link" target="_blank" rel="noopener">arXiv →</a>
    </div>

    <div class="hc-paper">
      <span class="hc-paper__venue">ACL 2026</span>
      <p class="hc-paper__title">The Agent's First Day: Benchmarking Learning &amp; Scheduling in Workplace Scenarios</p>
      <p class="hc-paper__authors">Fu D*, Mei J*, Wu R*, Yang X*, et al.</p>
      <a href="https://arxiv.org/pdf/2601.08173" class="hc-paper__link" target="_blank" rel="noopener">arXiv →</a>
    </div>

    <div class="hc-paper">
      <span class="hc-paper__venue">TMLR 2026</span>
      <p class="hc-paper__title">O²-Searcher: A Searching-based Agent for Open-domain Open-ended Question Answering</p>
      <p class="hc-paper__authors">Mei J, Hu T, Fu D, Wen L, Yang X, et al.</p>
      <a href="https://arxiv.org/pdf/2505.16582" class="hc-paper__link" target="_blank" rel="noopener">arXiv →</a>
    </div>

    <div class="hc-paper">
      <span class="hc-paper__venue">ACL 2026</span>
      <p class="hc-paper__title">Learning on the Job: An Experience-driven Self-evolving Agent for Long-horizon Tasks (MUSE)</p>
      <p class="hc-paper__authors">Yang C*, Yang X*, Wen L*, et al.</p>
      <a href="https://arxiv.org/pdf/2510.08002" class="hc-paper__link" target="_blank" rel="noopener">arXiv →</a>
    </div>

    <div class="hc-paper">
      <span class="hc-paper__venue">ICML 2025</span>
      <p class="hc-paper__title">EvolveR: Closed-loop Experience-driven Self-evolving Agent Architecture</p>
      <p class="hc-paper__authors">Mei J, ..., Yang X, et al.</p>
      <a href="https://arxiv.org/pdf/2510.16079" class="hc-paper__link" target="_blank" rel="noopener">arXiv →</a>
    </div>

    <div class="hc-paper">
      <span class="hc-paper__venue">NeurIPS 2024</span>
      <p class="hc-paper__title">LeapAD: Continuously Learning, Adapting, and Improving Autonomous Driving</p>
      <p class="hc-paper__authors">Mei J, Ma Y, Yang X, et al.</p>
      <a href="https://arxiv.org/pdf/2405.15324" class="hc-paper__link" target="_blank" rel="noopener">arXiv →</a>
    </div>

  </div>

  <!-- Recent News -->
  <section class="hc-section" id="news">
    <div class="hc-label">Recent News</div>
    <div class="hc-news-list">
      {% assign news_sorted = site.news | sort: "date" | reverse %}
      {% for item in news_sorted limit: 5 %}
      <div class="hc-news-item">
        <span class="hc-news__date">{{ item.date | date: "%b %Y" }}</span>
        <div class="hc-news__text">{{ item.content }}</div>
      </div>
      {% endfor %}
    </div>
  </section>

  <!-- Footer -->
  <footer class="hc-footer">
    <span class="hc-footer__name">{{ site.first_name }} {{ site.last_name }} · 杨雪梦</span>
    <a href="mailto:{{ site.email }}" class="hc-footer__email">{{ site.email }}</a>
  </footer>

  {% include scripts/analytics.html %}
</body>
</html>
```

- [ ] **Step 2: Commit**

```bash
git add _layouts/home-custom.html
git commit -m "feat: add home-custom layout with hero, research, publications, news, footer"
```

---

## Task 3: Wire up the layout and verify

**Files:**
- Modify: `_pages/about.md` (front matter only)

- [ ] **Step 1: Open `_pages/about.md` and change the layout line**

Find:
```yaml
layout: about
```

Replace with:
```yaml
layout: home-custom
```

Leave everything else in the front matter untouched (`profile`, `news`, `social`, etc.).

- [ ] **Step 2: Commit the change**

```bash
git add _pages/about.md
git commit -m "feat: switch homepage to home-custom layout"
```

- [ ] **Step 3: Start Jekyll and open the site**

```bash
bundle exec jekyll serve --livereload
```

Open `http://localhost:4000` in a browser. Expected: beige homepage with sticky navbar, split hero (name left, avatar right), Research section, 6 paper cards in a 3-column grid, news items, footer.

- [ ] **Step 4: Verify checklist**

Walk through each item:
- [ ] Navbar is sticky and shows correct name + links
- [ ] Hero left: eyebrow line + `Shanghai AI Lab · ADLab` + large name + bio text + 3 social links
- [ ] Hero right: `yxm.jpeg` circular avatar + name + pill buttons
- [ ] Research section: tagline + 6 topic tags
- [ ] Publications grid: 6 cards, 3 columns, each with venue badge + title + authors + arXiv link
- [ ] News: at least 3 items from `_news/` with date + content
- [ ] Footer: name + email
- [ ] No leftover al-folio Bootstrap navbar or footer visible (the page is fully standalone)

- [ ] **Step 5: If al-folio header/footer appears**, it means Jekyll is resolving `metadata.html` and injecting the `default` layout. Check that `_layouts/home-custom.html` has the `---\n---` front matter at line 1, and that `_pages/about.md` says `layout: home-custom` (not `layout: about`).

---

## Self-Review

**Spec coverage:**
- ✅ Color palette (CSS variables match spec)
- ✅ Typography (Georgia serif headings, system sans body, correct sizes)
- ✅ Navbar (sticky, name + 4 links)
- ✅ Hero split layout (left text + right photo)
- ✅ Eyebrow with line decoration
- ✅ Social links (Scholar, GitHub, Email)
- ✅ Research section (tagline + body + 6 tags)
- ✅ Publications grid (6 papers, 3 columns, venue badges)
- ✅ News via Jekyll Liquid loop (`site.news`)
- ✅ Footer (name + email)
- ✅ No JS animations (pure CSS)
- ✅ Content still editable via Markdown (`about.md` body → `{{ content }}`, news via `_news/`)

**Placeholder scan:** None found.

**Type consistency:** CSS class names used in HTML (`hc-nav`, `hc-hero`, etc.) match class definitions in CSS exactly.
