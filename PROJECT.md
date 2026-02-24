# ATG Innovatech Website

## What This Is
Consulting website for ATG Innovatech — SAP and Power BI consulting firm.
Live at: https://akhil-ghosh.github.io/atginnovatech/
Local dev: `cd ~/Projects/atginnovatech && python3 -m http.server 8866`

---

## People

**Ghosh Thinnakkakath** — Founder, SAP Principal Consultant
- 15+ years at IBM, currently at SAP
- Dual PhD: Information Technology + Business
- Author: *Media Literacy and Politics of Digital Misinformation*
- Clients: Cardinal Health, Google, Whirlpool, Baker Hughes
- SAP is the primary focus of the firm — he is the main draw

**Akhil Ghosh** — Power BI & Data Consultant
- Client: AbbVie
- Secondary, supporting role on the site

---

## Tech Stack
- Pure HTML/CSS/JS, single `index.html`, no build step
- Company logos served from Wikipedia Commons SVG URLs (real logos, browser-fetched)
- Photos: `dad.jpg` (Ghosh, graduation regalia), `akhil.jpg` (Akhil headshot)
- Hosted on GitHub Pages: https://github.com/Akhil-Ghosh/atginnovatech
- Local tunnel (temp): `nohup cloudflared tunnel --url http://localhost:8866 > /tmp/atg-tunnel.log 2>&1 &`

---

## Site Sections (in order)
1. **Nav** — Logo, Services, Clients, Team, Results, Contact CTA
2. **Hero** — Tagline, two CTAs, 3 stat callouts (150+ implementations, 98% retention, 12+ years)
3. **Client Heritage** — Marquee strip + featured cards for all 7 clients
4. **Services** — SAP (3 cards) + Power BI (3 cards)
5. **Why Us** — 4 value props
6. **Industries** — 6 industry tiles
7. **Results** — 3 case study stat cards
8. **Principal Consultant** — Ghosh full-width card (horizontal), Akhil small secondary card
9. **Tech/Certs** — Badge strip
10. **Contact** — Form + info

---

## Logo Sources (Wikipedia Commons)
All loaded as external `<img src>` URLs — browser fetches at runtime, nothing to maintain locally.

| Company | URL |
|---|---|
| IBM | https://upload.wikimedia.org/wikipedia/commons/5/51/IBM_logo.svg |
| SAP | https://upload.wikimedia.org/wikipedia/commons/5/59/SAP_2011_logo.svg |
| Google | https://upload.wikimedia.org/wikipedia/commons/2/2f/Google_2015_logo.svg |
| Cardinal Health | https://upload.wikimedia.org/wikipedia/commons/e/e1/Cardinal_Health_Logo.svg |
| Whirlpool | https://upload.wikimedia.org/wikipedia/commons/9/95/Whirlpool_Corporation_Logo_%28as_of_2017%29.svg |
| Baker Hughes | https://upload.wikimedia.org/wikipedia/commons/6/69/Baker_Hughes_logo.svg |
| AbbVie | https://upload.wikimedia.org/wikipedia/commons/c/cc/AbbVie_logo.svg |

Logo containers use `background: #ffffff` with rounded corners + shadow — logos are designed for light backgrounds, this is correct.

---

## Lessons Learned

### Logos
- **Don't try to hand-code SVG logos.** Custom text SVGs look amateurish. Use real source files.
- **Sandbox has no external internet access.** Can't `curl` Wikipedia PNGs or CDNs. Wikipedia SVG files (not PNGs) worked via curl because they're smaller/different routing.
- **Best approach for real logos on a static site:** reference Wikipedia Commons SVG URLs directly in `<img src>`. Browser fetches them at runtime. No local files needed.
- **White containers are correct for client logos.** Real logos are designed for light backgrounds. A frosted/white pill with shadow on a dark theme looks professional. Don't fight it.
- **Clearbit logo CDN is unreliable/deprecated.** Don't use it.
- **Simple Icons CDN** (`cdn.simpleicons.org`) has SAP, Google, AbbVie but not IBM, Whirlpool, Baker Hughes — partial coverage only.
- **CSS `filter: brightness(0) invert(1)`** turns any logo white but destroys color logos (Google, SAP gradient). Only use for monochrome dark logos.

### Deployment
- **Always `git add -A && git commit` before creating the GitHub repo.** `gh repo create --push` only pushes what's committed. Uncommitted files stay local.
- **GitHub Pages takes ~1 min to rebuild** after each push. Hard refresh (Cmd+Shift+R) to bust browser cache when checking updates.
- **Local server for testing:** `python3 -m http.server PORT` from the project dir. Use cloudflared for a shareable URL.
- **`sed -i ''` on macOS** requires the empty string arg. Python `str.replace()` is more reliable for multi-line blocks.

### Design
- **Team section:** Founder card should be horizontal (image left, content right), not stacked — avoids text-over-image overlap issues.
- **Photo cropping:** For portrait headshots in a card, `object-fit: contain` over `cover` prevents face cutoff.
- **Client section placement:** Put it immediately below the hero. It's the biggest credibility signal — don't bury it.
- **Marquee strip:** Duplicate items in the HTML for seamless CSS infinite scroll. `animation-play-state: paused` on hover.

---

## To Do / Future
- [ ] Custom domain (atginnovatech.com) — point DNS A record to GitHub Pages IP, add CNAME in repo settings
- [ ] Add AbbVie to the logo strip (currently only in Akhil's section)
- [ ] Contact form backend (Formspree or Netlify Forms — free tiers available)
- [ ] Add more case studies if real data becomes available
- [ ] Consider adding a "Book a Call" Calendly embed
