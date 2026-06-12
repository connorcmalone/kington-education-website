# Kington Education Website — Agent Instructions

## Scope

Use these instructions for all work inside the `kington-education-website`
folder.

First read `../CLAUDE.md` for Kington Education's business-wide context,
approval requirements, claims discipline, and offer direction. This file adds
website-specific guidance. If the two files conflict, follow the more cautious
rule and flag the conflict to Connor.

## What This Folder Contains

The website is built as a single HTML file (`index.html`) with a JavaScript
page router — no build step, no framework. All pages (Home, Services, About,
Partners, Contact, Projects) live in one file as hidden `<div class="page">`
sections that are shown or hidden by the router.

The design system uses:

- Fonts: Hanken Grotesk (display/headings), Mulish (body), JetBrains Mono
  (code/labels) — loaded from Google Fonts.
- Colour tokens: green-900 through green-50 scale, plus bg, surface, ink,
  muted, amber.
- Components: cards, quotes, steps, research block, chips, checklist,
  form-card, paths, cta-band, ribbon, stat-num, scroll reveal (.reveal/.in).
- Animations: hero blob drift, form float, scroll progress bar, stat number
  entrance, lightbox.

Image placeholders use `.ph` divs with `data-label` attributes. These are
stand-ins for real images and should be replaced when assets are available.

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

## Form And HubSpot Integration

The demo request form is currently front-end only — it shows a success message
on submit but does not connect to HubSpot or send anything. The intended
integration is:

- Form submission creates or updates the HubSpot contact and company.
- Connor and Paul are notified.
- Demo request is recorded in HubSpot notes.
- A personalised demo video is sent to the school.

Treat the form backend as a design task until Connor approves the
implementation.

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
  lightbox. No video src is wired yet.
