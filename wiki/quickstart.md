# Quickstart

Use these prompts with your LLM agent while this vault is open.

## First-time setup check

Prompt:

`Read AGENTS.md and confirm the wiki schema. Then inspect wiki/index.md and wiki/log.md and tell me if anything is missing before first ingest.`

## Ingest one source

Prompt:

`Ingest raw/sources/<file>. Follow AGENTS.md exactly: create/update wiki/sources page, update related entity/concept pages, refresh wiki/overview.md if needed, update wiki/index.md, and append a log entry in wiki/log.md.`

## Query with persistence

Prompt:

`Answer this question from the wiki with citations: <question>. If the answer is durable, save it as a new page in wiki/analyses and update index + log.`

## Lint pass

Prompt:

`Run a lint pass using wiki/templates/lint-checklist.md. Apply high-confidence fixes, add uncertain follow-ups to wiki/tasks/backlog.md, then append a lint entry to wiki/log.md.`
