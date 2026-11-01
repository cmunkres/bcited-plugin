---
name: explain
description: "Explain the six Answer Engine Optimization (AEO) signals that decide whether AI engines (ChatGPT, Claude, Perplexity) cite a site: llms.txt, ai.txt, AI crawler stance in robots.txt, citation-friendly schema, E-E-A-T, and body copy clarity. Use when the user asks what AEO is, why a site is not being cited by AI, or how AI answer engines choose sources."
---

# The six AEO signals

Answer Engine Optimization (AEO) is the practice of getting cited in AI answers from ChatGPT, Claude, and Perplexity, not just ranking in blue links. Where SEO asks "do I rank?", AEO asks "do AI assistants mention me when someone asks?".

When invoked, walk through the six signal areas below. Keep it practical and concrete. Implementation code for each signal is in the fix skill's reference file, [../fix/references/aeo-signals.md](../fix/references/aeo-signals.md).

## Six AEO signals every site needs

**1. llms.txt** — A plain-text file at `yourdomain.com/llms.txt` that gives LLMs a structured summary of the site's purpose, key content, and preferred citation format. Think `robots.txt` for AI comprehension, not crawl control.

**2. ai.txt** — The Spawning AI consent file at `yourdomain.com/ai.txt`. Signals whether AI systems may train on your content. Missing or disallowing reduces crawl depth on some providers.

**3. AI crawler allowance in robots.txt** — GPTBot (OpenAI), ClaudeBot (Anthropic), PerplexityBot each have their own user-agent strings. Block them and you don't appear in those providers' training or citation sets.

**4. Citation-friendly schema** — Structured data types AI engines preferentially extract:
   - `FAQPage` — Q&A content becomes directly quotable
   - `HowTo` — Step-by-step answers get cited verbatim
   - `Article` with `author` schema — Author credentials boost E-E-A-T trust signals
   - `Organization` + `WebSite` — Establishes domain identity for brand-name queries

**5. E-E-A-T signals** — Experience, Expertise, Authoritativeness, Trustworthiness:
   - Named authors with `Person` schema (`affiliation`, `sameAs` → LinkedIn/ORCID)
   - Primary sources cited inline (not just "research shows")
   - `dateModified` in Article schema (freshness signal)
   - External publications linking to the domain

**6. Body copy clarity** — AI citation engines extract from:
   - Direct, assertion-style sentences ("X does Y because Z")
   - Numbered lists and comparison tables
   - Short paragraphs with clear topic sentences
   - Specific claims with verifiable data points

## Where to go next

- To measure a live site against these signals, use the scan skill in this plugin.
- To turn a specific page or component into a patch list, use the fix skill.
- The vocabulary used here (citation, brand rank, visibility score, topical cluster) is defined at https://bcited.ai/glossary.
