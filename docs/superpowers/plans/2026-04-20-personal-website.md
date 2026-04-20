# Personal Website Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a 6-page personal website for Dr. Marc Bravin using plain HTML/CSS/JS with a fixed dark sidebar and teal accent color scheme matching Gopf AG's brand.

**Architecture:** Fixed 280px dark sidebar on all pages (duplicated per page — no build step). Shared `assets/style.css` for all components. Each page is a standalone `.html` file in the repo root. No JavaScript frameworks, no bundler, opens directly as `file://` or deploys to any static host.

**Tech Stack:** HTML5, CSS3 (custom properties, CSS Grid, Flexbox), vanilla JS (none required initially), no build tools.

**Spec:** `docs/superpowers/specs/2026-04-20-personal-website-design.md`

---

## File Map

| File | Responsibility |
|---|---|
| `assets/style.css` | All shared styles: sidebar, layout, typography, components |
| `assets/foto_marc_bravin.jpeg` | Profile photo (copy from Google Drive) |
| `index.html` | About page — hero, bio, badges, stat cards, recent highlights |
| `work.html` | Work Experience — full timeline |
| `research.html` | Research & Talks — papers, talks, patent, teaching |
| `projects.html` | Projects — card grid |
| `press.html` | Press & Awards — media + honours table |
| `contact.html` | Contact — email, LinkedIn, location |
| `.gitignore` | Ignore OS files, `.superpowers/` |

---

## Task 1: Scaffolding

**Files:**
- Create: `assets/` directory
- Create: `assets/foto_marc_bravin.jpeg` (copy from Google Drive)
- Create: `.gitignore`

- [ ] **Step 1: Create assets directory and copy photo**

```bash
mkdir -p assets
cp "/Users/tabravin/marcbravin94@gmail.com - Google Drive/My Drive/Zeugnisse/foto_marc_bravin.jpeg" assets/foto_marc_bravin.jpeg
ls -lh assets/foto_marc_bravin.jpeg
```

Expected: file listed at ~572K

- [ ] **Step 2: Create .gitignore**

Create `.gitignore`:
```
.DS_Store
.superpowers/
*.log
```

- [ ] **Step 3: Commit**

```bash
git add assets/foto_marc_bravin.jpeg .gitignore
git commit -m "chore: add photo asset and gitignore"
```

---

## Task 2: Shared CSS

**Files:**
- Create: `assets/style.css`

- [ ] **Step 1: Write assets/style.css**

