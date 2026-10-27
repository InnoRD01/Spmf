# Studio Sensorium website

Static site for https://studiosensorium.in. Plain HTML and CSS, no build step.

## Pages
- `index.html`: Home
- `work.html`: Work (placeholder project cards, to replace)
- `about.html`: About (a team section can be added where marked)
- `contact.html`: Contact (mailto links to hello@studiosensorium.in)
- `404.html`: Not-found page

## Preview locally
    cd studiosensorium && python3 -m http.server 8000

## Deploy (Cloudflare Pages)
- Build command: none
- Build output directory: `studiosensorium`

Email runs on Migadu. When pointing the domain at the host, add only the
website records and leave Migadu's MX, SPF, DKIM and DMARC records unchanged.
