# Portfolio Build Spec — GitHub Pages

Hand this file to Claude Code as the brief. Read it fully before writing any code.

---

## 1. Purpose

A static personal site that does three jobs, in priority order:

1. **Convince a hiring manager in 20 seconds** that I build production ML and agentic systems, not coursework.
2. **Give a recruiter or professor a skimmable, linkable record** — projects, publications, resume, contact.
3. **Be a durable home for writeups** so links I put in applications and outreach don't rot.

Primary audience: ML/data science hiring managers and technical recruiters. Secondary: research faculty and collaborators. Tertiary: people who found me via LinkedIn.

Design implication: **the landing view must work without scrolling and without JS.** Name, one-line positioning, three proof points, resume link, contact. Everything else is depth for people who want it.

---

## 2. Stack and GitHub Pages constraints

Prefer **Astro** (or plain HTML + a little CSS if the project stays small). Avoid a heavy SPA — this is a content site, and client-side routing hurts sharing, SEO, and first paint.

Hard constraints of the platform, do not get these wrong:

- **Repo choice.** `<username>.github.io` deploys at the domain root — no base path, simplest option. Any other repo name deploys under `/<repo>/`, which means `base` must be set in the build config and **every internal link and asset path must respect it**. Decide this first and write it at the top of the README.
- **Deploy via GitHub Actions**, not the legacy branch-publish, if there's a build step. Add a workflow that builds on push to `main` and publishes the artifact.
- **Add `.nojekyll`** to the output root. Without it, GitHub strips directories starting with `_`, which silently breaks Astro/Vite asset folders.
- **Add `404.html`** at the root. GitHub Pages serves it for unknown paths.
- **No server.** No API routes, no secrets, no server-side form handling. A contact form needs a third-party endpoint (Formspree or similar) or should just be a `mailto:` link. Default to `mailto:` — fewer moving parts, nothing to break.
- **Custom domain**: if used, add `CNAME` to the output root (and to `public/` so it survives rebuilds), then enable "Enforce HTTPS."
- **Case-sensitive paths.** Pages is case-sensitive; local macOS/Windows filesystems often aren't. Lowercase every filename and link.
- **Everything committed is public.** No draft resumes with a home address, no scraped data, no `.env`.

---

## 3. Site map

```
/                    home — positioning, featured work, contact
/projects            all projects, filterable by domain
/projects/<slug>     one page per major project (deep dive)
/research            publications, posters, research roles
/about               longer bio, timeline, community work
/resume.pdf          static file, versioned
/404.html
```

Keep it to these. A blog is optional — only scaffold `/writing` if there are two finished posts ready to ship. An empty blog with "coming soon" actively hurts.

---

## 4. Content spec

Use the real content below. Do not write placeholder lorem, and do not invent metrics, dates, employers, or paper titles — if a number is needed and isn't in this file, leave a `TODO(rahul):` marker instead.

### 4.1 Positioning line (home hero)

The through-line across my work is **applied ML on messy, high-stakes real-world data, plus the agent infrastructure to operationalize it.** Write the hero copy from that, not from a job title. Two candidate directions, pick one and commit:

- Domain-first: biomedical and institutional data → models that get used.
- Systems-first: I build the pipeline, the model, and the agent that runs it.

Avoid: "passionate about leveraging data to drive insights." Avoid any sentence with "passionate," "leveraging," or "cutting-edge."

### 4.2 Facts to render (verify each against my resume before publishing)

**Current**
- M.S., Engineering Data Science & AI — University of Houston
- Graduate Research Assistant — UH Office of Institutional Research
- Based in Houston, TX

**Education**
- B.S., Biomedical Engineering & Data Science — UT Austin

**Research**
- Computational oncology — Oden Institute, UT Austin. Publication in progress. Render as "in preparation" with a `TODO(rahul):` for the title; never list an unpublished paper as published.
- ML / data engineering — EmGenisys. Embryo viability classification from video.

**Credentials**
- Claude Certified Architect – Foundations. Depth: agent design, Claude Agent SDK, MCP, context management.
- AWS Bedrock (model access, quota, deployment)

**Community**
- Founder, Tamil Youth Leadership Program (2017–present)
- Led the effort that got Tamil recognized as a credit language by the Texas Education Agency

### 4.3 Projects

Each project gets a card on `/projects` and a detail page. **Card = 1 line of outcome + 3–5 tech tags + links.** Detail page follows this fixed structure so they're scannable in parallel:

