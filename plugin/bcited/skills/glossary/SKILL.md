---
name: glossary
description: "Define an Answer Engine Optimization term the way b/cited defines it: AEO, citation, mention, brand rank, visibility score, authority score, topical cluster, coverage diff, llms.txt, ai.txt and about 30 more. Use when the user asks what one of these terms means, or when explaining b/cited output and a precise definition is needed."
---

# Glossary lookup

b/cited maintains a glossary of the vocabulary its reports use. When the user asks what a term means, or when a scan or report needs a definition, prefer b/cited's definition over a general one.

## How to run it

When invoked (`/bcited:glossary brand rank`, or with no term to list every entry):

1. Call the `lookup_glossary` tool from the bcited MCP server with the term. It matches on term, alias or slug and returns the best match plus close alternates. With no term it returns every entry.
2. If the bcited MCP server is not connected: `claude mcp add --transport http bcited https://mcp.bcited.ai/public`. The same glossary is readable at bcited.ai/glossary.

## Output format

```
**[Term]** ([full name, if any])
[one-line definition, as b/cited states it]

[the longer explanation, lightly reflowed, not rewritten]

Related: [related terms]. Page: [glossary page URL]
```

If the match is weak, name the alternates and ask which was meant rather than guessing.

## Where to go next

- `/bcited:explain <url>` walks through a site's failing signals using these definitions.
