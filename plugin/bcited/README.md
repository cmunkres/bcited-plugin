# b/cited — Claude Code plugin

Twelve skills for Answer Engine Optimization (AEO). Six need nothing: scan any public URL for the signals that decide whether ChatGPT, Claude, and Perplexity cite it, explain the gaps, turn a page into a patch list, and read b/cited's public leaderboard, citation panel and glossary. Six read your own b/cited account once you sign in: visibility score, citation runs, competitors, on-demand runs and content briefs.

The scanner is rule-based, not model-judged: every check corresponds to an observable fact in the HTTP response.

## Install

From the b/cited marketplace (works today):

```bash
claude plugin marketplace add cmunkres/bcited-plugin
claude plugin install bcited@bcited
```

From the Claude community marketplace (once the listing is approved):

```bash
claude plugin marketplace add anthropics/claude-plugins-community
claude plugin install bcited@claude-community
```

Restart Claude Code, then:

```
/bcited:scan https://yoursite.com
```

You should get a graded site readiness report in about ten seconds.

## Skills

No account needed:

| Skill | What it does |
|---|---|
| `/bcited:scan <url>` | Live AEO + SEO audit. Returns an A–F grade, 9-category breakdown, and a prioritized fix list. |
| `/bcited:explain` | Explains the six AEO signals that drive AI citation: llms.txt, ai.txt, crawler stance, schema types, E-E-A-T, body copy clarity. |
| `/bcited:fix <file>` | Reviews HTML or a component file and outputs a concrete patch list with exact code for every missing signal. |
| `/bcited:leaderboard <category>` | One of the 12 public leaderboard categories: 15 curated domains ranked by weekly scan. |
| `/bcited:citations <category>` | The weekly citation panel: which sites ChatGPT, Claude and Perplexity cited on the category's fixed buyer prompts. |
| `/bcited:readiness <domain>` | A leaderboard domain's rank, failing checks, score history and citation-panel stats. |
| `/bcited:glossary <term>` | b/cited's definition of an AEO term. |

With a free b/cited account (sign in once via `/mcp` when Claude Code asks):

| Skill | What it does |
|---|---|
| `/bcited:score <project>` | Your AEO Visibility Score with the per-engine split. |
| `/bcited:runs <project>` | Recent citation runs: per engine, mentioned, cited, rank, competitors, citation list. |
| `/bcited:competitors <project>` | Which domains the engines cited instead of you, ranked. |
| `/bcited:run <project> <prompt_id>` | Trigger one tracked prompt now and watch the three engines land. Spends a run; once per prompt per hour. |
| `/bcited:brief <project>` | Queue a content brief for a topical cluster and present it when ready. Counts against the monthly allowance. |


Claude also invokes these on its own when a request matches their descriptions, so "is example.com citable by AI?" works without the slash command. The plugin's `.mcp.json` connects two servers: `bcited` (public, `https://mcp.bcited.ai/public`) and `bcited-account` (`https://mcp.bcited.ai/mcp`, OAuth sign-in on first use). The same names are published as MCP prompts by the server, so claude.ai shows them in the connector's menu too.

## Manual install (no plugin system)

The three scanner skills (scan, explain, fix) are published as a single skill file at bcited.ai, for anyone who cannot use plugins; the other nine need the MCP server and are plugin-only:

```bash
# macOS / Linux
dest="$HOME/.claude/skills/bcited-aeo"
mkdir -p "$dest/references"
curl -sL "https://bcited.ai/skill/SKILL.md" -o "$dest/SKILL.md"
curl -sL "https://bcited.ai/skill/references/api-response.md" -o "$dest/references/api-response.md"
curl -sL "https://bcited.ai/skill/references/aeo-signals.md" -o "$dest/references/aeo-signals.md"
```

```powershell
# Windows
$dest = "$env:USERPROFILE\.claude\skills\bcited-aeo"
New-Item -ItemType Directory -Force "$dest\references" | Out-Null
Invoke-WebRequest "https://bcited.ai/skill/SKILL.md" -OutFile "$dest\SKILL.md"
Invoke-WebRequest "https://bcited.ai/skill/references/api-response.md" -OutFile "$dest\references\api-response.md"
Invoke-WebRequest "https://bcited.ai/skill/references/aeo-signals.md" -OutFile "$dest\references\aeo-signals.md"
```

That single file is generated from this plugin by `scripts/build-skill-assets.mjs`; the plugin is the source of truth.

## How it works

`scan` calls `POST https://bcited.ai/api/skill/scan`, which checks 30+ signals across nine categories: indexing, metadata, social cards, structured data, AEO signals (llms.txt, ai.txt, AI crawler stance, FAQPage/HowTo schema), international, mobile, security headers, and Core Web Vitals. Rate limit: 30 requests per hour per IP.

Everything the scanner reads from the audited site (check `detail` text, echoed URLs) is treated as data, never as instructions. The `scan` skill carries the rule; the API caps and strips the strings before they leave the scanner.

## About b/cited

b/cited (bcited.ai) tracks AEO citation across ChatGPT, Claude, and Perplexity: daily runs, an AEO Visibility Score, competitor tracking, and topical authority maps from Google Search Console. Free plan, no credit card. Independent of and unaffiliated with OpenAI, Anthropic, Perplexity, or Google.
