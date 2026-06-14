# Kington Education Website — Agent Instructions

## Scope

Use these instructions for all work inside the `kington-education-website`
folder.

First read `../CLAUDE.md` for Kington Education's business-wide context,
approval requirements, claims discipline, and offer direction. This file adds
website-specific guidance. If the two files conflict, follow the more cautious
rule and flag the conflict to Connor.

## What This Folder Contains

The website is a single static HTML file (`index.html`) with a JavaScript
page router — no build step, no framework. All pages (Home, Services, About,
Partners, Contact, Projects) live in that file as hidden `<div class="page">`
sections that are shown or hidden by the router.

Folder layout:

```
kington-education-website/
├── index.html             # Single source of truth — HTML + CSS + JS
├── .htaccess              # SPA fallback rewrites for the JS page router
├── .gitignore             # Excludes .claude/, .DS_Store, etc.
├── CLAUDE.md              # This file
├── README.md              # Public-facing project overview
└── assets/
    ├── img/               # Logos, hero shots, carousel images
    └── video/             # Four background videos (home/services/about/partners)
```

The four `assets/video/*.mp4` files are scroll-scrubbed cinematic backgrounds
that form one continuous journey: schoolhouse approach → door opens to
classroom → round-table window → out the window to the floating K logo.
Each video is encoded with all-keyframes for smooth scrub seeking.

The design system uses:

- Fonts: Hanken Grotesk (display/headings), Mulish (body), JetBrains Mono
  (code/labels) — loaded from Google Fonts.
- Colour tokens: green-900 through green-50 scale, plus bg, surface, ink,
  muted, amber.
- Cards: two patterns share a unified spec via CSS variables
  (`--card-pad-scan`, `--card-pad-read`, `--card-radius`, etc.):
  `.card` (light, scan items) and `.partner-card` / `.testimonial-card` /
  `.research` (dark green, stop-and-read).
- Animations: hero blob drift, scroll reveal with micro-blur + micro-rotate,
  page-entrance choreography on navigation, scene-settle blur-resolve on the
  active background video, 3D parallax tilt on heavy cards, first-visit
  cinematic emergence gated by `localStorage.kington_visited` (`?skip=1` to
  bypass).

## Primary Conversion Actions

The website has two intended actions for interested schools:

1. **Get the demo video** — the primary CTA. A form captures name, role,
   school, email, pupil count, school type, focus areas, and specific
   concerns. On submit, a personalised demo video should be sent to the
   school's inbox.
2. **Book a 15-minute call** — the secondary CTA. Links to
   `contact.html#book`.

These two routes should remain the only conversion paths. Do not add
competing CTAs or unrelated links.

## Claims And Content Rules

All product claims, statistics, testimonials, and school examples on the
website must meet the same standards as campaign copy.

Use
`../Maths Whizz email campaign/01 Product Evidence and Claims/Maths-Whizz Product Evidence Bank.md`
as the controlled source before adding or editing any claim.

Current claims used on the site (verify these remain approved):

- "+18 months Maths Age in first year" — attributed to Whizz Education
  research with 12,000+ students, 45–60 min/week usage condition.
- "National Curriculum aligned from Reception to Year 8." (The earlier "98% UK
  curriculum aligned" wording was retired on 12 June 2026 — the Maths-Whizz
  curriculum page actually gives Reception–Year 6 100% and Year 8 96%, so the
  rounded 98% figure was inaccurate.)
- "Independent EEF evaluation published June 2026" — check this claim when
  the report status changes.

Testimonials currently shown:

- Kim Rogers, Director of Maths, Crofty MAT.
- Mandy Jones, Executive Head, Criftins CofE Primary, Shropshire.
- Lisa Tipping, William Gilbert Endowed CofE Primary & Nursery.

Do not add new testimonials without Connor's approval and confirmed
attribution.

## Form Backend

The demo request form (both instances — home page and contact page) submits
via AJAX to **FormSubmit.co**, a free email-relay service. The endpoint is
`https://formsubmit.co/ajax/connor.malone@kingtoneducation.com` and the form
includes hidden `_subject`, `_cc` (Paul), and `_template` fields so the email
arrives nicely formatted as a table.

User flow: validate → POST in background → show inline success message
("On its way, {name}!"). Network failures still surface the success message
so the user isn't blocked; failures are logged to the browser console.

Status as of 14 June 2026: FormSubmit.co activated by Connor on first
test submission. No HubSpot integration yet — leads currently arrive only
as email. A future round may add a HubSpot Forms API POST alongside the
FormSubmit relay so leads also land in the CRM. Do not add HubSpot
integration without Connor's explicit approval per the approval rules
below.

## Approval Rules

Ask Connor before:

- Publishing or deploying any website change.
- Adding, editing, or removing any claim, statistic, or testimonial.
- Changing the conversion flow or adding new CTAs.
- Connecting the form to HubSpot or any external service.

Local edits to `index.html` for review are allowed when Connor requests them.
Do not push or deploy without explicit approval.

## Development Notes

- No build step. Edit `index.html` directly.
- The page router is driven by `data-page` query params and anchor links.
  Internal links use `href="services.html"` style paths — the router
  intercepts these and shows the matching page section.
- The `.reveal` / `.in` scroll animation system uses IntersectionObserver.
- Stat number animation uses `data-count`, `data-prefix`, `data-suffix`
  attributes on `.stat-num` elements.
- Video placeholders use `.ph.video` with `data-video` — clicking opens a
  lightbox embedding a YouTube video.
- The four scroll-scrubbed background videos are driven by a single engine
  that polls for which page is visible, lerps `currentTime` based on scroll
  fraction, and applies a smoothstep curve for "linger on the opening +
  closing frames" pacing. Per-video bias via `data-bias` on the
  `<video>` element (services uses `data-bias="0.18"` so the door swings
  open a touch earlier).
- The local preview server in `.claude/range_server.py` serves the four
  videos with `Accept-Ranges` headers so `<video currentTime>` seeking
  works locally. Python's stdlib `http.server` does not support range
  requests and breaks video scrubbing. The standard `preview_start` tool
  may need the launch config renamed before it picks up the change.

## Deployment

The website is deployed to **Hostinger** (Business plan) via Hostinger's
GitHub auto-deploy integration. Pushing to `main` triggers an automatic
deploy to `public_html` within ~30 seconds.

Live domain: `https://kingtoneducation.com`
Repo: `https://github.com/connorcmalone/kington-education-website`

There is no Vercel deployment serving the live domain anymore. Any
remaining Vercel deployments live only at `.vercel.app` URLs and are not
the primary production target.