```css
/* ===== RESET & BASE ===== */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
html { font-size: 16px; }
body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif;
  display: flex;
  min-height: 100vh;
  background: #fff;
  color: #374151;
}
a { color: inherit; text-decoration: none; }

/* ===== SIDEBAR ===== */
.sidebar {
  width: 280px;
  min-width: 280px;
  background: #0f1117;
  color: #fff;
  position: fixed;
  top: 0; left: 0; bottom: 0;
  display: flex;
  flex-direction: column;
  padding: 36px 28px;
  overflow-y: auto;
  z-index: 100;
}
.sidebar-photo {
  width: 120px;
  height: 120px;
  border-radius: 50%;
  border: 3px solid #2ab4a0;
  overflow: hidden;
  margin-bottom: 20px;
  flex-shrink: 0;
}
.sidebar-photo img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}
.sidebar h1 {
  font-size: 17px;
  font-weight: 700;
  color: #f9fafb;
  margin-bottom: 5px;
}
.sidebar .subtitle {
  font-size: 11.5px;
  color: #9ca3af;
  line-height: 1.65;
  margin-bottom: 28px;
}
.sidebar .subtitle span { color: #2ab4a0; }

/* ===== NAV ===== */
nav { display: flex; flex-direction: column; gap: 2px; }
nav a {
  display: block;
  padding: 8px 10px;
  border-radius: 5px;
  font-size: 13px;
  color: #9ca3af;
  transition: background 0.15s, color 0.15s;
}
nav a:hover { background: #1e2532; color: #f9fafb; }
nav a.active { background: #1e2532; color: #2ab4a0; font-weight: 600; }

/* ===== SIDEBAR LINKS ===== */
.sidebar-links {
  margin-top: auto;
  padding-top: 24px;
  border-top: 1px solid #1e2532;
  display: flex;
  flex-direction: column;
  gap: 9px;
}
.sidebar-links a {
  font-size: 12px;
  color: #6b7280;
  display: flex;
  align-items: center;
  gap: 8px;
  transition: color 0.15s;
}
.sidebar-links a:hover { color: #2ab4a0; }
.dot {
  width: 5px;
  height: 5px;
  border-radius: 50%;
  background: #2ab4a0;
  flex-shrink: 0;
}

/* ===== MAIN CONTENT ===== */
.main {
  margin-left: 280px;
  flex: 1;
  padding: 52px 60px;
  max-width: 900px;
}

/* ===== TYPOGRAPHY ===== */
.section-label {
  font-size: 10px;
  font-weight: 700;
  letter-spacing: 2px;
  color: #2ab4a0;
  text-transform: uppercase;
  margin-bottom: 22px;
}
.page-title {
  font-size: 23px;
  font-weight: 700;
  color: #111;
  line-height: 1.4;
  margin-bottom: 18px;
}
.page-title em { color: #2ab4a0; font-style: normal; }
.lead {
  font-size: 15px;
  color: #4b5563;
  line-height: 1.85;
  margin-bottom: 32px;
  max-width: 640px;
}

/* ===== BADGES ===== */
.badges { display: flex; flex-wrap: wrap; gap: 8px; margin-bottom: 40px; }
.badge {
  background: #f3f4f6;
  color: #374151;
  padding: 5px 13px;
  border-radius: 20px;
  font-size: 12px;
  font-weight: 500;
}

/* ===== HIGHLIGHT CARDS ===== */
.highlights {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
  margin-bottom: 48px;
}
.highlight-card {
  background: #f9fafb;
  border: 1px solid #e5e7eb;
  border-radius: 8px;
  padding: 20px;
}
.highlight-card .num {
  font-size: 26px;
  font-weight: 800;
  color: #2ab4a0;
  margin-bottom: 5px;
}
.highlight-card .desc {
  font-size: 12px;
  color: #6b7280;
  line-height: 1.5;
}

/* ===== RECENT HIGHLIGHTS ===== */
.recent-section { margin-bottom: 48px; }
.recent-section h3 {
  font-size: 11px;
  font-weight: 700;
  color: #111;
  letter-spacing: 1.5px;
  text-transform: uppercase;
  margin-bottom: 14px;
}
.recent-item {
  display: flex;
  align-items: flex-start;
  gap: 12px;
  padding: 13px 0;
  border-bottom: 1px solid #f3f4f6;
}
.recent-item:last-child { border-bottom: none; }
.recent-tag {
  font-size: 10px;
  font-weight: 600;
  padding: 3px 9px;
  border-radius: 10px;
  white-space: nowrap;
  margin-top: 2px;
  flex-shrink: 0;
}
.tag-press { background: #fef3c7; color: #92400e; }
.tag-research { background: #ede9fe; color: #5b21b6; }
.tag-project { background: #d1fae5; color: #065f46; }
.recent-item .item-text { font-size: 13.5px; color: #374151; line-height: 1.5; }
.recent-item .item-date { font-size: 11px; color: #9ca3af; margin-top: 3px; }

/* ===== TIMELINE (Work Experience) ===== */
.timeline { display: flex; flex-direction: column; gap: 0; }
.timeline-item {
  display: flex;
  gap: 24px;
  padding-bottom: 36px;
  position: relative;
}
.timeline-item::before {
  content: '';
  position: absolute;
  left: 11px;
  top: 20px;
  bottom: 0;
  width: 2px;
  background: #e5e7eb;
}
.timeline-item:last-child::before { display: none; }
.timeline-dot {
  width: 24px;
  height: 24px;
  border-radius: 50%;
  border: 2px solid #e5e7eb;
  background: #fff;
  flex-shrink: 0;
  margin-top: 2px;
  z-index: 1;
}
.timeline-dot.active {
  border-color: #2ab4a0;
  background: #2ab4a0;
}
.timeline-body { flex: 1; }
.timeline-role {
  font-size: 15px;
  font-weight: 700;
  color: #111;
  margin-bottom: 2px;
}
.timeline-company {
  font-size: 13px;
  color: #2ab4a0;
  font-weight: 600;
  margin-bottom: 3px;
}
.timeline-date {
  font-size: 12px;
  color: #9ca3af;
  margin-bottom: 10px;
}
.timeline-body ul {
  padding-left: 16px;
  display: flex;
  flex-direction: column;
  gap: 5px;
}
.timeline-body li { font-size: 13.5px; color: #4b5563; line-height: 1.6; }

/* ===== PUBLICATIONS ===== */
.pub-section { margin-bottom: 40px; }
.pub-section-title {
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 1.5px;
  text-transform: uppercase;
  color: #111;
  margin-bottom: 16px;
  padding-bottom: 8px;
  border-bottom: 2px solid #2ab4a0;
}
.featured-paper {
  background: #f0fdf9;
  border: 1px solid #2ab4a0;
  border-radius: 8px;
  padding: 20px;
  margin-bottom: 32px;
}
.featured-paper .paper-badge {
  display: inline-block;
  background: #2ab4a0;
  color: #fff;
  font-size: 10px;
  font-weight: 700;
  letter-spacing: 1px;
  text-transform: uppercase;
  padding: 3px 10px;
  border-radius: 10px;
  margin-bottom: 10px;
}
.featured-paper .paper-title {
  font-size: 15px;
  font-weight: 700;
  color: #111;
  margin-bottom: 6px;
}
.featured-paper .paper-authors {
  font-size: 12.5px;
  color: #6b7280;
  margin-bottom: 8px;
}
.featured-paper .paper-meta {
  font-size: 12px;
  color: #4b5563;
}
.featured-paper .paper-meta a { color: #2ab4a0; text-decoration: underline; }
.pub-entry {
  padding: 14px 0;
  border-bottom: 1px solid #f3f4f6;
}
.pub-entry:last-child { border-bottom: none; }
.pub-entry .pub-title {
  font-size: 13.5px;
  font-weight: 600;
  color: #111;
  margin-bottom: 4px;
  font-style: italic;
}
.pub-entry .pub-authors { font-size: 12.5px; color: #4b5563; margin-bottom: 3px; }
.pub-entry .pub-venue { font-size: 12px; color: #9ca3af; }

/* ===== TEACHING TABLE ===== */
.table-wrap { overflow-x: auto; margin-bottom: 40px; }
table { width: 100%; border-collapse: collapse; font-size: 13.5px; }
thead th {
  text-align: left;
  font-size: 10px;
  font-weight: 700;
  letter-spacing: 1px;
  text-transform: uppercase;
  color: #9ca3af;
  padding: 8px 12px;
  border-bottom: 2px solid #e5e7eb;
}
tbody td {
  padding: 12px 12px;
  border-bottom: 1px solid #f3f4f6;
  color: #374151;
  vertical-align: top;
}
tbody tr:last-child td { border-bottom: none; }

/* ===== PROJECT CARDS ===== */
.project-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 20px;
  margin-bottom: 48px;
}
.project-card {
  background: #f9fafb;
  border: 1px solid #e5e7eb;
  border-radius: 8px;
  padding: 22px;
  transition: border-color 0.15s;
}
.project-card:hover { border-color: #2ab4a0; }
.project-card .project-tag {
  font-size: 10px;
  font-weight: 700;
  color: #2ab4a0;
  letter-spacing: 1px;
  text-transform: uppercase;
  margin-bottom: 8px;
}
.project-card .project-title {
  font-size: 15px;
  font-weight: 700;
  color: #111;
  margin-bottom: 8px;
  line-height: 1.35;
}
.project-card .project-desc {
  font-size: 13px;
  color: #6b7280;
  line-height: 1.65;
}

/* ===== PRESS ===== */
.press-section { margin-bottom: 36px; }
.press-section-title {
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 1.5px;
  text-transform: uppercase;
  color: #111;
  margin-bottom: 14px;
  padding-bottom: 6px;
  border-bottom: 1px solid #e5e7eb;
}
.press-item {
  display: flex;
  align-items: flex-start;
  gap: 16px;
  padding: 12px 0;
  border-bottom: 1px solid #f3f4f6;
}
.press-item:last-child { border-bottom: none; }
.press-year {
  font-size: 12px;
  font-weight: 700;
  color: #9ca3af;
  min-width: 36px;
  margin-top: 2px;
}
.press-outlet { font-size: 13.5px; font-weight: 600; color: #111; margin-bottom: 2px; }
.press-topic { font-size: 13px; color: #6b7280; font-style: italic; }

/* ===== AWARDS ===== */
.awards-table tbody tr:hover td { background: #f9fafb; }

/* ===== CONTACT ===== */
.contact-grid {
  display: flex;
  flex-direction: column;
  gap: 14px;
  max-width: 400px;
  margin-bottom: 40px;
}
.contact-item {
  display: flex;
  align-items: center;
  gap: 14px;
  font-size: 15px;
  color: #374151;
}
.contact-item .contact-label {
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 1px;
  text-transform: uppercase;
  color: #9ca3af;
  min-width: 70px;
}
.contact-item a { color: #2ab4a0; }
.contact-item a:hover { text-decoration: underline; }

/* ===== RESPONSIVE ===== */
@media (max-width: 768px) {
  body { flex-direction: column; }
  .sidebar {
    position: static;
    width: 100%;
    min-width: 0;
    padding: 24px 20px;
    flex-direction: row;
    flex-wrap: wrap;
    align-items: center;
    gap: 16px;
  }
  .sidebar-photo { width: 64px; height: 64px; margin-bottom: 0; }
  .sidebar h1 { font-size: 15px; }
  .sidebar .subtitle { display: none; }
  nav { flex-direction: row; flex-wrap: wrap; gap: 4px; }
  .sidebar-links { display: none; }
  .main { margin-left: 0; padding: 32px 20px; }
  .highlights { grid-template-columns: 1fr 1fr; }
  .project-grid { grid-template-columns: 1fr; }
}
```

