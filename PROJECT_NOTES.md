# Studio Sensorium website: project notes

## What we built
- A minimal static website for Studio Sensorium, a design studio and non-profit
  making design accessible in education across the Himalayas.
- Pages: Home, Work, About, Contact, plus a 404 page, favicon, `robots.txt` and
  `sitemap.xml`.
- Plain HTML and CSS, no build step. Light and dark themes, works on phones.
- Main call to action on every page: "Get in touch", which opens an email to
  ajottam@studiosensorium.in.
- Code lives in the `InnoRD01/Spmf` repo, folder `studiosensorium/`, on the
  branch `claude/lucid-curie-tbgpvy`.

## How it is hosted
- **Hosting:** Netlify (free plan), project `unique-youtiao-bdf0c7`.
  - Production branch: `claude/lucid-curie-tbgpvy`
  - Publish directory: `studiosensorium` (set in `netlify.toml`)
  - Every push to that branch redeploys the site automatically.
- **Domain:** `studiosensorium.in`, registered at GoDaddy. DNS stays at GoDaddy.
  - `studiosensorium.in` is the primary domain; `www` redirects to it.
- **Email:** Migadu, unchanged throughout.

## DNS records at GoDaddy
Changed for the website (these replaced the old Framer site):

| Type  | Name | Value |
|-------|------|-------|
| A     | `@`  | `75.2.60.5` (Netlify), the only A record on `@` |
| CNAME | `www`| `unique-youtiao-bdf0c7.netlify.app` |

Never touch these (they are the email records):
- MX `aspmx1.migadu.com` (10) and `aspmx2.migadu.com` (20)
- TXT `v=spf1 include:spf.migadu.com -all`
- TXT `hosted-email-verify=…`
- CNAME `key1/key2/key3._domainkey` → Migadu (DKIM)
- TXT `_dmarc`

Harmless leftovers from GoDaddy: `email` CNAME, `secureserver1/2._domainkey`,
`_autodiscover` SRV, `_domainconnect`.

## What we learned
1. **Deploying the wrong branch:** Netlify first deployed `main`, which only had a
   README. The site is on another branch, so the production branch had to be
   changed in Netlify, followed by a new deploy.
2. **Domains have to be added in two places:** pointing GoDaddy at Netlify isn't
   enough. The domain must also be added in Netlify's Domain management, or
   Netlify can't issue a certificate.
3. **Certificate errors right after a DNS switch are normal:**
   "Your connection is not private" (`ERR_CERT_COMMON_NAME_INVALID`) showed up
   because Netlify had no certificate for the domain yet. Framer had marked the
   domain HTTPS-only (HSTS), so the browser wouldn't let us click through.
   Fix: add the domain in Netlify, then Verify DNS configuration and Provision
   certificate.
4. **The first certificate attempt can fail:** old DNS records can linger for up
   to an hour. Retrying after they expire works. Things that can block it: a
   leftover AAAA record (IPv6) or a CAA record that doesn't allow Let's Encrypt.
5. **Netlify projects can be private:** a "This site is private" screen means
   Visitor access protection is on. Set it to no protection to make the site
   public.
6. **The address bar isn't search:** typing "studio sensorium" searches Google,
   which won't know a new site for days or weeks. Type `studiosensorium.in`.
   To get found, verify the domain in Google Search Console (a TXT record at
   GoDaddy) and submit `sitemap.xml`.
7. **Email is safe if you only edit the website records:** changing the `@` A
   record and the `www` CNAME never affects Migadu.

## How we worked
- **Screenshots were the fastest way to fix things:** each one showed exactly
  where the problem was (wrong branch, Framer records, domain not added,
  private setting).
- **Starting simple paid off:** plain HTML with no build step meant almost
  nothing could break during deployment.
- **Placeholders beat invented content:** draft wording, with clear gaps for
  real projects and team details.
- **Check instructions against the screen:** when guidance and the dashboard
  disagree, the dashboard wins.
- **Agree a clear brief before building:** four pages, minimal, "Get in touch",
  and the domain. That is what got the site live.

## Still to do
- [ ] Confirm HTTPS is active in Netlify and the site is public (Visitor access off).
- [ ] Remove `studiosensorium.in` from the old Framer project.
- [ ] Review and edit the draft wording on all pages.
- [ ] Add real projects (image, title, category, year, short description) to Work.
- [ ] Add a logo, and a team section on About, if wanted.
- [ ] Optional: rename the Netlify project (e.g. `studiosensorium`) and update the
      `www` CNAME to match.
- [ ] Set up Google Search Console and submit the sitemap.
- [ ] Optional: merge the branch into `main` and switch Netlify's production
      branch back to `main`.
