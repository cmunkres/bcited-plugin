---
name: leaderboard
description: "Show one category of b/cited's public AEO readiness leaderboard: 15 curated domains ranked by weekly rule-based scan, with grade, overall score and AEO score. Use when the user asks who leads a software category for AI-citation readiness, how a vendor category compares, or names a category like CRM, project management or SEO tools."
---

# Leaderboard category

b/cited scans 180 curated domains across 12 software categories every week with the same rule-based scanner as `/bcited:scan`, and publishes the ranking at bcited.ai/leaderboard.

## How to run it

When invoked (`/bcited:leaderboard crm`, or a request that names a category):

1. Call the `get_leaderboard` tool from the bcited MCP server with the category slug. If the slug is unknown, call `list_leaderboard_categories` and pick the closest match; if nothing matches, list the 12 slugs and stop.
2. If the bcited MCP server is not connected, say so and give the one-line fix: `claude mcp add --transport http bcited https://mcp.bcited.ai/public`. There is no curl fallback for this skill.

## Output format

```
## AEO readiness leaderboard: [category name]
[total] domains · scanned weekly · rule-based, not model-judged

| # | Site | Grade | Score | AEO |
|---|---|---|---|---|
| 1 | [display_name or domain] | A | 94 | 88 |
...

[Two sentences on what separates the top of the board from the bottom, drawn
from the AEO scores. Then:] Full board and per-site checks: [page URL of #1]'s
category page at bcited.ai/leaderboard/[slug].
```

Unscanned domains sort last with null scores; show them as "—", never as zero. Rankings are listings, not endorsements.

## Where to go next

- One domain's checks, history and citation-panel stats: `/bcited:readiness <domain>`.
- Which sites the engines actually cite in this category: `/bcited:citations <category>`.