- [ ] **Step 2: Verify CSS syntax**

```bash
# Check file was written
wc -l assets/style.css
```
Expected: ~300+ lines

- [ ] **Step 3: Commit**

```bash
git add assets/style.css
git commit -m "feat: add shared stylesheet"
```

---

## Task 3: About Page (index.html)

**Files:**
- Create: `index.html`

- [ ] **Step 1: Write index.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Dr. Marc Bravin</title>
  <link rel="stylesheet" href="assets/style.css">
</head>
<body>

<aside class="sidebar">
  <div class="sidebar-photo">
    <img src="assets/foto_marc_bravin.jpeg" alt="Dr. Marc Bravin">
  </div>
  <h1>Dr. Marc Bravin</h1>
  <p class="subtitle">
    CTO &amp; Co-Founder at <span>Gopf AG</span><br>
    AI Researcher · Lecturer at HSLU
  </p>
  <nav>
    <a href="index.html" class="active">About</a>
    <a href="work.html">Work Experience</a>
    <a href="research.html">Research &amp; Talks</a>
    <a href="projects.html">Projects</a>
    <a href="press.html">Press &amp; Awards</a>
    <a href="contact.html">Contact</a>
  </nav>
  <div class="sidebar-links">
    <a href="https://www.linkedin.com/in/marc-bravin" target="_blank"><span class="dot"></span>linkedin.com/in/marc-bravin</a>
    <a href="https://gopf.com" target="_blank"><span class="dot"></span>gopf.com</a>
    <a href="mailto:marc.bravin@gopf.com"><span class="dot"></span>marc.bravin@gopf.com</a>
  </div>
</aside>

<main class="main">
  <p class="section-label">About</p>

  <h1 class="page-title">
    Building AI that works in the <em>real world</em> —<br>
    from lab to production.
  </h1>

  <p class="lead">
    I'm a CTO, AI researcher, and lecturer based in Zürich. At <strong>Gopf AG</strong>
    I lead the engineering of an AI-powered market intelligence platform. My research —
    anchored in a <strong>PhD Summa Cum Laude</strong> from the University of Lucerne —
    focuses on multimodal machine learning and what it reveals about human behaviour.
    At <strong>HSLU</strong> I teach deep learning and run applied R&amp;D projects with
    industry partners.
  </p>

  <div class="badges">
    <span class="badge">Machine Learning</span>
    <span class="badge">NLP</span>
    <span class="badge">Computer Vision</span>
    <span class="badge">Agentic AI</span>
    <span class="badge">B2B SaaS</span>
    <span class="badge">Research</span>
    <span class="badge">Python</span>
    <span class="badge">PyTorch</span>
  </div>

  <div class="highlights">
    <div class="highlight-card">
      <div class="num">15+</div>
      <div class="desc">peer-reviewed publications &amp; conference papers</div>
    </div>
    <div class="highlight-card">
      <div class="num">PhD</div>
      <div class="desc">Summa Cum Laude, University of Lucerne</div>
    </div>
    <div class="highlight-card">
      <div class="num">10y+</div>
      <div class="desc">experience in ML engineering &amp; research</div>
    </div>
  </div>

  <div class="recent-section">
    <h3>Recent Highlights</h3>
    <div class="recent-item">
      <span class="recent-tag tag-press">Press</span>
      <div>
        <div class="item-text">SRF Kassensturz — interviewed on AI &amp; society: <em>Schöne neue KI Welt</em></div>
        <div class="item-date">2025</div>
      </div>
    </div>
    <div class="recent-item">
      <span class="recent-tag tag-project">Project</span>
      <div>
        <div class="item-text">Co-authored the Swiss AI Jobs Report 2025 with HSLU</div>
        <div class="item-date">September 2025</div>
      </div>
    </div>
    <div class="recent-item">
      <span class="recent-tag tag-research">Research</span>
      <div>
        <div class="item-text"><em>How to Follow Social Media Trends?</em> — Under Review, Journal of Marketing (4th Round)</div>
        <div class="item-date">Bravin, Clegg, Hofstetter, Pouly &amp; Berger · 2025</div>
      </div>
    </div>
    <div class="recent-item">
      <span class="recent-tag tag-research">Research</span>
      <div>
        <div class="item-text">EMAC 2024 — <em>AI Creativity: Studying the Effects of Similarity in Co-Work with Generative AI</em></div>
        <div class="item-date">Bucharest, Romania</div>
      </div>
    </div>
  </div>
</main>

</body>
</html>
```

- [ ] **Step 2: Open in browser and verify**

```bash
open index.html
```

Check:
- Profile photo shows (not broken)
- Teal accent color on section label, headline emphasis, highlight numbers
- Dark sidebar with white text
- "About" nav link is active (teal + dark bg)
- Three highlight cards in a row

- [ ] **Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add about page"
```

---

## Task 4: Work Experience Page (work.html)

**Files:**
- Create: `work.html`

- [ ] **Step 1: Write work.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Work Experience — Dr. Marc Bravin</title>
  <link rel="stylesheet" href="assets/style.css">
</head>
<body>

<aside class="sidebar">
  <div class="sidebar-photo">
    <img src="assets/foto_marc_bravin.jpeg" alt="Dr. Marc Bravin">
  </div>
  <h1>Dr. Marc Bravin</h1>
  <p class="subtitle">
    CTO &amp; Co-Founder at <span>Gopf AG</span><br>
    AI Researcher · Lecturer at HSLU
  </p>
  <nav>
    <a href="index.html">About</a>
    <a href="work.html" class="active">Work Experience</a>
    <a href="research.html">Research &amp; Talks</a>
    <a href="projects.html">Projects</a>
    <a href="press.html">Press &amp; Awards</a>
    <a href="contact.html">Contact</a>
  </nav>
  <div class="sidebar-links">
    <a href="https://www.linkedin.com/in/marc-bravin" target="_blank"><span class="dot"></span>linkedin.com/in/marc-bravin</a>
    <a href="https://gopf.com" target="_blank"><span class="dot"></span>gopf.com</a>
    <a href="mailto:marc.bravin@gopf.com"><span class="dot"></span>marc.bravin@gopf.com</a>
  </div>
</aside>

