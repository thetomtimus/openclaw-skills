---
name: neon-egress-optimizer
description: "Audit and optimize database queries to minimize egress (outbound data transfer) costs on Neon Postgres and other cloud databases. Use this skill whenever the user mentions high database costs, Neon billing, egress charges, slow queries, database optimization, query performance, SELECT *, overfetching, N+1 queries, caching database results, or wants to reduce data transfer from their database — even if they don't specifically say 'egress'."
---

# Neon Egress Optimizer

Audit a codebase for database egress inefficiencies and apply targeted fixes. While the examples use Next.js and Drizzle ORM, the principles apply to any framework or ORM connecting to Neon, Supabase, PlanetScale, or any cloud database with egress charges.

## What is egress and why it matters

Egress is data leaving the database over the network to your application. Cloud providers charge for this after a free tier (Neon: $0.09/GiB after the plan allowance). The cost is proportional to **bytes transferred**, not query count — so one query returning 50 unused columns costs more than one returning the 3 you need.

Unoptimized apps can 10-50x their egress without realizing it. The fixes below are ordered by typical impact.

## Step 1: Measure before fixing

Before changing anything, identify where egress is going. This prevents wasted effort on low-impact queries.

**Neon dashboard:** Check the "Consumption" tab for egress trends. Look for spikes that correlate with deployments or traffic changes.

**Identify heavy queries:** Run this on your Neon database to find the most data-intensive queries:

\`\`\`sql
SELECT query, calls, rows,
  pg_size_pretty(shared_blks_hit * 8192 + shared_blks_read * 8192) as total_data,
  rows / NULLIF(calls, 0) as avg_rows_per_call
FROM pg_stat_statements
ORDER BY rows DESC
LIMIT 20;
\`\`\`

Focus optimization effort on the top offenders.

## Step 2: Audit checklist

### 1. SELECT * and unnecessary columns in list queries

**The problem:** List/index pages only display titles, dates, and thumbnails — but the query fetches full content bodies, JSON blobs, and metadata.

**Fix — Drizzle ORM:**
\`\`\`typescript
// BAD
const items = await db.query.results.findMany({
  where: eq(results.brandId, brandId),
});

// GOOD
const items = await db.query.results.findMany({
  where: eq(results.brandId, brandId),
  columns: {
    id: true,
    promptText: true,
    createdAt: true,
    visibilityScore: true,
  },
});
\`\`\`

### 2. N+1 queries

**Fix — use relations:**
\`\`\`typescript
// GOOD — single query with relation
const items = await db.query.results.findMany({
  where: eq(results.brandId, brandId),
  columns: { id: true, createdAt: true },
  with: {
    prompt: { columns: { id: true, promptText: true } },
  },
});
\`\`\`

### 3. Missing query caching

\`\`\`typescript
import { unstable_cache } from 'next/cache';

const getCachedLeaderboard = unstable_cache(
  async (brandId: string) => {
    return db.select({ /* ... */ }).from(results).where(eq(results.brandId, brandId));
  },
  ['leaderboard'],
  { revalidate: 300 }
);
\`\`\`

### 4. Unbounded queries

\`\`\`typescript
// BAD
const allResults = await db.query.results.findMany({
  where: eq(results.brandId, brandId),
});

// GOOD
const page = await db.query.results.findMany({
  where: eq(results.brandId, brandId),
  limit: 25,
  offset: (pageNum - 1) * 25,
});
\`\`\`

## Step 3: Apply fixes by priority

| Priority | Fix | Effort | Impact |
|---|---|---|---|
| 1 | Remove large fields from list queries | Low | High |
| 2 | Fix N+1 queries | Medium | High |
| 3 | Add caching to high-frequency queries | Medium | High |
| 4 | Add LIMITs to unbounded queries | Low | Medium |

## Step 4: Verify

1. Run \`pnpm build\` to verify no type errors
2. Check list pages still display correctly
3. Monitor Neon "Consumption" tab over 1-7 days
