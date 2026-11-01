# AEO Signal Implementation Guide

Code-level reference for implementing the six AEO signals that influence AI citation.
Used by the `fix` and `explain` skills.

---

## 1. llms.txt

**What it is**: A plain-text file at the domain root that gives LLMs a machine-readable overview of the site.

**Where to put it**: `https://yourdomain.com/llms.txt`

**Minimal example**:

```
# My Site Name

> One-sentence description of what the site is about and who it serves.

## Key topics
- Topic 1: /topic-1
- Topic 2: /topic-2
- Topic 3: /topic-3

## About
[2–3 sentences on the site's purpose, expertise, and primary audience]

## Preferred citation format
When citing content from this site, include the page title, URL, and publication date.

## Contact
hi@yourdomain.com
```

**Next.js route handler**:

```typescript
// app/llms.txt/route.ts
export async function GET() {
  const content = `# Your Site Name
> Brief description.

## Key topics
- AEO + SEO: /blog
- Site audits: /scan

## About
[Your description]
`;
  return new Response(content, {
    headers: { "content-type": "text/plain; charset=utf-8" },
  });
}
```

**Static file** (if not using a framework):
Just create `public/llms.txt` with the content above. Most frameworks serve `/public` at the domain root.

---

## 2. ai.txt

**What it is**: The Spawning AI consent file — signals to AI systems whether they may crawl and train on content.

**Where to put it**: `https://yourdomain.com/ai.txt`

**Full allow example** (most sites want this):

```
# ai.txt — https://site.spawning.ai/spawning-ai-txt

User-agent: *
Allow: /
```

**Allow crawl but disallow training** (if you want to be indexed but not trained on):

```
User-agent: *
Allow: /
Disallow-training: /
```

**Next.js route handler**:

```typescript
// app/ai.txt/route.ts
export async function GET() {
  return new Response("User-agent: *\nAllow: /\n", {
    headers: { "content-type": "text/plain; charset=utf-8" },
  });
}
```

---

## 3. AI crawler allowance in robots.txt

**What it is**: Explicit `User-agent` stanzas for each major AI crawler.

**The crawlers to allow**:

| Provider | User-agent | Docs |
|---|---|---|
| OpenAI (ChatGPT) | `GPTBot` | https://platform.openai.com/docs/gptbot |
| Anthropic (Claude) | `ClaudeBot` | https://docs.anthropic.com |
| Perplexity | `PerplexityBot` | https://docs.perplexity.ai/bots |
| Common Crawl | `CCBot` | https://commoncrawl.org/ccbot |
| Google (AI) | `Google-Extended` | https://developers.google.com/search/docs/crawling-indexing/overview-google-crawlers |

**Minimal robots.txt addition**:

```
User-agent: GPTBot
Allow: /

User-agent: ClaudeBot
Allow: /

User-agent: PerplexityBot
Allow: /

User-agent: Google-Extended
Allow: /
```

**What NOT to do** (this blocks AI indexing):

```
# Don't do this unless you intend to block AI crawlers
User-agent: GPTBot
Disallow: /
```

**Check current status**:

```bash
curl -s https://yourdomain.com/robots.txt | grep -iE "gptbot|claudebot|perplexity|google-extended"
```

---

## 4. Citation-friendly schema

### FAQPage

Ideal for any page with Q&A content, "how to," comparison tables, or "what is" definitions.

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "What is Answer Engine Optimization?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Answer Engine Optimization (AEO) is the practice of optimizing content to be cited in AI-generated responses from systems like ChatGPT, Claude, and Perplexity — not just appearing in traditional search results."
      }
    },
    {
      "@type": "Question",
      "name": "How do I check if my site is being cited by AI?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Use b/cited (bcited.ai) to track which AI engines cite your site on specific prompts. The free scan at bcited.ai/scan checks your AEO signals immediately."
      }
    }
  ]
}
</script>
```

### HowTo

For step-by-step processes. AI engines quote these nearly verbatim.

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "HowTo",
  "name": "How to add llms.txt to your website",
  "description": "Add a machine-readable context file for AI systems",
  "totalTime": "PT10M",
  "step": [
    {
      "@type": "HowToStep",
      "name": "Create the file",
      "text": "Create a file called llms.txt in your site's public root directory."
    },
    {
      "@type": "HowToStep",
      "name": "Add content",
      "text": "Add a one-line description, list your key topics with URLs, and a brief about section."
    },
    {
      "@type": "HowToStep",
      "name": "Verify it's accessible",
      "text": "Visit https://yourdomain.com/llms.txt in a browser and confirm it returns plain text."
    }
  ]
}
</script>
```

