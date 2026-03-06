# Technical SEO Analysis

## Checklist

### 1. Crawlability
- [ ] robots.txt exists and is valid
- [ ] No critical pages blocked
- [ ] XML sitemap exists and is referenced
- [ ] No crawl errors in sitemap

### 2. Indexability
- [ ] No unintended noindex tags
- [ ] Canonical tags are correct
- [ ] No redirect chains (max 1 hop)
- [ ] No redirect loops

### 3. Security
- [ ] HTTPS enabled
- [ ] Valid SSL certificate
- [ ] HSTS header present
- [ ] No mixed content warnings

### 4. Core Web Vitals (2024+ standards)
| Metric | Good | Needs Improvement | Poor |
|--------|------|-------------------|------|
| LCP | ≤2.5s | 2.5s–4s | >4s |
| INP | ≤200ms | 200ms–500ms | >500ms |
| CLS | ≤0.1 | 0.1–0.25 | >0.25 |

**Note**: INP replaced FID on March 12, 2024.

### 5. Mobile Friendliness
- [ ] Viewport meta tag present
- [ ] No horizontal scroll
- [ ] Touch targets ≥48px
- [ ] Readable font sizes (≥16px)

### 6. Page Speed
- [ ] HTML response <200ms (TTFB)
- [ ] Total page weight <3MB
- [ ] No render-blocking resources
- [ ] Images lazy-loaded

### 7. URL Structure
- [ ] Clean, descriptive URLs
- [ ] No dynamic parameters for content pages
- [ ] Consistent trailing slash usage
- [ ] Lowercase URLs

### 8. International (if applicable)
- [ ] hreflang tags present
- [ ] Self-referencing hreflang
- [ ] Return tags for each language
- [ ] x-default specified

## How to Check

```bash
# Fetch robots.txt
curl -s https://example.com/robots.txt

# Check sitemap
curl -s https://example.com/sitemap.xml | head -50

# Check headers
curl -I https://example.com
```

Or use web_fetch tool to analyze the page HTML.
