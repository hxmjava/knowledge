# LLM Wiki Operating Schema

This vault uses a three-layer architecture:

1. `raw/` - immutable source material (human-curated; never edited by agent)
2. `wiki/` - maintained markdown knowledge base (agent-owned)
3. `AGENTS.md` - this schema (human+agent maintained)

## Operating Principles

- Treat `raw/` as source-of-truth inputs; do not rewrite raw files.
- Treat `wiki/` as compiled knowledge; prefer updating existing pages over creating duplicates.
- Every meaningful operation should leave an auditable trace in `wiki/log.md`.
- Prefer explicit uncertainty over fabricated confidence.
- Preserve contradictory evidence; do not hide it.
- Keep writing concise, link-rich, and easy to navigate in Obsidian.

## Required Directory Layout

- `raw/sources/` - primary source documents
- `raw/assets/` - local images, figures, and attachments
- `wiki/index.md` - catalog of wiki pages
- `wiki/log.md` - append-only chronological operations log
- `wiki/overview.md` - current top-level synthesis
- `wiki/sources/` - one page per source
- `wiki/entities/` - people, orgs, tools, places, etc.
- `wiki/concepts/` - themes, ideas, methods
- `wiki/analyses/` - query outputs worth preserving
- `wiki/tasks/` - proposed follow-up investigations

## Page Conventions

### Naming

- Use kebab-case filenames.
- Keep stable names once created.
- Avoid date prefixes except for `wiki/analyses/` when helpful.

### Frontmatter (recommended)

Use this minimal schema when useful:

```yaml
---
title: Page Title
type: source|entity|concept|analysis|overview|task
status: draft|active|superseded
updated: YYYY-MM-DD
source_count: 0
---
```

### Linking

- Add at least 2-5 internal links for non-trivial pages.
- Ensure every non-index page has at least one inbound link.
- Prefer specific anchor links when referencing long pages.

### Evidence style

- When citing a source page, use local wiki links (e.g., `[[sources/example-report]]`).
- For contested claims, add a short "Contradictions / Tensions" section.

## Core Workflows

## 1) Ingest (new source)

Trigger: user asks to process a new file in `raw/sources/`.

Steps:

1. Read the source (and optionally related images in `raw/assets/`).
2. Produce or update a source page in `wiki/sources/`.
3. Update relevant `wiki/entities/` pages.
4. Update relevant `wiki/concepts/` pages.
5. Update `wiki/overview.md` if synthesis changes.
6. Update `wiki/index.md` entries for touched/created pages.
7. Append one entry to `wiki/log.md` using the required log format.
8. If gaps are discovered, create/update a task page under `wiki/tasks/`.

Expected touch count: often 5-15 files.

## 2) Query (answer from wiki)

Trigger: user asks a question.

Steps:

1. Read `wiki/index.md` first to identify likely relevant pages.
2. Read a focused set of linked pages; do not read everything by default.
3. Produce an answer with clear wiki citations.
4. If answer has durable value, save it to `wiki/analyses/` and link it.
5. Append a query entry to `wiki/log.md`.

## 3) Lint (health check)

Trigger: user asks for maintenance or periodic quality review.

Checks:

- Contradictions between key pages
- Stale claims superseded by newer sources
- Orphan pages (no inbound links)
- Missing concept/entity pages for frequently mentioned terms
- Weak cross-referencing opportunities
- High-value data gaps and suggested source searches

Actions:

- Apply high-confidence fixes directly.
- Add follow-up tasks for uncertain fixes in `wiki/tasks/`.
- Append lint entry to `wiki/log.md`.

## Log Format (required)

Append entries to `wiki/log.md` using this heading format:

`## [YYYY-MM-DD] <operation> | <short title>`

Where `<operation>` is one of: `ingest`, `query`, `lint`, `refactor`.

Each entry should include:

- Scope (files created/updated)
- Key outcomes
- Open questions / next actions

## Index Maintenance Rules

- `wiki/index.md` is content-oriented, not chronological.
- Group pages by section (`Overview`, `Sources`, `Entities`, `Concepts`, `Analyses`, `Tasks`).
- For each page include: link + one-line summary + optional metadata.
- Update index in the same operation as page changes.

## Quality Bar

Before finishing an operation, verify:

- No duplicated page for same entity/concept.
- New claims are traceable to at least one source page.
- New/updated pages are linked from at least one hub page.
- `wiki/index.md` and `wiki/log.md` both updated.

## Human-Agent Contract

Human responsibilities:

- Curate source quality
- Set goals and ask high-leverage questions
- Review important synthesis changes

Agent responsibilities:

- Do all wiki bookkeeping and cross-link maintenance
- Keep synthesis pages coherent as corpus grows
- Surface contradictions and uncertainty early
