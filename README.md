# Prosperity REIS — IDX Staging Site

Self-contained static staging site demonstrating Bright MLS IDX compliance on a pre-launch preview of `staging.prosperityreis.com`. Built for Burgundy's compliance review (June 2026).

## Pages

| Path | Purpose |
|---|---|
| `index.html` | Home page — hero + search bar + counties + IDX explainer + footer disclosures |
| `search.html` | IDX search results — 6 mocked listings each with broker attribution, Bright watermark, brokerage prominence |
| `listing/sample-1.html` | Single listing detail — full attribution block, AVM labeled "estimate", appraisal disclaimer, all footer disclosures |
| `assets/style.css` | Brand styling (copper + black, Cinzel headings) |

## Compliance checklist (mapped to gap report)

Every page renders these required disclosures:

- "© 2026 Bright MLS, All Rights Reserved" (footer)
- "Information Deemed Reliable But Not Guaranteed" (footer + inline on listing detail)
- IDX nature explanation (home + every search page + footer)
- Personal non-commercial use notification (home + every search page + footer)
- Currency disclaimer (footer)
- Completeness disclaimer (footer)
- Last-updated timestamp (footer, dynamically rendered to current local time on load)
- Data-correction contact (footer — inquiry@prosperityreis.com + (866) 327-7673)
- Prosperity brokerage name in copper strap above every search/listing page (Section 4(i) prominence)
- Per-listing broker attribution + listing office on every card and detail page
- Bright MLS watermark on every photo placeholder
- AVM labeled "Estimated value" (never "appraisal") with inline disclaimer
- Pre-launch staging banner at top of every page — no public confusion
- `<meta name="robots" content="noindex, nofollow">` on every page

## Deploying to Cloudflare Pages

prosperityreis.com is already on Cloudflare static. Easiest path:

1. **Create a new Pages project** at dash.cloudflare.com → Workers & Pages → Create application → Pages → Direct upload.
2. **Drag this folder** (`staging-prosperityreis/`) into the upload area, or zip it and upload.
3. **Project name suggestion:** `prosperityreis-staging`. Cloudflare gives you `prosperityreis-staging.pages.dev` automatically.
4. **Add custom domain:** Settings → Custom domains → Add `staging.prosperityreis.com`. CF will give you a CNAME to add to DNS.
5. **DNS:** In prosperityreis.com's Cloudflare DNS, add a CNAME `staging` → `prosperityreis-staging.pages.dev` (proxied).
6. **Verify TLS green** — should be automatic within a minute.

Once live, send `https://staging.prosperityreis.com` to Burgundy on the existing Bright thread.

## Test data note

This site uses **mocked listings** (`MLS# PAPH-DEMO-*`) for compliance demonstration. Burgundy at Bright offered to provide test data; once those credentials/feeds arrive, swap the mocked listing data for the test feed via simple template binding. No template/layout changes should be required — the compliance posture is locked in.

## Why a separate staging subdomain (not a path)

Bright's IDX policy explicitly requires the licensed display to be on a domain controlled by the broker. Putting compliance changes on a `/staging` path of the live `prosperityreis.com` would risk consumer confusion before launch. The subdomain keeps the live site untouched and signals "pre-launch" through both the URL and the banner at the top.

## Local preview

```bash
# from this directory:
python3 -m http.server 8080
# then open http://localhost:8080
```
