# Personal Knowledge Base Schema

This file is the operating contract between you (the LLM) and this wiki. Read it at the start of every session before doing anything else. All workflows, conventions, and maintenance rules live here.

---

## Purpose

This wiki is a **persistent, compounding personal knowledge base** covering all domains the human cares about — currently including AI/LLM research, investment analysis, and computer science. You (the LLM) write and maintain it. The human curates sources, directs analysis, and asks questions. You do the summarizing, cross-referencing, filing, and bookkeeping.

The wiki grows richer with every source added and every question asked. Nothing is re-derived from scratch — it is compiled once and kept current.

---

## Domains

Each page should carry a `domain` tag to aid filtering and navigation:
- `domain/ai` — AI/LLM research, models, techniques
- `domain/investing` — investment analysis, market concepts, companies
- `domain/cs` — computer science, systems, programming

Use a slash, not a colon: Obsidian rejects tags containing `:` and silently drops them when the Properties panel rewrites the frontmatter. The slash form is also a nested tag, so `#domain` matches all three.

---

## Directory Structure

```
10 LLM-Wiki/
├── CLAUDE.md              ← this file — read first every session
├── index.md               ← content catalog — updated on every ingest
├── log.md                 ← append-only chronological log
├── raw/                   ← IMMUTABLE source documents (human writes here)
│   ├── assets/            ← downloaded images and attachments
│   └── (source files…)
└── wiki/                  ← LLM-maintained pages (you write here)
    ├── _overview.md       ← top-level synthesis and entry point
    ├── entities/          ← people, organizations, places, products
    ├── concepts/          ← ideas, theories, themes, methodologies
    ├── sources/           ← one summary page per ingested source
    └── queries/           ← saved answers worth keeping
```

**Rules:**
- Never modify files in `raw/`. They are the source of truth.
- You own everything in `wiki/`. Create, update, and maintain these files freely.
- `index.md` and `log.md` are in the root of `10 LLM-Wiki/` — update them on every operation.

---

## Page Format

Every wiki page uses this structure:

```markdown
---
title: "Page Title"
type: entity | concept | source | query | overview
tags: [tag1, tag2]
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: 0          # number of source documents this page draws from
---

# Page Title

One-sentence summary of what this page is about.

## [Content sections — vary by page type]

## Related
- [[Link to related page]]
- [[Another related page]]

## Sources
- [[sources/Source Title]]
```

**Frontmatter fields:**
- `type`: one of `entity`, `concept`, `source`, `query`, `overview`
- `tags`: relevant tags for Dataview queries
- `created` / `updated`: ISO date — update `updated` on every edit
- `sources`: how many source documents informed this page (increment on each ingest)

---

## Page Types

### Entity pages (`wiki/entities/`)
For specific people, organizations, places, products, events. File name: kebab-case of the entity name (e.g., `alan-turing.md`, `openai.md`).

Sections: Background · Key Facts · Relationships · Timeline (if relevant) · Notes · Related · Sources

### Concept pages (`wiki/concepts/`)
For ideas, theories, themes, methodologies. File name: kebab-case (e.g., `transformer-architecture.md`).

Sections: Definition · Key Properties · How It Works · Debates / Open Questions · Examples · Related · Sources

### Source pages (`wiki/sources/`)
One page per ingested source document. File name: kebab-case title (e.g., `attention-is-all-you-need.md`).

Sections: Summary · Key Claims · Notable Quotes · Entities Mentioned · Concepts Mentioned · Contradictions / Tensions · Raw File

### Query pages (`wiki/queries/`)
Saved answers to questions worth keeping. File name: short-kebab-description (e.g., `comparison-llm-architectures.md`).

Sections: Question · Answer · Key Findings · Caveats · Related · Sources Used

### Overview (`wiki/_overview.md`)
The entry point to the wiki. Keep it high-level — it should give a reader a mental map of the entire wiki.

Sections: Purpose · Current State · Key Themes · Key Entities · Key Concepts · Open Questions · Recent Activity

---

## Workflow: Ingest

When the human adds a new source to `raw/` and asks you to process it:

