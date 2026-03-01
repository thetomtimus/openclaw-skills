# SEO Audit Skill for OpenClaw

Comprehensive SEO analysis skill for OpenClaw agents. Performs full site audits, technical SEO checks, schema validation, E-E-A-T assessment, and AI search optimization (GEO).

## Installation

### OpenClaw
```bash
# Copy to your skills directory
cp -r seo ~/.openclaw/skills/
```

### Manual
Download and place in `~/.openclaw/skills/seo/`

## Usage

Just ask naturally:

```
"Do an SEO audit of example.com"
"Check the technical SEO of my site"
"Analyze schema markup on this page"
"How can I optimize for AI search?"
```

## Commands

| Command | Description |
|---------|-------------|
| `audit <url>` | Full website audit with health score |
| `page <url>` | Deep single-page analysis |
| `technical <url>` | Technical SEO (robots, sitemap, CWV) |
| `schema <url>` | Schema markup detection & validation |
| `content <url>` | E-E-A-T and content quality |
| `geo <url>` | AI search optimization (GEO) |
| `sitemap <url>` | XML sitemap analysis |
| `images <url>` | Image optimization audit |

## Features

### Technical SEO
- Crawlability & indexability checks
- robots.txt and sitemap validation
- Core Web Vitals (LCP, INP, CLS)
- Security headers (HTTPS, HSTS)
- Mobile friendliness

### Content Quality
- E-E-A-T framework (Sept 2025 QRG)
- Readability scoring
- Thin content detection
- Duplicate content checks

### Schema Markup
- JSON-LD, Microdata, RDFa detection
- Validation against Google's supported types
- Template generation
- Deprecation warnings (HowTo, FAQ restrictions)

### AI Search (GEO)
- AI crawler access (GPTBot, ClaudeBot, etc.)
- llms.txt compliance
- Citability scoring
- Passage-level optimization

## SEO Health Score

Weighted scoring (0-100):

| Category | Weight |
|----------|--------|
| Technical SEO | 25% |
| Content Quality | 25% |
| On-Page SEO | 20% |
| Schema/Structured Data | 10% |
| Performance (CWV) | 10% |
| Images | 5% |
| AI Search Readiness | 5% |

## File Structure

```
seo/
├── SKILL.md           # Main skill instructions
├── README.md          # This file
├── commands/
│   ├── technical.md   # Technical SEO checklist
│   └── geo.md         # AI search optimization
├── references/
│   ├── cwv-thresholds.md
│   ├── eeat-framework.md
│   ├── schema-types.md
│   └── quality-gates.md
└── schema/
    └── templates.json # Schema.org templates
```

## Requirements

- OpenClaw with web_fetch capability
- Internet access for page analysis


MIT License