<main class="main">
  <p class="section-label">Work Experience</p>
  <h1 class="page-title">Career</h1>

  <div class="timeline">

    <div class="timeline-item">
      <div class="timeline-dot active"></div>
      <div class="timeline-body">
        <div class="timeline-role">CTO &amp; Co-Founder</div>
        <div class="timeline-company">Gopf AG</div>
        <div class="timeline-date">February 2023 – Present · Lucerne/Zürich, Switzerland</div>
        <ul>
          <li>Lead the engineering team building an AI-powered competitive intelligence platform for B2B clients</li>
          <li>Responsible for full technical architecture and development of the SaaS product</li>
          <li>Oversee scalable cloud infrastructure, NLP pipelines, and Agentic AI models</li>
          <li>Bridge the gap between academic research and production-ready machine learning</li>
          <li>Led the product from concept to launch, including infrastructure management and technology strategy</li>
        </ul>
      </div>
    </div>

    <div class="timeline-item">
      <div class="timeline-dot active"></div>
      <div class="timeline-body">
        <div class="timeline-role">Lecturer for Artificial Intelligence &amp; Deputy Head of Digital Business Lab</div>
        <div class="timeline-company">Lucerne University of Applied Sciences and Arts (HSLU)</div>
        <div class="timeline-date">April 2025 – Present · Rotkreuz, Switzerland</div>
        <ul>
          <li>Lecture on Deep Learning in the Master's program (3 ECTS)</li>
          <li>Contribute to strategic direction of the Digital Business Lab</li>
          <li>Lead applied research projects with industry partners from idea through deployment</li>
          <li>Secure funding and write grant proposals for research initiatives</li>
          <li>Active public communication: representing HSLU on AI/Data Science topics in press, radio, and TV</li>
        </ul>
      </div>
    </div>

    <div class="timeline-item">
      <div class="timeline-dot"></div>
      <div class="timeline-body">
        <div class="timeline-role">Postdoctoral Researcher</div>
        <div class="timeline-company">University of St. Gallen (HSG) — Institut für Marketing und Consumer Insight</div>
        <div class="timeline-date">March 2025 – August 2025 · 40%</div>
        <ul>
          <li>Designed and implemented a novel framework to transform unstructured video data into structured representations using multimodal (visual + audio) embeddings</li>
          <li>Validated the framework through a field experiment demonstrating strong predictive power for social media engagement</li>
          <li>Finalized and submitted a scientific publication introducing the multimodal video analysis framework</li>
        </ul>
      </div>
    </div>

    <div class="timeline-item">
      <div class="timeline-dot"></div>
      <div class="timeline-body">
        <div class="timeline-role">Senior Research Associate in Artificial Intelligence</div>
        <div class="timeline-company">Lucerne University of Applied Sciences and Arts (HSLU)</div>
        <div class="timeline-date">January 2023 – March 2025 · Rotkreuz, Switzerland</div>
        <ul>
          <li>Independently led multi-year applied R&amp;D projects with industry partners (up to 3 years), including planning, execution, and controlling</li>
          <li>Designed, implemented, and validated custom ML algorithms and data analysis solutions</li>
          <li>Acquired new research projects including grant proposals with research and industry partners</li>
          <li>Published and presented research findings at national and international conferences</li>
        </ul>
      </div>
    </div>

    <div class="timeline-item">
      <div class="timeline-dot"></div>
      <div class="timeline-body">
        <div class="timeline-role">Data Scientist</div>
        <div class="timeline-company">Jaywalker Digital AG</div>
        <div class="timeline-date">March 2020 – August 2023 · Lucerne, Switzerland</div>
        <ul>
          <li>Deep exploratory analysis of complex customer data for a youth marketing agency</li>
          <li>Developed NLP-based competitor text analysis tools</li>
          <li>Built recommender systems from prototype to production</li>
          <li>Created interactive data visualizations and Streamlit dashboards</li>
        </ul>
      </div>
    </div>

    <div class="timeline-item">
      <div class="timeline-dot"></div>
      <div class="timeline-body">
        <div class="timeline-role">Research Associate in Artificial Intelligence</div>
        <div class="timeline-company">Lucerne University of Applied Sciences and Arts (HSLU)</div>
        <div class="timeline-date">March 2021 – December 2022 · Rotkreuz, Switzerland</div>
        <ul>
          <li>Data scientist and engineer for ML solutions for industry partners</li>
          <li>Developed NLP and computer vision systems at the Algorithmic Business Research Lab</li>
        </ul>
      </div>
    </div>

    <div class="timeline-item">
      <div class="timeline-dot"></div>
      <div class="timeline-body">
        <div class="timeline-role">Research Assistant in Artificial Intelligence</div>
        <div class="timeline-company">Lucerne University of Applied Sciences and Arts (HSLU)</div>
        <div class="timeline-date">September 2018 – February 2021 · Rotkreuz, Switzerland</div>
        <ul>
          <li>Data scientist and engineer for ML solutions</li>
          <li>Teaching assistant for machine learning modules</li>
        </ul>
      </div>
    </div>

    <div class="timeline-item">
      <div class="timeline-dot"></div>
      <div class="timeline-body">
        <div class="timeline-role">Full-Stack Software Engineer</div>
        <div class="timeline-company">Network 41 AG</div>
        <div class="timeline-date">August 2015 – August 2018 · Sursee, Switzerland</div>
        <ul>
          <li>Developed one of the company's first AI applications: automated image quality inspection using TensorFlow</li>
          <li>Designed and built the company's Intranet/Extranet with ASP.NET C# and JavaScript</li>
          <li>Developed business applications and complex T-SQL stored procedures</li>
        </ul>
      </div>
    </div>

    <div class="timeline-item">
      <div class="timeline-dot"></div>
      <div class="timeline-body">
        <div class="timeline-role">Software Engineer</div>
        <div class="timeline-company">Pilatus Aircraft Ltd</div>
        <div class="timeline-date">August 2014 – January 2015 · Stans, Switzerland</div>
        <ul>
          <li>Developed and maintained the Pilatus customer portal (ASP.NET)</li>
          <li>Integrated enterprise systems (SAP, JIRA, Teamcenter) via REST APIs</li>
          <li>Configured Jenkins and Octopus CI/CD pipelines</li>
        </ul>
      </div>
    </div>

    <div class="timeline-item">
      <div class="timeline-dot"></div>
      <div class="timeline-body">
        <div class="timeline-role">Apprenticeship in Computer Science (Software Development)</div>
        <div class="timeline-company">Pilatus Aircraft Ltd</div>
        <div class="timeline-date">August 2010 – August 2014 · Stans, Switzerland</div>
        <ul>
          <li>Specialization in Software Development</li>
          <li>Grade: 5.7/6 — Awarded Apprenticeship Graduation (top grade)</li>
        </ul>
      </div>
    </div>

  </div>

  <div style="margin-top: 48px;">
    <p class="section-label">Education</p>
    <div class="timeline">
      <div class="timeline-item">
        <div class="timeline-dot"></div>
        <div class="timeline-body">
          <div class="timeline-role">PhD in Algorithmic Marketing / Business Administration</div>
          <div class="timeline-company">University of Lucerne</div>
          <div class="timeline-date">January 2021 – February 2025 · <strong style="color:#2ab4a0;">Summa Cum Laude</strong></div>
          <ul>
            <li>Dissertation: <em>Unlocking Consumer Insights: Multimodal Approaches to Unstructured Data Analysis</em></li>
            <li>Advisor: Prof. Reto Hofstetter</li>
          </ul>
        </div>
      </div>
      <div class="timeline-item">
        <div class="timeline-dot"></div>
        <div class="timeline-body">
          <div class="timeline-role">Master of Science in Engineering (MSc) — Data Science</div>
          <div class="timeline-company">Lucerne University of Applied Sciences and Arts (HSLU)</div>
          <div class="timeline-date">2018 – 2021 · Thesis grade: 6/6</div>
          <ul>
            <li>Specialization: Machine Learning for NLP and Computer Vision</li>
            <li>Thesis: <em>Learning Video Embeddings for Similarity Computation</em></li>
          </ul>
        </div>
      </div>
      <div class="timeline-item">
        <div class="timeline-dot"></div>
        <div class="timeline-body">
          <div class="timeline-role">Bachelor of Science in Computer Science (BSc)</div>
          <div class="timeline-company">Lucerne University of Applied Sciences and Arts (HSLU)</div>
          <div class="timeline-date">2015 – 2018 · Thesis grade: 6/6 · Dean's List 2018</div>
          <ul>
            <li>Thesis: <em>Deep Neural Fridge Analyzer</em></li>
          </ul>
        </div>
      </div>
    </div>
  </div>

