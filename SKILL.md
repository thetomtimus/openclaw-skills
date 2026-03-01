# SEO Audit Skill

Comprehensive SEO analysis for any website. Performs full site audits, technical SEO checks, schema markup validation, content quality assessment (E-E-A-T), Core Web Vitals analysis, and AI search optimization (GEO).

## Description

Universal SEO analysis covering:
- **Technical SEO**: Crawlability, indexability, security headers, Core Web Vitals (LCP, INP, CLS)
- **Content Quality**: E-E-A-T framework (Sept 2025 QRG), readability, thin content detection
- **Schema Markup**: Detection, validation, generation (JSON-LD, Microdata, RDFa)
- **On-Page SEO**: Title tags, meta descriptions, headings, internal linking
- **Image Optimization**: Alt text, sizing, format recommendations
- **AI Search (GEO)**: Citability for Google AI Overviews, ChatGPT, Perplexity

## When to Use

Trigger this skill when the user mentions:
- "SEO audit", "SEO analysis", "analyze SEO"
- "check my site", "website health"
- "technical SEO", "Core Web Vitals"
- "schema markup", "structured data"
- "E-E-A-T", "content quality"
- "AI Overviews", "GEO optimization"
- "page speed", "site performance"

## Commands

### Full Audit
```
audit <url>
```
Full website audit — crawls pages, analyzes all categories, generates health score (0-100).

### Single Page Analysis
```
page <url>
```
Deep analysis of a single page — all SEO factors.

### Technical SEO
```
technical <url>
```
Technical audit: robots.txt, sitemaps, canonicals, security headers, CWV.

### Schema Markup
```
schema <url>
```
Detect, validate, and generate Schema.org markup recommendations.

### Content Quality
```
content <url>
```
E-E-A-T assessment, readability, thin content detection.

### AI Search Optimization
```
geo <url>
```
Optimize for AI Overviews, ChatGPT citations, Perplexity.

### Sitemap Analysis
```
sitemap <url>
```
Analyze XML sitemap structure and coverage.

### Image Audit
```
images <url>
```
Image optimization — alt text, sizing, format recommendations.

## Workflow

### For Full Audit (`audit <url>`)

1. **Fetch Homepage**
   ```
   Use web_fetch to retrieve the page HTML
   ```

2. **Detect Business Type**
   - SaaS: pricing page, /features, /docs, "free trial"
   - Local: phone, address, service area, Google Maps
   - E-commerce: /products, /cart, "add to cart", product schema
   - Publisher: /blog, /articles, article schema, author pages
   - Agency: /case-studies, /portfolio, client logos

3. **Analyze Categories**
   Run each analysis sequentially or spawn subagents:
   - Technical SEO (25% weight)
   - Content Quality (25% weight)
   - On-Page SEO (20% weight)
   - Schema/Structured Data (10% weight)
   - Performance/CWV (10% weight)
   - Images (5% weight)
   - AI Search Readiness (5% weight)

4. **Calculate SEO Health Score (0-100)**
   Weighted aggregate of all categories.

5. **Generate Report**
   - Executive summary with top issues
   - Prioritized action plan (Critical → High → Medium → Low)

### For Single Commands

Load the relevant reference file and analyze:
- `technical` → Check robots.txt, sitemap, canonicals, headers
- `schema` → Detect JSON-LD/Microdata, validate against Google's supported types
- `content` → Assess E-E-A-T signals, readability, uniqueness
- `geo` → Check AI crawler access, llms.txt, citability signals

## Scoring

### SEO Health Score (0-100)

| Category | Weight |
|----------|--------|
| Technical SEO | 25% |
| Content Quality | 25% |
| On-Page SEO | 20% |
| Schema/Structured Data | 10% |
| Performance (CWV) | 10% |
| Images | 5% |
| AI Search Readiness | 5% |

### Priority Levels

- **Critical**: Blocks indexing or causes penalties → fix immediately
- **High**: Significantly impacts rankings → fix within 1 week
- **Medium**: Optimization opportunity → fix within 1 month
- **Low**: Nice to have → backlog

## Quality Gates

⚠️ **Warnings**:
- 30+ location pages → require 60%+ unique content
- 100+ programmatic pages → thin content audit required

🛑 **Hard Stops**:
- 50+ location pages → require user justification
- 500+ programmatic pages → require explicit audit approval

**Schema Deprecations**:
- ❌ HowTo schema (deprecated Sept 2023)
- ⚠️ FAQ schema (restricted to gov/health sites, Aug 2023)
- ❌ SpecialAnnouncement (deprecated July 2025)

**Core Web Vitals**:
- Always use INP (Interaction to Next Paint), never FID
- LCP target: ≤2.5s
- INP target: ≤200ms
- CLS target: ≤0.1

## Reference Files

Load on-demand from `references/`:
- `cwv-thresholds.md` — Core Web Vitals targets and measurement
- `eeat-framework.md` — E-E-A-T evaluation criteria
- `schema-types.md` — Supported schema types with deprecations
- `quality-gates.md` — Content thresholds per page type

## Report Template

```markdown
# SEO Audit Report: [domain]

## Executive Summary
- **SEO Health Score**: [0-100]/100
- **Business Type**: [detected type]
- **Pages Analyzed**: [count]

### Top 5 Critical Issues
1. [issue]
2. [issue]
...

### Top 5 Quick Wins
1. [opportunity]
2. [opportunity]
...

## Technical SEO
[findings]

## Content Quality
[findings]

## On-Page SEO
[findings]

## Schema & Structured Data
[findings]

## Performance (Core Web Vitals)
[findings]

## Images
[findings]

## AI Search Readiness
[findings]

## Action Plan

### Critical (Fix Immediately)
- [ ] [task]

### High Priority (This Week)
- [ ] [task]

### Medium Priority (This Month)
- [ ] [task]

### Low Priority (Backlog)
- [ ] [task]
```