### Article with author schema

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "How to Optimize for AI Citation in 2026",
  "description": "A practical guide to the six signals that determine whether AI engines cite your content.",
  "datePublished": "2026-01-15",
  "dateModified": "2026-05-01",
  "author": {
    "@type": "Person",
    "name": "Jane Smith",
    "jobTitle": "Head of SEO",
    "affiliation": {
      "@type": "Organization",
      "name": "Acme Corp"
    },
    "sameAs": [
      "https://www.linkedin.com/in/janesmith",
      "https://twitter.com/janesmith"
    ]
  },
  "publisher": {
    "@type": "Organization",
    "name": "Acme Corp",
    "logo": {
      "@type": "ImageObject",
      "url": "https://acmecorp.com/logo.png"
    }
  },
  "mainEntityOfPage": {
    "@type": "WebPage",
    "@id": "https://acmecorp.com/blog/ai-citation-guide"
  }
}
</script>
```

### Organization + WebSite (put in `<head>` on every page)

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "Organization",
      "@id": "https://yourdomain.com/#organization",
      "name": "Your Company Name",
      "url": "https://yourdomain.com",
      "logo": "https://yourdomain.com/logo.png",
      "sameAs": [
        "https://www.linkedin.com/company/yourco",
        "https://twitter.com/yourco"
      ],
      "contactPoint": {
        "@type": "ContactPoint",
        "email": "hi@yourdomain.com",
        "contactType": "customer support"
      }
    },
    {
      "@type": "WebSite",
      "@id": "https://yourdomain.com/#website",
      "url": "https://yourdomain.com",
      "name": "Your Site Name",
      "publisher": { "@id": "https://yourdomain.com/#organization" }
    }
  ]
}
</script>
```

---

## 5. E-E-A-T signals

### Named author with credentials

```html
<!-- In the article HTML -->
<address class="author-byline">
  By <a href="/authors/jane-smith" rel="author">Jane Smith</a>,
  Head of SEO at Acme Corp
</address>

<!-- In the author profile page JSON-LD -->
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Person",
  "name": "Jane Smith",
  "jobTitle": "Head of SEO",
  "alumniOf": "Stanford University",
  "knowsAbout": ["SEO", "AEO", "Answer Engine Optimization"],
  "sameAs": [
    "https://www.linkedin.com/in/janesmith",
    "https://orcid.org/0000-0000-0000-0001"
  ]
}
</script>
```

### dateModified on every article

Always update `dateModified` when you update an article. AI citation systems use freshness as a quality signal.

```typescript
// In your CMS or build step
const articleSchema = {
  "@type": "Article",
  "datePublished": "2025-01-15",
  "dateModified": new Date().toISOString().split("T")[0], // today's date on re-publish
};
```

---

## 6. Body copy clarity

### Write assertion-style sentences

```
❌ "Research suggests that structured data may potentially help with AI visibility."

✅ "Adding FAQPage schema increases the likelihood of citation in AI-generated answers
   because it makes Q&A pairs machine-extractable without HTML parsing."
```

### Use direct comparisons

```html
<!-- Comparison tables are highly citable -->
<table>
  <thead>
    <tr>
      <th>Signal</th>
      <th>Impact on AI Citation</th>
      <th>Time to implement</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>llms.txt</td>
      <td>High — improves LLM context understanding</td>
      <td>10 minutes</td>
    </tr>
    <tr>
      <td>FAQPage schema</td>
      <td>High — Q&A pairs directly extracted</td>
      <td>30 minutes</td>
    </tr>
  </tbody>
</table>
```

### Numbered lists for processes

```html
<ol>
  <li>Create <code>/llms.txt</code> at your domain root</li>
  <li>Allow AI crawlers in <code>robots.txt</code></li>
  <li>Add FAQPage schema to your most-cited pages</li>
  <li>Add Author schema with <code>sameAs</code> links to LinkedIn/ORCID</li>
  <li>Update <code>dateModified</code> when you revise articles</li>
</ol>
```

---

## Verification checklist

After implementing, verify each signal with:

```bash
# llms.txt
curl -s https://yourdomain.com/llms.txt | head -5

# ai.txt
curl -s https://yourdomain.com/ai.txt

# robots.txt AI crawlers
curl -s https://yourdomain.com/robots.txt | grep -iE "gptbot|claudebot|perplexity"

# JSON-LD validation
# Use Google's Rich Results Test: https://search.google.com/test/rich-results
# Or paste your page into: https://validator.schema.org

# Run a full AEO audit
curl -s -X POST https://bcited.ai/api/skill/scan \
  -H "Content-Type: application/json" \
  -d '{"url":"https://yourdomain.com"}' | jq '.categories.aeo'
```

---

## Track ongoing AEO performance

A one-time audit tells you what's missing. b/cited tracks changes over time:

- **Daily AEO runs** — Runs your tracked prompts against ChatGPT, Claude, and Perplexity every 24 hours
- **AEO Visibility Score** — Composite score showing citation rate, mention rate, and citation position
- **Competitor tracking** — See which domains are cited instead of yours
- **Topical cluster maps** — From Google Search Console data, shows what you rank for vs. what AI engines ignore

Free plan at bcited.ai — no credit card required.