</main>
</body>
</html>
```

- [ ] **Step 2: Open in browser and verify**

```bash
open work.html
```

Check: timeline renders with teal dots on current roles, grey dots on past, "Work Experience" nav item is active.

- [ ] **Step 3: Commit**

```bash
git add work.html
git commit -m "feat: add work experience page"
```

---

## Task 5: Research & Talks Page (research.html)

**Files:**
- Create: `research.html`

- [ ] **Step 1: Write research.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Research &amp; Talks — Dr. Marc Bravin</title>
  <link rel="stylesheet" href="assets/style.css">
</head>
<body>

<aside class="sidebar">
  <div class="sidebar-photo">
    <img src="assets/foto_marc_bravin.jpeg" alt="Dr. Marc Bravin">
  </div>
  <h1>Dr. Marc Bravin</h1>
  <p class="subtitle">
    CTO &amp; Co-Founder at <span>Gopf AG</span><br>
    AI Researcher · Lecturer at HSLU
  </p>
  <nav>
    <a href="index.html">About</a>
    <a href="work.html">Work Experience</a>
    <a href="research.html" class="active">Research &amp; Talks</a>
    <a href="projects.html">Projects</a>
    <a href="press.html">Press &amp; Awards</a>
    <a href="contact.html">Contact</a>
  </nav>
  <div class="sidebar-links">
    <a href="https://www.linkedin.com/in/marc-bravin" target="_blank"><span class="dot"></span>linkedin.com/in/marc-bravin</a>
    <a href="https://gopf.com" target="_blank"><span class="dot"></span>gopf.com</a>
    <a href="mailto:marc.bravin@gopf.com"><span class="dot"></span>marc.bravin@gopf.com</a>
  </div>
</aside>

<main class="main">
  <p class="section-label">Research &amp; Talks</p>
  <h1 class="page-title">Publications, Talks &amp; Teaching</h1>

  <!-- Under Review -->
  <div class="pub-section">
    <div class="pub-section-title">Under Review</div>
    <div class="featured-paper">
      <span class="paper-badge">Journal of Marketing · 4th Round</span>
      <div class="paper-title">How to Follow Social Media Trends? An Empirical Investigation Using TikTok Short Video Data</div>
      <div class="paper-authors">Bravin, M., Clegg, M., Hofstetter, R., Pouly, M. &amp; Berger, J.A. (2025)</div>
      <div class="paper-meta">
        Multimodal video analytics (MUVID) across 57,000+ TikTok videos. Key finding: atypical trend videos receive more engagement — especially as trends mature. Follow-up experiments confirm causal impact. ·
        <a href="https://papers.ssrn.com/sol3/papers.cfm?abstract_id=5117564" target="_blank">SSRN ↗</a> · 1,215 downloads
      </div>
    </div>
  </div>

  <!-- Journal Articles -->
  <div class="pub-section">
    <div class="pub-section-title">Journal Articles</div>
    <div class="pub-entry">
      <div class="pub-title">Human-Machine Creativity: How AI Can Influence Human Creativity in Open Innovation</div>
      <div class="pub-authors">Clegg, M., Hofstetter, R., Blohm, I. &amp; Bravin, M. (2022)</div>
      <div class="pub-venue">Marketing Review St. Gallen</div>
    </div>
  </div>

  <!-- Conference Papers -->
  <div class="pub-section">
    <div class="pub-section-title">Peer-Reviewed Conference Papers</div>

    <div class="pub-entry">
      <div class="pub-title">AI Creativity: Studying the Effects of Similarity in Co-Work with Generative Artificial Intelligence</div>
      <div class="pub-authors">Clegg, M., Bravin, M., Hofstetter, R., Fuchs, C. &amp; Schamp, C. (2024)</div>
      <div class="pub-venue">European Marketing Academy Conference (EMAC), Bucharest, Romania</div>
    </div>
    <div class="pub-entry">
      <div class="pub-title">AI Creativity: How Solution Dissimilarity Harms AI Usage and Idea Selection</div>
      <div class="pub-authors">Clegg, M., Bravin, M., Hofstetter, R. &amp; Fuchs, C. (2023)</div>
      <div class="pub-venue">Association for Consumer Research (ACR), Seattle, Washington</div>
    </div>
    <div class="pub-entry">
      <div class="pub-title">Trend Following: How Content Prototypicality Drives Liking on TikTok</div>
      <div class="pub-authors">Bravin, M., Clegg, M., Hofstetter, R., Pouly, M. &amp; Berger, J. (2023)</div>
      <div class="pub-venue">EMAC Conference, Odense, Denmark</div>
    </div>
    <div class="pub-entry">
      <div class="pub-title">Should You Really be Creative on Social Media? A Machine Learning Approach to Examine Originality of Video Content from TikTok</div>
      <div class="pub-authors">Bravin, M., Clegg, M., Hofstetter, R., Pouly, M. &amp; Berger, J. (2022)</div>
      <div class="pub-venue">Association for Consumer Research (ACR), Denver, Colorado</div>
    </div>
    <div class="pub-entry">
      <div class="pub-title">Minimal Hand Pose Estimation for Touchable Projector-Depth Systems</div>
      <div class="pub-authors">Bürli, A., Bravin, M., Beck, M. &amp; Koller, T. (2022)</div>
      <div class="pub-venue">9th Swiss Conference on Data Science (SDS), IEEE</div>
    </div>
    <div class="pub-entry">
      <div class="pub-title">Does it help to be creative on TikTok?</div>
      <div class="pub-authors">Bravin, M., Clegg, M., Hofstetter, R., Pouly, M. &amp; Berger, J. (2022)</div>
      <div class="pub-venue">ISMS Marketing Science Conference, Chicago, Illinois</div>
    </div>
    <div class="pub-entry">
      <div class="pub-title">Does it help to be creative on Social Media? A Machine Learning Approach to examine Originality of Video Content from TikTok</div>
      <div class="pub-authors">Bravin, M., Clegg, M., Hofstetter, R., Pouly, M. &amp; Berger, J. (2022)</div>
      <div class="pub-venue">EMAC Conference, Budapest, Hungary</div>
    </div>
    <div class="pub-entry">
      <div class="pub-title">Does It Help to Be Creative on Social Media? The Value of Originality for User-Generated Content</div>
      <div class="pub-authors">Bravin, M., Clegg, M., Hofstetter, R., Pouly, M. &amp; Berger, J. (2022)</div>
      <div class="pub-venue">Society of Consumer Psychology (SCP) Annual Conference, Nashville, Tennessee</div>
    </div>
    <div class="pub-entry">
      <div class="pub-title">Does it help to be creative on Social Media?</div>
      <div class="pub-authors">Bravin, M., Clegg, M., Hofstetter, R., Pouly, M. &amp; Berger, J. (2022)</div>
      <div class="pub-venue">AMA Educators Proceedings Vol. 32, AMA Winter Conference, Las Vegas, Nevada</div>
    </div>
    <div class="pub-entry">
      <div class="pub-title">Towards Crafting Beer with Artificial Intelligence</div>
      <div class="pub-authors">Bravin, M., Pfäffli, D., Kuhn, K. &amp; Pouly, M. (2021)</div>
      <div class="pub-venue">8th Swiss Conference on Data Science (SDS), pp. 54–55, IEEE</div>
    </div>
    <div class="pub-entry">
      <div class="pub-title">Should You Really be Creative on Social Media? An Empirical Investigation of Video Content from TikTok</div>
      <div class="pub-authors">Bravin, M., Clegg, M., Hofstetter, R., Pouly, M. &amp; Berger, J. (2021)</div>
      <div class="pub-venue">Association for Consumer Research (ACR), Seattle, Washington</div>
    </div>
    <div class="pub-entry">
      <div class="pub-title">Should You Really be Creative on Social Media? An Empirical Investigation of User-Generated Content from TikTok</div>
      <div class="pub-authors">Clegg, M., Hofstetter, R., Bravin, M. &amp; Pouly, M. (2021)</div>
      <div class="pub-venue">EMAC Conference, 50th Edition, Madrid, Spain</div>
    </div>
    <div class="pub-entry">
      <div class="pub-title">Automated Smartification of Notices to Airmen</div>
      <div class="pub-authors">Bravin, M., Pfäffli, D., Mazumder, S. &amp; Pouly, M. (2020)</div>
      <div class="pub-venue">7th Swiss Conference on Data Science (SDS), pp. 51–52, IEEE</div>
    </div>
  </div>

  <!-- Invited Talks -->
  <div class="pub-section">
    <div class="pub-section-title">Invited Talks &amp; Presentations</div>
    <div class="pub-entry">
      <div class="pub-title">Quantifying Video Content: An Application to Content Atypicality on TikTok</div>
      <div class="pub-venue">Theory + Practice in Marketing (TPM) Conference, HEC Lausanne, Switzerland · May 2023</div>
    </div>
    <div class="pub-entry">
      <div class="pub-title">AI Overstimulation: How Generative AI Can Harm or Help Human Creativity</div>
      <div class="pub-venue">TPM Conference, HEC Lausanne, Switzerland · May 2023</div>
    </div>
    <div class="pub-entry">
      <div class="pub-title">Meme Coin Marketing: How Anticipation Triggers Value in Valueless Markets</div>
      <div class="pub-venue">International Conference on Crypto-Marketing, Columbia Business School, New York City · December 2022</div>
    </div>
    <div class="pub-entry">
      <div class="pub-title">AI in the Food Innovation Process</div>
      <div class="pub-venue">Swiss Food Research, 9th Meeting of the IG Digitalization, ETH Zurich · November 2022</div>
    </div>
    <div class="pub-entry">
      <div class="pub-title">Should You Really Be Creative on Social Media?</div>
      <div class="pub-venue">Swiss Academy of Marketing Science (SAMS), University of Lucerne · October 2021</div>
    </div>
  </div>

  <!-- Patent -->
  <div class="pub-section">
    <div class="pub-section-title">Patent</div>
    <div class="pub-entry">
      <div class="pub-title">Interactive Display Apparatus and Method for Operating the Same</div>
      <div class="pub-authors">Julen, L. &amp; Bravin, M. · US11809662B2 · Abusizz AG</div>
      <div class="pub-venue">Filed: March 2021 · Granted: November 2023</div>
    </div>
  </div>

  <!-- Teaching -->
  <div class="pub-section">
    <div class="pub-section-title">Teaching</div>
    <div class="table-wrap">
      <table class="awards-table">
        <thead>
          <tr>
            <th>Role</th>
            <th>Institution</th>
            <th>Period</th>
            <th>Details</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>Lecturer (Deep Learning)</td>
            <td>HSLU, Dept. of Business</td>
            <td>Mar 2025–present</td>
            <td>Master's program, 3 ECTS</td>
          </tr>
          <tr>
            <td>Guest Lecturer (Intro to AI/ML)</td>
            <td>HSLU, Dept. of Computer Science</td>
            <td>Mar 2022–present</td>
            <td>"Informatik &amp; Gesellschaft", Master's, 3 ECTS</td>
          </tr>
          <tr>
            <td>Lecturer (AI for Content Marketing)</td>
            <td>HSLU, International Summer School</td>
            <td>Sep 2023</td>
            <td>Bachelor's, 3 ECTS</td>
          </tr>
          <tr>
            <td>Teaching Assistant (ML)</td>
            <td>HSLU</td>
            <td>Sep 2018–Feb 2021</td>
            <td>Exercise preparation for ML course, Bachelor's, 3 ECTS</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>

</main>
</body>
</html>
```

