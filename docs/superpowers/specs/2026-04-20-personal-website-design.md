# Personal Website Design Spec — Dr. Marc Bravin

**Date:** 2026-04-20  
**Status:** Approved

---

## Context

Marc Bravin is CTO & Co-Founder of Gopf AG, a PhD-holding AI researcher (Summa Cum Laude), and a lecturer at HSLU. He needs a personal website that serves as a comprehensive hub: personal brand, academic profile, and networking landing page in one. The site should feel like the professional extension of Gopf's brand while being warm and human enough to represent the person, not just the CV.

---

## Design Decisions

| Decision | Choice | Rationale |
|---|---|---|
| Tech stack | Plain HTML/CSS/JS | No build tooling, easy to host anywhere, no dependencies to maintain |
| Structure | Multi-page | Volume of content (15+ papers, 6 roles, press, projects) warrants separate pages |
| Layout | Left sidebar (fixed) | Persistent navigation, profile always visible; inspired by kevinkuhn.ch |
| Style | Dark sidebar + white content + teal accent | Directly echoes Gopf's brand identity |
| Tone | Professional but warm | Credentials prominent, writing accessible and human |

---

## Visual Design

### Colors
- **Sidebar background:** `#0f1117` (near-black)
- **Content background:** `#ffffff`
- **Primary accent:** `#2ab4a0` (teal — matches Gopf)
- **Body text:** `#4b5563`
- **Muted text:** `#9ca3af`
- **Borders/dividers:** `#e5e7eb`, `#1e2532` (dark variant for sidebar)
- **Tag backgrounds:** yellow `#fef3c7`, purple `#ede9fe`, green `#d1fae5`

### Typography
- Font: `-apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif`
- Hero headline: 23px, bold, `#111`
- Section labels: 10px, uppercase, letter-spacing 2px, teal
- Body: 15px, 1.85 line-height, `#4b5563`
- Sidebar name: 17px bold, `#f9fafb`
- Sidebar nav: 13px, `#9ca3af` default, teal + `#1e2532` bg when active

### Sidebar (fixed, 280px wide)
- Profile photo: 120px circle, 3px teal border, `foto_marc_bravin.jpeg`
- Name: Dr. Marc Bravin
- Subtitle: CTO & Co-Founder at Gopf AG / AI Researcher · Lecturer at HSLU
- Navigation links (active state: teal text + dark bg)
- Bottom links: LinkedIn, gopf.com, email — each with a teal dot prefix

---

## Pages & Content

### 1. About (`index.html`)
- Section label: "ABOUT"
- Hero headline: *"Building AI that works in the real world — from lab to production."*
- 2-paragraph bio (professional summary from CV)
- Skill badges: Machine Learning, NLP, Computer Vision, Agentic AI, B2B SaaS, Research
- 3 highlight cards (stat boxes):
  - 15+ peer-reviewed publications & conference papers
  - PhD Summa Cum Laude, University of Lucerne
  - 10y+ experience in ML engineering & research
- Recent highlights feed (3 items with colored tags: Press / Research / Project):
  - SRF Kassensturz interview (2025)
  - Swiss AI Jobs Report 2025
  - Journal of Marketing paper (4th round review)

### 2. Work Experience (`work.html`)
- Timeline format with teal left-border for current roles, grey for past
- Entries (chronological, newest first):
  - Gopf AG — CTO & Co-Founder (Feb 2023–Present)
  - University of St. Gallen — Postdoctoral Researcher (Mar–Aug 2025, 40%)
  - HSLU — Lecturer & Deputy Head of Digital Business Lab (Apr 2025–Present)
  - HSLU — Senior Research Associate (Jan 2023–Mar 2025)
  - HSLU — Research Associate (Mar 2021–Dec 2022)
  - HSLU — Research Assistant (Sep 2018–Feb 2021)
  - Jaywalker Digital AG — Data Scientist (Mar 2020–Aug 2023)
  - Network 41 AG — Full-Stack Software Engineer (Aug 2015–Aug 2018)
  - Pilatus Aircraft Ltd — Software Engineer + Apprenticeship (Aug 2010–Jan 2015)
