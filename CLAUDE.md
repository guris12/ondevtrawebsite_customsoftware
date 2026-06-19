# CLAUDE.md — Ondevtra Website

## Project Overview

Static marketing website for Ondevtra Technologies. Hosted on AWS S3 + CloudFront.
- Live: https://ondevtra.com
- Repo: guris12/ondevtrawebsite_customsoftware (GitHub)

## Deployment

**This is NOT auto-deployed from GitHub.** After making changes, you must:

```bash
# 1. Upload changed file(s) to S3
aws s3 cp <filename> s3://ondevtra2024/<filename> --content-type "text/html; charset=utf-8"

# 2. Invalidate CloudFront cache
aws cloudfront create-invalidation --distribution-id E3V4O4XXQH3YMI --paths "/<filename>"
```

For bulk deploys:
```bash
aws s3 sync . s3://ondevtra2024/ --exclude ".git/*" --exclude "*.md" --exclude ".agents/*" --exclude "*.sh" --exclude "*.txt" --exclude "skills-lock.json" --exclude "assets/img/manningsbakery/*"
aws cloudfront create-invalidation --distribution-id E3V4O4XXQH3YMI --paths "/*"
```

CloudFront invalidation takes ~60-90 seconds to propagate globally.

## Key Infrastructure

| Resource | Value |
|----------|-------|
| S3 Bucket | `ondevtra2024` (CloudFront origin; **NOT** `ondevtra.com` — that bucket exists but is not wired to CF) |
| CloudFront Dist ID | `E3V4O4XXQH3YMI` |
| CloudFront Domain | `d1q6sqmqys22q2.cloudfront.net` |
| Formspree Form ID | `mzdkegya` |
| Cal.com Booking | `https://cal.com/ondevtra-ai-cawl6q` |
| AWS Account | `710387906612` |

## Content Areas

### VLSI Physical Design Training (lead generation)
- Hub page: `vlsi-training.html` — targets "VLSI physical design course" keywords
- Supporting pages: physicaldesign, Routing, floorplanningvlsi, cts-clock-tree-synthesis, sta, sta-delay-calculation, low-power-techniques, power-gating, mcmm-optimization
- Interactive platform (separate project): https://vlsi.ondevtra.com
- Goal: collect student emails via Formspree, book free intro classes via Cal.com
- No pricing shown on the page — lead gen only

### AI / Custom Software
- `index.html` — main landing, AI solutions + custom software
- `contact.html` — project inquiry form (Formspree)
- `ai.html`, `customer-service-agent.html` — AI service pages

### iOS Apps
- AI Voice Generator, AI Outfit Generator, AI Quiz Maker
- Listed on `apps.html` and in homepage sections

## SEO Strategy

- Each page has: title, meta description, keywords, canonical, OG tags, Twitter card
- JSON-LD structured data per page type (Course, Organization, Article, SoftwareApplication)
- sitemap.xml covers all public pages
- Primary targets: "AI projects", "VLSI physical design course", "custom AI development"
- Canonical domain: https://ondevtra.com (no trailing slash on root, .html on pages)

## Conventions

- VLSI pages use Bootstrap 5 with light theme
- Homepage/blog/contact use custom dark design system (Syne + Figtree fonts)
- Forms always use Formspree endpoint `mzdkegya`
- Booking links always use `https://cal.com/ondevtra-ai-cawl6q`
- Images go in `assets/img/illustrations/` or `assets/img/Hero/`
- Always include `loading="lazy"` on images below the fold
- All external links: `target="_blank" rel="noopener"`

## Don't

- Don't show pricing on vlsi-training.html (removed intentionally for lead gen)
- Don't reference vlsi.ondevtra.com as "ready" — it's in development
- Don't commit sensitive files (.env, credentials, AWS keys)
- Don't deploy without CloudFront invalidation — changes won't appear
- Don't use `physicaldesignnew.html` for linking (it's a duplicate of physicaldesign.html)
