# Kington Education website

The marketing website for [Kington Education](https://kingtoneducation.com) —
the UK distribution partner for Maths-Whizz, an adaptive AI maths tutor for
primary and lower-secondary schools.

The site is a single static HTML file with scroll-scrubbed cinematic background
videos forming a four-page autumn journey: from the schoolhouse exterior,
through a door into the Maths-Whizz classroom, across the round-table
window, and out to the Kington K logo.

## Stack

- One static `index.html` (HTML + CSS + JS, no build step, no framework)
- Vanilla page router (data-page attributes, history hash navigation)
- IntersectionObserver-driven scroll reveals
- Custom scroll-scrubbed `<video>` engine with smoothstep pacing
- Asset folders: `assets/img/`, `assets/video/`
- `.htaccess` SPA fallback for direct page URLs

## Local development

```bash
# clone
git clone https://github.com/connorcmalone/kington-education-website.git
cd kington-education-website

# serve locally with Range-request support (needed for video scrubbing)
python3 .claude/range_server.py 8788

# open
open http://localhost:8788
```

Python's stdlib `http.server` will not work for the video scrubbing — it does
not send `Accept-Ranges` headers, so the browser refuses to seek inside the
loaded videos. Use `range_server.py` (included).

## Deployment

Push to `main` and Hostinger auto-deploys to `public_html` within ~30s.

## Form backend

The demo request form submits to **FormSubmit.co**, which emails Connor and
CCs Paul. No HubSpot integration yet.

## Folder map

```
.
├── index.html                  # The site
├── .htaccess                   # SPA fallback rewrites
├── README.md                   # You are here
├── CLAUDE.md                   # Agent instructions for Claude Code
├── .gitignore                  # Excludes .claude/, .DS_Store, etc.
└── assets/
    ├── img/                    # Logos, hero shots, carousel images
    └── video/                  # The four background videos
```