- [ ] **Step 2: Open in browser and verify**

```bash
open research.html
```

Check: featured paper box has teal border, "Under Review" badge visible, SSRN link works, all sections separated cleanly.

- [ ] **Step 3: Commit**

```bash
git add research.html
git commit -m "feat: add research and talks page"
```

---

## Task 6: Projects Page (projects.html)

**Files:**
- Create: `projects.html`

- [ ] **Step 1: Write projects.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Projects — Dr. Marc Bravin</title>
  <link rel="stylesheet" href="assets/style.css">
</head>
<body>

<aside class="sidebar">
  <div class="sidebar-photo">
    <img src="assets/foto_marc_bravin.jpeg" alt="Dr. Marc Bravin">
  </div>
  <h1>Dr. Marc Bravin</h1>
  <p class="subtitle">
    CTO &amp; Co-Founder at <span>Gopf AG</span><br>
    AI Researcher · Lecturer at HSLU
  </p>
  <nav>
    <a href="index.html">About</a>
    <a href="work.html">Work Experience</a>
    <a href="research.html">Research &amp; Talks</a>
    <a href="projects.html" class="active">Projects</a>
    <a href="press.html">Press &amp; Awards</a>
    <a href="contact.html">Contact</a>
  </nav>
  <div class="sidebar-links">
    <a href="https://www.linkedin.com/in/marc-bravin" target="_blank"><span class="dot"></span>linkedin.com/in/marc-bravin</a>
    <a href="https://gopf.com" target="_blank"><span class="dot"></span>gopf.com</a>
    <a href="mailto:marc.bravin@gopf.com"><span class="dot"></span>marc.bravin@gopf.com</a>
  </div>