> **Problem** (2 sentences, why it's hard) → **Approach** (what I built, with the real modeling and infra decisions) → **Result** (what it does now, with numbers where I have them) → **What I'd change** (one honest paragraph) → **Links** (repo, live demo, writeup)

That last section is the one most portfolios skip and it's the most convincing part of the page. Keep it.

**Project 1 — Sports forecasting & pricing engine (REV+ / RazzyV)**
XGBoost and Poisson models for WNBA, MLB, and NFL player outcomes; three models deployed on Streamlit; a Discord bot that converts model output to American odds, computes implied probability, and pushes positive-expected-value alerts in real time.

Framing note, and follow it: **lead with the forecasting and market-pricing problem, not with betting.** The transferable skills are probabilistic forecasting, calibration, real-time data pipelines, and comparing a model's price against a market's price. Some employers in healthcare, education, and finance are sensitive to gambling content. Title the page around modeling; mention the sportsbook application plainly in the body, without promotion, without "profit" claims, and without screenshots of wagers. Include a one-line note that it's a personal research project. If a calibration plot or backtest exists, show it — that single chart does more than the whole description.

**Project 2 — Agentic job-search pipeline**
An agent that runs a multi-stage search-and-application workflow. This one is directly on-thesis for the Claude Certified Architect credential and for any agentic-AI role, so give it the most detailed detail page. Show the **architecture** — tool boundaries, context management strategy, where MCP fits, what state persists between runs, what a failure looks like and how it recovers. A diagram beats three paragraphs here.

**Project 3 — Embryo viability classification (EmGenisys)**
Only include what's publicly shareable. No proprietary data, no internal metrics, no model weights. Describe the problem class and my contribution to the ML/data engineering side, and mark anything uncertain with `TODO(rahul): confirm what's cleared to publish.` If in doubt, this becomes a two-line entry under Research instead of a project page.

**Project 4 — Computational oncology research (Oden Institute)**
Lives on `/research`, not `/projects`. Methods and problem framing only until the paper lands.

### 4.4 Resume

Link a PDF at a stable path (`/resume.pdf`) so links in old applications keep working. Keep a dated copy in the repo (`/resume/rahul-resume-2026-08.pdf`) and have `/resume.pdf` be the current one. Strip the home address and personal phone from the public version — city, email, LinkedIn, GitHub only.

---

## 5. Design direction

Do not ship a template. Before writing CSS, produce a short design plan — 4–6 named hex values, a display face and a body face chosen deliberately (not the same pairing you'd reach for on any portfolio), a layout concept, and one signature element the page is remembered by. Then critique that plan: if any part of it is what you'd generate for any generic portfolio prompt, revise it and say what changed.

Specific things to avoid because they are the current defaults:

- Cream `#F4F1EA` background + high-contrast serif + terracotta `#D97757` accent
- Near-black background with a single acid-green or vermilion accent
- Broadsheet layout with hairline rules and zero border-radius
- `01 / 02 / 03` numbered section markers, unless the content is genuinely a sequence
- A gradient blob hero, a typewriter-effect headline, or an animated particle background

Spend the boldness in **one** place and keep everything else quiet. Given the subject matter — models, distributions, calibration, uncertainty — the most honest signature element would come from that world: a real plot rendered as the hero, a live-updating figure, a type treatment that does something with numbers. Ground it in my actual work rather than decorating around it.

Motion: restrained. One orchestrated page-load or scroll reveal, not effects scattered on every element. Respect `prefers-reduced-motion`.

---

## 6. Quality floor

Non-negotiable, verify each before calling it done:

- Responsive to 360px. Test the projects grid and any table or chart specifically.
- Keyboard navigable with visible focus rings. Skip-to-content link.
- Semantic HTML: one `<h1>` per page, real heading hierarchy, `alt` text on every image, landmarks.
- Color contrast ≥ 4.5:1 for body text. Check the accent against its background, don't assume.
- Dark mode via `prefers-color-scheme` if the palette supports it. If it doesn't, skip it — a bad dark mode is worse than none.
- Per-page `<title>` and `<meta name="description">`. Open Graph and Twitter card tags with a real preview image — this is what renders when I paste a link into LinkedIn or a recruiter email, so it matters more than usual.
- `sitemap.xml` and `robots.txt`.
- Self-host fonts or use `font-display: swap`. No render-blocking third-party font call.
- Images: modern format, explicit `width`/`height` to prevent layout shift, lazy-load below the fold.
- No analytics that need a cookie banner. If analytics at all, use a cookieless one.
- Lighthouse ≥ 95 on performance and accessibility. Actually run it.

---

## 7. Repo hygiene

The portfolio repo is itself a work sample — a recruiter who clicks through will see the commit history.

- Real README: what the site is, how to run it locally, how it deploys.
- Meaningful commit messages. No `update`, no `fix stuff`.
- Every linked project repo needs its own README with a screenshot or demo GIF at the top and setup instructions that work. **A dead link or an empty repo is worse than not linking it.** Audit every outbound link before launch.
- Pin the Node version. Commit the lockfile.

---

## 8. Build order

1. Confirm repo name and base path. Write the decision into the README.
2. Scaffold, deploy a nearly empty page, confirm it's live at the right URL. Do not build the whole site before the first successful deploy.
3. Design plan and self-critique (§5). Show it to me before building out the CSS.
4. Home page complete, content real.
5. Projects index + the agentic pipeline detail page (the most important one).
6. Remaining project pages, research, about.
7. Meta tags, OG image, sitemap, 404.
8. Accessibility and Lighthouse pass, link audit, mobile check.

## 9. Acceptance checklist

- [ ] Live at the intended URL over HTTPS
- [ ] No `TODO(rahul):` markers left in shipped pages
- [ ] Every external link resolves, every linked repo has a README
- [ ] Resume PDF loads at `/resume.pdf`, address and phone removed
- [ ] Link preview renders correctly when pasted into LinkedIn or Slack
- [ ] Nothing unpublished is described as published
- [ ] Passes at 360px width and with keyboard only
