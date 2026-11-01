# b/cited API Response Schema

Reference for the `POST https://bcited.ai/api/skill/scan` endpoint response.

## Top-level fields

| Field | Type | Description |
|---|---|---|
| `url` | string | Canonical URL that was audited (may differ from input after redirect following) |
| `scanned_at` | ISO 8601 string | When the scan completed |
| `source` | `"live"` \| `"cache"` | Whether result came from a fresh fetch or KV cache |
| `duration_ms` | integer | Wall-clock time for the scan in ms (typical: 3,000–25,000) |
| `overall_score` | number 0–100 | Weighted average across all checks |
| `grade` | `"A"` \| `"B"` \| `"C"` \| `"D"` \| `"F"` | Letter grade from overall_score |
| `summary` | object | Aggregate pass/warn/fail counts |
| `categories` | object | Per-category results (see below) |
| `warnings` | string[] | Non-fatal issues (optional, omitted if empty) |

## Grade thresholds

| Grade | Score range |
|---|---|
| A | 90–100 |
| B | 75–89 |
| C | 60–74 |
| D | 45–59 |
| F | 0–44 |

## Summary object

```json
{
  "pass": 28,
  "warn": 6,
  "fail": 4,
  "total": 38
}
```

## Categories object

Each key is a category name. Each value has the same shape:

```json
{
  "score": 72,
  "checks": [
    {
      "category": "aeo",
      "check": "llms.txt",
      "severity": "fail",
      "detail": "No /llms.txt found. This file helps LLMs understand your site structure and preferred citation format.",
      "docs": "https://llmstxt.org"
    }
  ]
}
```

### Category names

| Category | What it covers |
|---|---|
| `indexing` | robots.txt rules, sitemap.xml, canonical tags, X-Robots-Tag header |
| `metadata` | title tag, meta description, H1, lang attribute, viewport |
| `social` | Open Graph tags, Twitter Card completeness |
| `schema` | JSON-LD presence, schema types found, completeness |
| `aeo` | llms.txt, ai.txt, AI crawler stance in robots.txt, FAQPage/HowTo/Author schema |
| `international` | hreflang, language variant links |
| `mobile` | viewport tag, touch-friendly signals |
| `security` | HSTS, X-Frame-Options, CSP, Referrer-Policy, Permissions-Policy |
| `performance` | Core Web Vitals via PageSpeed Insights (may be empty if PSI quota hit) |

### Check severity

| Severity | Meaning |
|---|---|
| `pass` | Signal present and correct |
| `warn` | Present but suboptimal (e.g. title is too long) |
| `fail` | Missing or broken |

## Score calculation

Each check contributes to its category score:
- `pass` = 1.0 points
- `warn` = 0.5 points
- `fail` = 0.0 points

Category score = (sum of check points / total checks in category) × 100.
`overall_score` = mean of all category scores.

## Full example response

```json
{
  "url": "https://example.com",
  "scanned_at": "2026-05-27T14:32:11.000Z",
  "source": "live",
  "duration_ms": 4823,
  "overall_score": 61,
  "grade": "C",
  "summary": {
    "pass": 22,
    "warn": 8,
    "fail": 8,
    "total": 38
  },
  "categories": {
    "aeo": {
      "score": 20,
      "checks": [
        {
          "category": "aeo",
          "check": "llms.txt",
          "severity": "fail",
          "detail": "No /llms.txt found. This file helps LLMs understand site structure and preferred citation format.",
          "docs": "https://llmstxt.org"
        },
        {
          "category": "aeo",
          "check": "ai.txt",
          "severity": "fail",
          "detail": "No /ai.txt found. This Spawning AI consent file signals training and crawl preferences to AI systems.",
          "docs": "https://site.spawning.ai/spawning-ai-txt"
        },
        {
          "category": "aeo",
          "check": "AI crawlers allowed (GPTBot)",
          "severity": "warn",
          "detail": "GPTBot is not explicitly allowed in robots.txt. Add 'User-agent: GPTBot\\nAllow: /' to permit OpenAI crawlers.",
          "docs": "https://platform.openai.com/docs/gptbot"
        },
        {
          "category": "aeo",
          "check": "FAQPage schema",
          "severity": "fail",
          "detail": "No FAQPage JSON-LD found. FAQ schema makes Q&A content directly extractable by AI engines.",
          "docs": "https://schema.org/FAQPage"
        },
        {
          "category": "aeo",
          "check": "Author schema",
          "severity": "fail",
          "detail": "No Person schema with author credentials found. Author metadata is a primary E-E-A-T signal for AI citation.",
          "docs": "https://schema.org/Person"
        }
      ]
    },
    "metadata": {
      "score": 75,
      "checks": [
        {
          "category": "metadata",
          "check": "Title tag length",
          "severity": "warn",
          "detail": "Title is 72 characters — ideally under 60. Longer titles get truncated in search results.",
          "docs": null
        },
        {
          "category": "metadata",
          "check": "Meta description",
          "severity": "pass",
          "detail": "Meta description is 142 characters — within the 100–160 char sweet spot.",
          "docs": null
        }
      ]
    }
  }
}
```

## Rate limits

- 30 requests per hour per IP address
- On `429`, response includes `retry_after` (seconds until reset)
