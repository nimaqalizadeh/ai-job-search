# Search Queries for Job Scraper

<!-- Personalized for Nima Ghasemalizadeh on 2026-09-10. -->

## Installed portal CLIs (primary for `/scrape`)

`/scrape` discovers every portal skill under `.agents/skills/*/SKILL.md` and runs its CLI first. Shipped country-agnostic CLIs include `linkedin-search` and `freehire-search`; Danish demos and any skill you add with `/add-portal` are included the same way. You do **not** need a matching `site:` line below for those CLIs to run.

The `site:` query templates in this file are the **WebSearch fallback** — for portals without a CLI, company career pages, or when a CLI fails.

**Language scope:** write every query category in every language listed in your CLAUDE.md Languages table (typically 1-2, sometimes more). A posting requiring a language you have *not* declared, as a job condition, is excluded before scoring; a posting requiring a *higher level* than you declared in a language you *do* work in is flagged for your own judgment, not excluded — see `04-job-evaluation.md`'s Language Gate, the single source of truth for this rule. Translate each category's keywords rather than machine-translating word-for-word (e.g. "Frontend Developer" -> "Desarrollador Frontend", not a literal word-for-word translation) if you work in more than one language.

## Search Sites

Primary (your market's job boards - scaffold one with `/add-portal`):
- **linkedin.com/jobs** - LinkedIn job listings filtered to Dubai; also covered by `linkedin-search`
- **freehire.me** - multi-market technical job aggregator; covered by `freehire-search`
- **Employer career pages** - searched through WebSearch when no portal CLI is available

Secondary (company career pages via Google):
- Direct Google searches with `site:` filters for known target companies

## Query Categories

Queries are grouped by priority. Write **each category in every language from your Languages table** (see Language scope above). Combine each query with your location terms (e.g. your city, region, or metro area) where the site supports it.

**Organize by function, not job title.** The same underlying work carries different titles across companies and markets (a "Data Scientist" role at one employer may be posted as "Insights Analyst" or "Data Consultant" at another). Name each priority category after the function it covers, and list several plausible job titles as query variants within that category rather than betting an entire priority tier on one exact title string.

### Priority 1: Python Backend Engineering

These match your strongest and most desired career direction.

```
site:linkedin.com/jobs "Python Backend Engineer" Dubai
site:linkedin.com/jobs "Backend Developer" Python Dubai
site:linkedin.com/jobs FastAPI Dubai
site:linkedin.com/jobs Django backend Dubai
site:linkedin.com/jobs "توسعه دهنده بک اند پایتون" دبی
```

### Priority 2: Financial and Data-Intensive Backend Systems

These match your domain expertise.

```
site:linkedin.com/jobs fintech backend Python Dubai
site:linkedin.com/jobs banking backend Python Dubai
site:linkedin.com/jobs "Financial Systems Engineer" Dubai
site:linkedin.com/jobs credit risk software Python Dubai
site:linkedin.com/jobs "مهندس نرم افزار مالی" پایتون دبی
```

### Priority 3: API and Backend Software Engineering

Adjacent roles you could pivot into.

```
site:linkedin.com/jobs "API Engineer" Python Dubai
site:linkedin.com/jobs "Software Engineer Backend" Dubai
site:linkedin.com/jobs PostgreSQL Redis Python Dubai
site:linkedin.com/jobs "توسعه دهنده API" دبی
```

### Priority 4: Broader Technical / Consulting

Wider net for general technical roles.

```
site:linkedin.com/jobs Python developer Dubai
site:linkedin.com/jobs backend engineer Dubai
site:linkedin.com/jobs technical consultant Python Dubai
site:linkedin.com/jobs "برنامه نویس پایتون" دبی
```

## Location Filter

Configured location:
- Dubai

Only include roles located in Dubai.

## Language Filter

Your working languages and levels are in CLAUDE.md's Languages table. When filtering scraped results, apply `04-job-evaluation.md`'s Language Gate: a posting requiring a language you haven't declared at all is excluded; a posting requiring a higher level than you declared in a language you do work in is not excluded, flag it clearly instead (see `job-scraper/SKILL.md`'s Step 3 "Quick Fit Assessment" for how the flag surfaces in `/scrape` output). Postings simply *written* in a language you don't work in, that don't require it on the job, are fine.

## Date Filter

Only include jobs posted within the last 14 days, or with an application deadline that has not yet passed. If a posting date cannot be determined, include it but flag as "date unknown".

## Adapting Queries

If the user specifies a focus area, select queries from the matching category and also generate 2-3 custom queries for that focus. For example:
- "/scrape [focus_area]" -> relevant category queries + custom focus-specific queries
