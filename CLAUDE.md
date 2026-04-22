# MaltipoosForsale.com — Claude Code Project Guide

## Site Overview
- **Domain:** https://maltipoosforsale.com
- **Stack:** Static HTML — exported from WordPress, NO React, NO build tools
- **Host:** Cloudflare Pages (DNS proxy) → Netlify (static host) → GitHub auto-deploy
- **Repo:** github.com/jl69lucas-netizen/maltipoosforsale-com
- **Branch:** main (auto-deploys to Netlify on push)
- **Two breeds:** Maltipoo ($1,200–$1,700) + AKC Maltese ($1,500–$2,000)

## File Structure
```
site2/
├── index.html              # Homepage
├── [slug]/index.html       # All pages (99+ total)
├── usa-locations/*/        # State location pages (22 states)
├── wp-content/uploads/     # All images (739 files) — DO NOT DELETE
├── *.xml                   # Sitemaps (9 files — all URLs must be absolute)
├── _redirects              # Netlify redirect rules
├── _headers                # Security + CSP headers
├── robots.txt              # Crawl rules
├── llms.txt                # AI crawler guide
├── a1b2c3d4e5f6789012345678maltipoos.txt  # IndexNow key file
└── .claude/skills/         # Superpowers + Impeccable skills
```

## Critical Rules — ALWAYS Follow

### 1. Preserve SEO on Every Edit
- **NEVER change H1 text** without explicit user approval
- **NEVER change canonical href** — all must be `https://maltipoosforsale.com/slug/`
- **NEVER remove schema JSON-LD** blocks — preserve verbatim
- **NEVER make og:url, og:image, canonical relative** — must be absolute

### 2. Images
- All images live at `/wp-content/uploads/` — reference with root-relative paths
- **NEVER use `src="data:image/gif;base64,..."`** — that's the broken lazy-load pattern
- Always use real `src="/wp-content/uploads/filename.jpg"`

### 3. Sitemaps — All URLs Must Be Absolute
- All `<loc>`, `<image:loc>`, `<video:*>` tags must start with `https://maltipoosforsale.com`
- After adding new pages, add to `page-sitemap.xml` with absolute URL

### 4. Deploy Flow
```bash
git add -A
git commit -m "Description of change"
git push origin main   # Triggers Netlify auto-deploy (1-3 min)
```

### 5. After Any Deploy — Submit to IndexNow
```python
import json, urllib.request
key = "a1b2c3d4e5f6789012345678maltipoos"
urls = ["https://maltipoosforsale.com/changed-slug/"]
payload = json.dumps({"host":"maltipoosforsale.com","key":key,
    "keyLocation":f"https://maltipoosforsale.com/{key}.txt","urlList":urls}).encode()
req = urllib.request.Request("https://api.indexnow.org/indexnow",data=payload,
    headers={"Content-Type":"application/json; charset=utf-8"},method="POST")
urllib.request.urlopen(req)
```

## Credentials & Keys

| Service | Location |
|---|---|
| GitHub token | Already in git remote URL |
| GSC OAuth | `/Users/apple/mfs-dashboard/.env.local` |
| Cloudflare token | Ask user — zone ID: `7c1b9a778236d4b00b5c9810c00e1bc5` |
| IndexNow key | `a1b2c3d4e5f6789012345678maltipoos` |
| Netlify API | Ask user for token |

## Agent Skills (use these files)

| Agent | Skill File | Trigger |
|---|---|---|
| Technical Health | `MFS-WEBSITE-HEALTH-SKILL.md` | Broken images, canonicals, redirects |
| Indexing | `MFS-INDEXING-SKILL.md` | After any deploy, sitemap fixes, GSC submission |
| Broken Links | `MFS-BROKEN-LINKS-SKILL.md` | GSC 404 errors, broken internal links, missing hub pages |
| Contact Form | `MFS-CONTACT-FORM-SKILL.md` | Form audit/fix, Formspree ID, newsletter, batch apply to all pages |
| YouTube | `MFS-YOUTUBE-SKILL.md` | Fix broken iframes, video-sitemap.xml errors, add new videos |
| Google Map | `MFS-GOOGLE-MAP-SKILL.md` | Fix broken embed maps, add maps to location pages |
| Location Pages | `LOCATION-PAGE-BUILDER-SKILL.md` | Creating state/city pages |
| Design Rebuild | `MFS-DESIGN-REBUILD-SKILL.md` | Redesigning pages with new design system |
| SEO Content | `MFS.md` | All content creation, keyword strategy |