</aside>

<main class="main">
  <p class="section-label">Projects</p>
  <h1 class="page-title">Notable Work</h1>

  <div class="project-grid">

    <div class="project-card">
      <div class="project-tag">2023 – Present</div>
      <div class="project-title">Gopf AG — AI-Powered Competitive Intelligence Platform</div>
      <div class="project-desc">Co-founded and built from scratch: a B2B SaaS platform for competitive and market intelligence powered by NLP and Agentic AI. Full-stack: cloud infrastructure, ML pipelines, and frontend. Helps businesses make better-informed strategic decisions.</div>
    </div>

    <div class="project-card">
      <div class="project-tag">2025</div>
      <div class="project-title">Swiss AI Jobs Report 2025</div>
      <div class="project-desc">Co-authored the Swiss AI Jobs Report 2025 in collaboration with HSLU, analyzing the Swiss AI labor market. Widely covered in Swiss media and released September 2025.</div>
    </div>

    <div class="project-card">
      <div class="project-tag">2021 – 2025 · PhD Research</div>
      <div class="project-title">TikTok Content Originality — Multimodal Video Analytics</div>
      <div class="project-desc">Developed a machine learning pipeline (MUVID) to quantify originality in short-form video content on TikTok using multimodal embeddings across 57,000+ videos. Key finding: being too original hurts engagement — audiences prefer prototypical content. Under review at Journal of Marketing.</div>
    </div>

    <div class="project-card">
      <div class="project-tag">2020 · First in Switzerland</div>
      <div class="project-title">AI Beer Brewing — "Deeper"</div>
      <div class="project-desc">In collaboration with HSLU, Jaywalker Digital, and craft brewery MN Brew, developed the first AI-brewed beer in Switzerland. Neural networks trained on ~67,000 international beer recipes generated novel brewable recipes. The beer "Deeper" was commercially sold by MN Brew. Covered by Communications of the ACM.</div>
    </div>

    <div class="project-card">
      <div class="project-tag">2021</div>
      <div class="project-title">AI-Generated Christmas Cookies for Betty Bossi</div>
      <div class="project-desc">Used generative AI trained on recipe data to create novel Guetzli (cookie) recipes, in collaboration with Betty Bossi and HSLU. Widely covered in Swiss media including Luzerner Zeitung and Die Welt.</div>
    </div>

    <div class="project-card">
      <div class="project-tag">2020</div>
      <div class="project-title">NOTAM Automation</div>
      <div class="project-desc">Automated Smartification of Notices to Airmen (NOTAMs) using NLP and ML to convert unstructured aviation notices into structured, queryable data. Presented at the 7th Swiss Conference on Data Science (IEEE).</div>
    </div>

    <div class="project-card">
      <div class="project-tag">2022</div>
      <div class="project-title">Hand Pose Estimation for Touchable Projectors</div>
      <div class="project-desc">Minimal hand pose estimation system for touchable projector-depth systems, enabling gesture-based interaction with projected surfaces. Presented at the 9th IEEE Swiss Conference on Data Science.</div>
    </div>

  </div>
</main>
</body>
</html>
```

- [ ] **Step 2: Open in browser and verify**

```bash
open projects.html
```

Check: 2-column card grid renders, hover effect adds teal border, "Projects" nav active.

- [ ] **Step 3: Commit**

```bash
git add projects.html
git commit -m "feat: add projects page"
```

---

## Task 7: Press & Awards Page (press.html)

**Files:**
- Create: `press.html`

- [ ] **Step 1: Write press.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Press &amp; Awards — Dr. Marc Bravin</title>
  <link rel="stylesheet" href="assets/style.css">
</head>
<body>

<aside class="sidebar">
  <div class="sidebar-photo">
    <img src="assets/foto_marc_bravin.jpeg" alt="Dr. Marc Bravin">
  </div>
  <h1>Dr. Marc Bravin</h1>
  <p class="subtitle">
    CTO &amp; Co-Founder at <span>Gopf AG</span><br>
    AI Researcher · Lecturer at HSLU
  </p>
  <nav>
    <a href="index.html">About</a>
    <a href="work.html">Work Experience</a>
    <a href="research.html">Research &amp; Talks</a>
    <a href="projects.html">Projects</a>
    <a href="press.html" class="active">Press &amp; Awards</a>
    <a href="contact.html">Contact</a>
  </nav>
  <div class="sidebar-links">
    <a href="https://www.linkedin.com/in/marc-bravin" target="_blank"><span class="dot"></span>linkedin.com/in/marc-bravin</a>
    <a href="https://gopf.com" target="_blank"><span class="dot"></span>gopf.com</a>
    <a href="mailto:marc.bravin@gopf.com"><span class="dot"></span>marc.bravin@gopf.com</a>
  </div>
</aside>

<main class="main">
  <p class="section-label">Press &amp; Awards</p>
  <h1 class="page-title">Media &amp; Recognition</h1>

  <!-- TV & Video -->
  <div class="press-section">
    <div class="press-section-title">TV &amp; Video</div>
    <div class="press-item">
      <div class="press-year">2025</div>
      <div>
        <div class="press-outlet">SRF Kassensturz (TV)</div>
        <div class="press-topic">Schöne neue KI Welt — interviewed about AI and society</div>
      </div>
    </div>
    <div class="press-item">
      <div class="press-year">2023</div>
      <div>
        <div class="press-outlet">Digital Festival Basel</div>
        <div class="press-topic">Invited speaker/presenter</div>
      </div>
    </div>
  </div>

  <!-- Radio & Podcast -->
  <div class="press-section">
    <div class="press-section-title">Radio &amp; Podcast</div>
    <div class="press-item">
      <div class="press-year">2022</div>
      <div>
        <div class="press-outlet">SRF News Plus (Radio/Podcast)</div>
        <div class="press-topic">Hype um die App «Lensa» und die Kritik an Künstlicher Intelligenz — expert commentary on AI image generation and ethics</div>
      </div>
    </div>
  </div>

  <!-- Print & Online -->
  <div class="press-section">
    <div class="press-section-title">Print &amp; Online</div>
    <div class="press-item">
      <div class="press-year">2025</div>
      <div>
        <div class="press-outlet">HSLU / Swiss AI Jobs Report</div>
        <div class="press-topic">Co-authored the Swiss AI Jobs Report 2025</div>
      </div>
    </div>
    <div class="press-item">
      <div class="press-year">2021</div>
      <div>
        <div class="press-outlet">Communications of the ACM</div>
        <div class="press-topic">AI Helps Craft New Beers</div>
      </div>
    </div>
    <div class="press-item">
      <div class="press-year">2021</div>
      <div>
        <div class="press-outlet">Forschungsmosaik (Swissuniversities)</div>
        <div class="press-topic">Künstliche Intelligenz: (K)ein einfaches Rezept</div>
      </div>
    </div>
    <div class="press-item">
      <div class="press-year">2021</div>
      <div>
        <div class="press-outlet">Luzerner Zeitung</div>
        <div class="press-topic">Weihnachtsguetzli dank Künstlicher Intelligenz</div>
      </div>
    </div>
    <div class="press-item">
      <div class="press-year">2021</div>
      <div>
        <div class="press-outlet">Hotellerie Gastronomie Magazin</div>
        <div class="press-topic">KI schreibt Rezepte — interview on AI beer and food recipes</div>
      </div>
    </div>
    <div class="press-item">
      <div class="press-year">2020</div>
      <div>
        <div class="press-outlet">Die Welt</div>
        <div class="press-topic">In der Zukunft kommt der Arztbericht von der KI</div>
      </div>
    </div>
    <div class="press-item">
      <div class="press-year">2020</div>
      <div>
        <div class="press-outlet">Die Welt</div>
        <div class="press-topic">i-Dötzchen Computer – Auch Kochrezepte helfen dabei, Rechnersystemen das Schreiben anzutrainieren</div>
      </div>
    </div>
  </div>

  <!-- Awards -->
  <p class="section-label" style="margin-top: 48px;">Awards &amp; Honours</p>
  <div class="table-wrap">
    <table class="awards-table">
      <thead>
        <tr>
          <th>Year</th>
          <th>Award</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>2022</td>
          <td>Best Poster Video Award — Swiss Conference on Data Science</td>
        </tr>
        <tr>
          <td>2022</td>
          <td>Best Paper in Big Data, Analytics, AI &amp; Machine Learning Track — AMA Winter Academic Conference</td>
        </tr>
        <tr>
          <td>2021</td>
          <td>Award for the Best Master's Thesis in Computer Science — HSLU</td>
        </tr>
        <tr>
          <td>2018</td>
          <td>Member of the Lucerne University of Applied Sciences and Arts' Dean's List</td>
        </tr>
        <tr>
          <td>2014</td>
          <td>Awarded Apprenticeship Graduation (top grade, 5.7/6)</td>
        </tr>
      </tbody>
    </table>
  </div>

</main>
</body>
</html>
```

