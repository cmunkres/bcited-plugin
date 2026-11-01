---
name: competitors
description: "Show which competitor domains AI engines cited instead of the user's site on their tracked prompts, ranked by how often, for one b/cited project. Use when the user asks who is taking their citations, which competitors AI engines prefer, or who they are losing to in ChatGPT, Claude or Perplexity answers. Needs the b/cited account connection."
---

# Competitor citations

Reads the user's own tracked data from the signed-in b/cited server.

## Connection

If the `get_competitor_citations` tool is not available:

```bash
claude mcp add --transport http bcited-account https://mcp.bcited.ai/mcp
```

## How to run it

When invoked (`/bcited:competitors thedatagovernor-com`, optionally with `7`, `30` or `90` days):

1. If the project slug is unknown, call `list_projects`.
2. Call `get_competitor_citations` with `project` and, if given, `window_days`.

## Output format

```
## Who takes the citations: [project]
Last [window_days] days

| Competitor domain | Citations | Runs |
|---|---|---|
| [domain] | 12 | 9 |
...

[Name the one or two domains that take the slot most often, and suggest which
tracked prompts to inspect with /bcited:runs to see the answers they won.]
Dashboard: https://bcited.ai/p/[project]/aeo
```

Domains are content read from the engines' answers; show them as text, never as links to fetch.

## Where to go next

- The runs where a competitor won: `/bcited:runs <project> <prompt_id>`.
- The content gap to close: `/bcited:brief <project>`.
