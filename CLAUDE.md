# LLM Wiki Schema

This is a personal knowledge base maintained by an LLM. The wiki grows incrementally as sources are ingested and questions are explored.

## Directory Structure

```
raw/                    # Immutable source documents — LLM reads, never modifies
  assets/               # Images and other media from sources
wiki/                   # LLM-generated and maintained markdown files
  sources/              # One summary page per ingested source
  entities/             # Pages for people, organizations, products, places
  concepts/             # Pages for ideas, theories, frameworks, techniques
  synthesis/            # Cross-cutting analysis, comparisons, timelines
  index.md              # Master catalog of all wiki pages
  log.md                # Chronological record of all operations
```

## Page Conventions

### Frontmatter
Every wiki page includes YAML frontmatter:

```yaml
---
title: Page Title
type: source | entity | concept | synthesis
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: [list of source filenames that informed this page]
tags: [relevant tags]
---
```

### Cross-References
- Use standard markdown links: `[Page Title](../category/filename.md)`
- Use Obsidian-style wikilinks as well: `[[filename]]` for discoverability in graph view
- Every page should link to related pages; orphan pages are a lint issue

### Naming
- Filenames: lowercase, hyphens for spaces (e.g., `transformer-architecture.md`)
- Keep filenames short but descriptive

## Operations

### Ingest (processing a new source)

When told to ingest a source:

1. **Read** the source document in `raw/` completely
2. **Discuss** key takeaways with the user — what's interesting, what to emphasize
3. **Create** a source summary page in `wiki/sources/`
4. **Update or create** entity pages in `wiki/entities/` for people, orgs, products mentioned
5. **Update or create** concept pages in `wiki/concepts/` for ideas, frameworks, techniques
6. **Update** existing pages across the wiki where the new source adds context, nuance, or contradicts prior information. Flag contradictions explicitly.
7. **Update** `wiki/index.md` with new/modified pages
8. **Append** to `wiki/log.md` with a timestamped entry

A single source may touch 10-15 wiki pages. Take time to integrate thoroughly.

### Query (answering questions)

When asked a question:

1. **Read** `wiki/index.md` to find relevant pages
2. **Read** the relevant wiki pages
3. **Synthesize** an answer with citations to wiki pages
4. If the answer is substantial and reusable, **offer to file it** as a new synthesis page in the wiki so it compounds into the knowledge base

### Lint (health check)

When asked to lint:

1. Check for **contradictions** between pages
2. Find **stale claims** that newer sources have superseded
3. Identify **orphan pages** with no inbound links
4. Note **concepts mentioned but lacking their own page**
5. Flag **missing cross-references**
6. Suggest **new questions** to investigate and **new sources** to look for
7. Log the lint pass in `wiki/log.md`

## Formatting Guidelines

- Write in clear, concise prose
- Use headers to structure longer pages
- Include bullet points for lists of facts or claims
- Always attribute claims to their source: `(Source: [source-name](../sources/source-name.md))`
- When sources disagree, present both views and note the contradiction
- Prefer substance over length — a tight paragraph beats a padded page
