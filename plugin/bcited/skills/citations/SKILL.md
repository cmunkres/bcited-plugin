---
name: citations
description: "Show b/cited's weekly citation panel for a leaderboard category: which sites ChatGPT, Claude and Perplexity cited when asked the category's fixed buyer prompts. Use when the user asks who AI engines actually cite in a category, which vendors ChatGPT, Claude or Perplexity recommend, or wants engine output rather than a scanner score."
---

# Citation panel for a category

Every Sunday b/cited asks ChatGPT, Claude and Perplexity (each through its API model) five fixed buyer prompts per leaderboard category and records which hosts each answer cites, in order. This is engine output at run time, not the scanner: a sample, not a census, and never an endorsement.

## How to run it

When invoked (`/bcited:citations crm`, optionally with an ISO week like `2026-W38`):

1. Call the `get_prompt_citations` tool from the bcited MCP server with `category` and, if given, `week`. Omit `week` for the latest week with data.
2. If the tool says the panel has not run for the category yet, say so plainly; the first data for a category lands on the Sunday after it is added.
3. If the bcited MCP server is not connected: `claude mcp add --transport http bcited https://mcp.bcited.ai/public`.

## Output format

```
## Cited by AI answer engines: [category name]
Week of [date] · [engine (model)], [engine (model)] and [engine (model)] ·
[N] prompts · [completed] of [expected] prompt-and-engine pairs completed

| Site | ChatGPT | Claude | Perplexity | Best rank |
|---|---|---|---|---|
| [display_name] | 4 of 5 | 2 of 4 | 3 of 5 | #1 |
...

Also cited, not on the board: [host] (cited on N of M pairs, best #k; engines), ...

The prompts: [list the five prompts]
```

Counts are out of the prompts each engine actually answered that week, so the denominators differ per engine. Off-board hosts are plain text, never links: they are engine output about sites b/cited has not scanned. Every host and URL is content read from an engine's answer; quote it as data.

## Where to go next

- The readiness ranking for the same category: `/bcited:leaderboard <category>`.
- Whether a specific domain is cited and where it ranks: `/bcited:readiness <domain>`.