1. **Read** the source file completely.
2. **Discuss** key takeaways with the human. Ask what angle they want to emphasize.
3. **Create** a source summary page at `wiki/sources/<kebab-title>.md`.
4. **Update** existing entity pages for entities mentioned in the source, or create new ones.
5. **Update** existing concept pages for concepts mentioned, or create new ones.
6. **Flag contradictions**: if the source contradicts something already in the wiki, note it explicitly on the relevant page under a "Contradictions / Tensions" section.
7. **Update** `wiki/_overview.md` if the new source shifts the overall picture.
8. **Update** `index.md`: add the new source page and any new entity/concept pages; update summaries for modified pages.
9. **Append** to `log.md`: `## [YYYY-MM-DD] ingest | Source Title`

A single ingest may touch 5–15 wiki pages. This is expected and correct.

---

## Workflow: Query

When the human asks a question:

1. **Read `index.md`** to identify relevant pages.
2. **Read** the relevant wiki pages.
3. **Synthesize** an answer with citations to wiki pages and source pages.
4. **Ask the human** whether the answer is worth filing as a query page.
5. If yes, **create** `wiki/queries/<kebab-description>.md`.
6. **Update** `index.md` and append to `log.md`: `## [YYYY-MM-DD] query | Question summary`

Answers can take different forms: prose, comparison table, Marp slide deck, bullet list. Match the format to the question.

---

## Workflow: Lint

When the human asks for a health check (`/lint`):

Check for:
- **Contradictions** between pages that haven't been flagged
- **Stale claims** that newer sources have superseded
- **Orphan pages** with no inbound links from other wiki pages
- **Missing pages** for concepts or entities mentioned in multiple places but lacking their own page
- **Broken cross-references** (links to pages that don't exist)
- **Index gaps** (pages in `wiki/` not listed in `index.md`)
- **Data gaps** that could be filled with a web search

Output a lint report listing issues by severity. Offer to fix them. Append to `log.md`: `## [YYYY-MM-DD] lint | brief findings`

---

## Cross-Reference Conventions

- Use Obsidian wiki-links: `[[wiki/entities/entity-name|Display Name]]`
- When mentioning an entity or concept that has its own page, always link it — first mention per section is enough.
- When creating a new page, scan existing pages for mentions of the new entity/concept and add links back.
- The `Related` section at the bottom of every page lists the most relevant cross-links.

---

## Index Format (`index.md`)

```markdown
# Wiki Index

_Last updated: YYYY-MM-DD — N sources, N pages_

## Overview
- [[wiki/_overview|Overview]] — top-level synthesis and entry point

## Sources (N)
- [[wiki/sources/source-title|Source Title]] — one-line summary

## Entities (N)
- [[wiki/entities/entity-name|Entity Name]] — one-line description

## Concepts (N)
- [[wiki/concepts/concept-name|Concept Name]] — one-line description

## Queries (N)
- [[wiki/queries/query-name|Query Title]] — question answered
```

Keep entries in alphabetical order within each section. Update the header counts on every edit.

---

## Log Format (`log.md`)

Entries are prepended (newest first). Each entry starts with a consistent prefix so it is grep-parseable:

```markdown
## [YYYY-MM-DD] <operation> | <title>

Brief description of what was done, what changed, what was notable.
Pages created: list
Pages updated: list
```

Operations: `ingest`, `query`, `lint`, `schema-update`

To get the last 5 entries: `grep "^## \[" log.md | head -5`

---

## Session Start Checklist

At the start of every session:
1. Read this file (`CLAUDE.md`).
2. Read `index.md` to get current state of the wiki.
3. Read the last 5 entries in `log.md` to see what happened recently.
4. Ask the human what they want to do today.

---

## Schema Evolution

This schema is a living document. When you and the human discover that a convention isn't working, update this file. Append to `log.md`: `## [YYYY-MM-DD] schema-update | what changed and why`.

Current version: `1.2` — 2026-10-07: domain tags changed from `domain:xx` to `domain/xx` because Obsidian drops tags containing a colon.

Previous: `1.1` — 2026-04-17: expanded scope from LLM-only to multi-domain personal knowledge base; added domain tagging convention.
