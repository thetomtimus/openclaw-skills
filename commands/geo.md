# AI Search Optimization (GEO)

Optimize for Generative Engine Optimization — getting cited in:
- Google AI Overviews
- ChatGPT web search
- Perplexity
- Claude web search

## AI Crawler Access

Check if AI crawlers can access your content:

| Crawler | User-Agent | robots.txt directive |
|---------|------------|---------------------|
| GPTBot | GPTBot | `User-agent: GPTBot` |
| ChatGPT-User | ChatGPT-User | `User-agent: ChatGPT-User` |
| Google-Extended | Google-Extended | `User-agent: Google-Extended` |
| ClaudeBot | ClaudeBot | `User-agent: ClaudeBot` |
| PerplexityBot | PerplexityBot | `User-agent: PerplexityBot` |
| Amazonbot | Amazonbot | `User-agent: Amazonbot` |

### Check robots.txt
```
# Good - allows AI crawlers
User-agent: GPTBot
Allow: /

# Bad - blocks AI crawlers
User-agent: GPTBot
Disallow: /
```

## llms.txt

Check for `/llms.txt` — a standard for AI-friendly content:
```
# Example llms.txt
# Company: Example Inc
# Description: We make widgets

## Allowed
/docs/
/blog/
/api/

## Disallowed  
/internal/
/admin/
```

## Citability Signals

### Content Structure
- [ ] Clear, scannable headings (H1 → H2 → H3)
- [ ] Short paragraphs (2-3 sentences)
- [ ] Bullet points for lists
- [ ] Tables for comparisons
- [ ] Direct answers in first paragraph

### Authority Signals
- [ ] Author bylines with credentials
- [ ] Publication dates
- [ ] Last updated dates
- [ ] Citations and sources
- [ ] Expert quotes

### Brand Mentions
- [ ] Consistent brand name usage
- [ ] Brand + category associations
- [ ] Product/service descriptions
- [ ] Unique value propositions

### Passage-Level Optimization
- [ ] Self-contained paragraphs
- [ ] FAQ sections with clear Q&A
- [ ] Definition paragraphs
- [ ] Step-by-step instructions
- [ ] Comparison tables

## Scoring (0-100)

| Factor | Weight |
|--------|--------|
| AI Crawler Access | 20% |
| Content Structure | 25% |
| Authority Signals | 25% |
| Passage Citability | 20% |
| llms.txt Compliance | 10% |

## Quick Wins

1. **Unblock AI crawlers** in robots.txt
2. **Add llms.txt** to root
3. **Add FAQ schema** (if gov/health) or FAQ section
4. **Add author bios** with credentials
5. **Structure content** with clear headings and short paragraphs