- [ ] **Step 2: Open in browser and verify**

```bash
open press.html
```

Check: press items render with year column, awards table renders cleanly, "Press & Awards" nav active.

- [ ] **Step 3: Commit**

```bash
git add press.html
git commit -m "feat: add press and awards page"
```

---

## Task 8: Contact Page (contact.html)

**Files:**
- Create: `contact.html`

- [ ] **Step 1: Write contact.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Contact — Dr. Marc Bravin</title>
  <link rel="stylesheet" href="assets/style.css">
</head>
<body>

<aside class="sidebar">
  <div class="sidebar-photo">
    <img src="assets/foto_marc_bravin.jpeg" alt="Dr. Marc Bravin">
  </div>
  <h1>Dr. Marc Bravin</h1>
  <p class="subtitle">
    CTO &amp; Co-Founder at <span>Gopf AG</span><br>
    AI Researcher · Lecturer at HSLU
  </p>
  <nav>
    <a href="index.html">About</a>
    <a href="work.html">Work Experience</a>
    <a href="research.html">Research &amp; Talks</a>
    <a href="projects.html">Projects</a>
    <a href="press.html">Press &amp; Awards</a>
    <a href="contact.html" class="active">Contact</a>
  </nav>
  <div class="sidebar-links">
    <a href="https://www.linkedin.com/in/marc-bravin" target="_blank"><span class="dot"></span>linkedin.com/in/marc-bravin</a>
    <a href="https://gopf.com" target="_blank"><span class="dot"></span>gopf.com</a>
    <a href="mailto:marc.bravin@gopf.com"><span class="dot"></span>marc.bravin@gopf.com</a>
  </div>
</aside>

<main class="main">
  <p class="section-label">Contact</p>
  <h1 class="page-title">Get in touch</h1>

  <p class="lead" style="margin-bottom: 40px;">
    I'm always open to conversations about AI research, startup collaboration, consulting, 
    speaking engagements, or just an interesting idea. Based in Zürich, Switzerland.
  </p>

  <div class="contact-grid">
    <div class="contact-item">
      <span class="contact-label">Email</span>
      <a href="mailto:marc.bravin@gopf.com">marc.bravin@gopf.com</a>
    </div>
    <div class="contact-item">
      <span class="contact-label">LinkedIn</span>
      <a href="https://www.linkedin.com/in/marc-bravin" target="_blank">linkedin.com/in/marc-bravin</a>
    </div>
    <div class="contact-item">
      <span class="contact-label">Company</span>
      <a href="https://gopf.com" target="_blank">gopf.com</a>
    </div>
    <div class="contact-item">
      <span class="contact-label">Location</span>
      <span>Zürich, Switzerland</span>
    </div>
  </div>
</main>
</body>
</html>
```

- [ ] **Step 2: Open in browser and verify**

```bash
open contact.html
```

Check: links render in teal, "Contact" nav active, layout clean.

- [ ] **Step 3: Commit**

```bash
git add contact.html
git commit -m "feat: add contact page"
```

---

## Task 9: Full Site Verification

- [ ] **Step 1: Verify all navigation links work**

Open `index.html` in browser and click every nav link in sequence:
- About → Work Experience → Research & Talks → Projects → Press & Awards → Contact
- Verify active state updates on each page (teal text + dark bg)
- Verify sidebar photo loads on all pages

- [ ] **Step 2: Verify all external links**

On `index.html`: right-click LinkedIn, gopf.com, email links — confirm correct URLs.
On `research.html`: click SSRN link — should open `https://papers.ssrn.com/sol3/papers.cfm?abstract_id=5117564`.

- [ ] **Step 3: Verify responsive layout at mobile width**

In browser DevTools (F12), toggle device toolbar and set width to 375px. Check:
- Sidebar stacks to top, not fixed
- Navigation links wrap horizontally
- Content padding reduces appropriately
- Highlight cards stack to 2 columns

- [ ] **Step 4: Final commit**

```bash
git add -A
git status
# Verify nothing unexpected is staged
git commit -m "feat: complete personal website — 6-page plain HTML/CSS site"
```

---

## Spec Coverage Check

| Spec Requirement | Covered In |
|---|---|
| Dark sidebar #0f1117, teal #2ab4a0 | Task 2 (style.css) |
| Profile photo 120px circle with teal border | Task 2, Task 3 |
| Multi-page structure, fixed sidebar | All tasks |
| About: hero, bio, badges, highlight cards, recent feed | Task 3 |
| Work: full timeline with all 9 roles + education | Task 4 |
| Research: under review paper (JM 4th round), journal, 13 conference papers, 5 talks, patent, teaching | Task 5 |
| Projects: 7 project cards | Task 6 |
| Press: TV, radio, print + awards table | Task 7 |
| Contact: email, LinkedIn, Gopf, location | Task 8 |
| Responsive at 768px | Task 2 (CSS) + Task 9 |
| `.gitignore` with `.superpowers/` | Task 1 |
