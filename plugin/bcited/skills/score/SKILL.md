---
name: score
description: "Show the AEO Visibility Score for one of the user's b/cited projects over 7, 30 or 90 days: runs, mention rate, citation rate, mean brand rank, and the per-engine split across ChatGPT, Claude and Perplexity. Use when the user asks how visible their site is to AI engines, for their score, or how it differs by engine. Needs the b/cited account connection."
---

# AEO visibility score

Reads the user's own tracked data. It needs the signed-in b/cited server, not the public one.

## Connection

The account tools live on `https://mcp.bcited.ai/mcp` behind sign-in. If the `get_visibility_score` tool is not available, add the server and sign in when prompted:

```bash
claude mcp add --transport http bcited-account https://mcp.bcited.ai/mcp
```

A free b/cited account with one connected Search Console property is enough.

## How to run it

When invoked (`/bcited:score thedatagovernor-com`, optionally with `7`, `30` or `90` days):

1. If the project slug is unknown, call `list_projects` and use the slug the user means; with one project, use it without asking.
2. Call `get_visibility_score` with `project` and, if given, `window_days`.

## Output format

```
## AEO visibility score: [project]
**[score] / 100** · last [window_days] days · computed [computedAt]

Runs [runs] · Cited [citationRate as %] · Mentioned [mentionRate as %] · Mean rank when cited [meanRank or —]

| Engine | Runs | Cited | Mentioned | Mean rank |
|---|---|---|---|---|
| ChatGPT | ... |
| Claude | ... |
| Perplexity | ... |

[One or two sentences: which engine carries the score, which is missing.]
Dashboard: https://bcited.ai/p/[project]/aeo
```

`mentionRate` and `citationRate` arrive as 0–1 fractions; show them as whole percents. On the Free plan prompts run only when triggered, so a sparse window is expected, not a fault; paid plans run every prompt nightly.

## Where to go next

- The runs behind the score: `/bcited:runs <project>`.
- Who is taking the citations instead: `/bcited:competitors <project>`.