- Each entry: role, company, date range, bullet-point highlights

### 3. Research & Talks (`research.html`)
Subsections:
- **Under Review** (featured, highlighted box):
  - *How to Follow Social Media Trends?* — Journal of Marketing, 4th Round (Jan 2025)  
    Bravin, Clegg, Hofstetter, Pouly & Berger · SSRN: 1,215 downloads
- **Journal Articles:**
  - Clegg, Hofstetter, Blohm & Bravin (2022) — Marketing Review St. Gallen
- **Conference Papers** (14 entries, 2021–2024):
  - EMAC, ACR, AMA, SCP, ISMS, IEEE SDS — full citation list
- **Invited Talks** (5 entries)
- **Patent:**
  - Julen & Bravin — US11809662B2, Interactive Display Apparatus (2023)
- **Teaching:**
  - Table of courses: Deep Learning (HSLU Master's), Intro AI/ML, Summer School, TA roles

### 4. Projects (`projects.html`)
Cards layout (2-col grid):
- **Gopf AG — AI-Powered Competitive Intelligence Platform** (2023–Present)
- **Swiss AI Jobs Report 2025** (with HSLU)
- **TikTok Content Originality** — PhD core research
- **AI Beer Brewing — "Deeper"** (2020) — first AI-brewed beer in Switzerland
- **AI-Generated Christmas Cookies for Betty Bossi** (2021)
- **NOTAM Automation** (2020)
- **Hand Pose Estimation for Touchable Projectors** (2022)

### 5. Press & Awards (`press.html`)
Subsections:
- **TV & Video:** SRF Kassensturz (2025), Digital Festival Basel (2023)
- **Radio & Podcast:** SRF News Plus (2022)
- **Print & Online:** HSLU Swiss AI Jobs Report, Comm. of the ACM, Luzerner Zeitung, Die Welt, etc.
- **Awards table:**
  - Best Poster Video Award — Swiss Conf. on Data Science (2022)
  - Best Paper — AMA Winter Academic Conference (2022)
  - Best Master's Thesis in CS — HSLU (2021)
  - Dean's List — HSLU (2018)
  - Awarded Apprenticeship Graduation (2014)

### 6. Contact (`contact.html`)
- Short intro paragraph
- Links: Email, LinkedIn, Gopf AG
- Location: Zürich, Switzerland

---

## File Structure

```
/
├── index.html          # About
├── work.html           # Work Experience
├── research.html       # Research & Talks
├── projects.html       # Projects
├── press.html          # Press & Awards
├── contact.html        # Contact
├── assets/
│   ├── style.css       # Shared styles (sidebar, nav, layout, components)
│   └── foto_marc_bravin.jpeg
└── .gitignore
```

---

## Shared CSS Components

- `.sidebar` — fixed 280px dark sidebar
- `.sidebar-photo` — 120px circle with teal border
- `.main` — content area with left margin
- `.section-label` — teal uppercase label
- `.timeline-item` — bordered left timeline entry (teal = current, grey = past)
- `.highlight-card` — stat box with large teal number
- `.badge` — pill tag (skills)
- `.recent-tag` — colored category tag (press/research/project)
- `.project-card` — card with title, date, description
- `.publication-entry` — citation block with optional badge

---

## Hosting

Plain HTML — deployable to GitHub Pages, Netlify, or any static host. No build step required. Suggested domain: `marcbravin.ch` or `marc-bravin.com`.

---

## Verification

1. Open `index.html` in browser — photo appears, teal accent consistent, nav links work
2. Navigate all 6 pages — sidebar stays fixed, active nav item highlights correctly
3. Resize to mobile — sidebar collapses or stacks (responsive breakpoint at 768px)
4. Check all external links: LinkedIn, gopf.com, email mailto
5. Verify Journal of Marketing paper appears under Review with correct SSRN link
6. Confirm photo loads from `assets/foto_marc_bravin.jpeg`