All skill files are in `/Users/apple/Downloads/MFS/`

## Impeccable Design Skills
Installed at `.claude/skills/` — run at start of any design session:
```
/impeccable teach
```
Then use: `/audit`, `/critique`, `/polish`, `/typeset`, `/layout`

## Design System v1.1 (defined in MFS-DESIGN-REBUILD-SKILL.md)
- **Primary/Hero:** `#FF8C00` dark orange (hero backgrounds, section highlights)
- **Accent/CTA:** `#FFA500` vibrant orange (transactional buttons)
- **Ink/Text:** `#000000` black (all body text — WCAG AAA on white)
- **Canvas:** `#FFFFFF` white + `#F8F9FA` off-white (alternating sections)
- **Fonts:** Rosario (headings, 700) + Open Sans (body, 500) — already loaded
- **Radius:** `8px` standard corner radius
- **Reference page:** `/male-vs-female-maltipoo/` — fully redesigned 2026-04-21

## Top Pages by GSC Traffic (redesign priority)
1. Homepage `/` — 78 clicks, 4,345 impr, pos 57
2. `/buy-maltipoo-near-me/` — 15 clicks, 1,820 impr, pos 20
3. `/usa-locations/maltipoo-puppies-arizona/` — 14 clicks
4. `/toy-maltipoo-puppies/` — 14 clicks
5. `/mini-maltipoo-puppies/` — 9 clicks, 562 impr
6. `/teacup-maltipoo-puppies/` — 8 clicks, 230 impr

## Fixed Issues Log (2026-04-21)
- ✅ 707 broken lazy-load images (GIF placeholders → real src)
- ✅ 99 relative canonical tags → absolute URLs
- ✅ 189 relative og:url + og:image + twitter:image → absolute
- ✅ 115 relative sitemap URLs across 9 XML files
- ✅ Homepage was blank on GitHub — restored
- ✅ www redirect via Cloudflare page rule (301)
- ✅ llms.txt relative URLs + HTML entities decoded
- ✅ robots.txt missing Disallow rules added
- ✅ 86 URLs submitted to IndexNow (Bing/Yandex)
- ✅ 6 sitemaps submitted to Google Search Console
- ✅ Impeccable (17 skills) + Superpowers (14 skills) installed
- ✅ 14 broken internal links fixed (redirects + /usa-locations/ hub page)
- ✅ 12 URLs re-submitted to IndexNow after link fixes
- ✅ Homepage contact form: 5-field stub → full 17-field Formspree form (xpqoeazq)
- ✅ Homepage newsletter: 3× SureForms blocks → modern orange/white Formspree widgets
- ✅ Homepage YouTube iframes: data-src → src (lazy-load fix)
- ✅ contact-2, white-maltese, teacup-maltipoo-puppies, ny/ga location pages: upgraded to full 17-field form + correct Formspree ID
- ✅ video-sitemap.xml: 9 relative uploader URLs fixed, thumbnail_loc added to all 9 entries
- ✅ 128 inner pages: injected missing Astra main.min.css (broken header fix)
- ✅ YouTube Agent skill created (MFS-YOUTUBE-SKILL.md)

## What's Next
1. Run 7 Claude Design prompts in claude.ai (from MFS-DESIGN-REBUILD-SKILL.md)
2. Build batch page rebuild agent (applies design to all 99 pages)
3. Create content agent for new pages
4. Build SEO audit agent (checks rankings weekly)
