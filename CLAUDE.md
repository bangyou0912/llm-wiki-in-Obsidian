# Personal Knowledge Base Instructions

Read this file at the start of every session. It defines how to build and maintain this Obsidian wiki with the user.

## Purpose

Help the user turn their chosen sources into a connected, reusable knowledge base. The user selects sources and directs the work; you summarize, link, organize, and maintain pages.

Do not assume the user's interests, profession, preferred language, or subject categories. Preserve existing conventions unless the user asks to change them.

## User Preferences

The wiki starts without predefined domains. Use these settings when provided; otherwise follow the user's request and the wiki's existing conventions.

- **Scope:** User-defined; no default subject.
- **Language:** Follow the user's requested language or existing page language.
- **Domains:** Optional, user-defined topic labels.
- **Focus:** Follow the requested analysis angle; ask only when needed.
- **Wiki root:** The directory containing this file.
- **Vault location:** Use links relative to the Obsidian vault root.

When the wiki is empty, organize only the material the user supplies. Do not invent categories, sources, or content to fill the template. Ask about preferences when they affect the task, without requiring a setup questionnaire.

## Directory Structure

```text
<wiki-root>/
├── CLAUDE.md              # These instructions
├── index.md               # Page catalog
├── log.md                 # Activity history, newest first
├── raw/                   # Original sources managed by the user
│   ├── assets/            # Images and attachments
│   └── ...
└── wiki/
    ├── _overview.md       # Overview and entry point
    ├── entities/          # People, organizations, places, products, events
    ├── concepts/          # Ideas, theories, methods, themes
    ├── sources/           # One summary per source
    └── queries/           # Saved answers
```

- Never edit, rename, move, or delete files in `raw/`.
- Maintain `wiki/` within the user's requested scope. Preserve useful existing content.
- The distributed template already includes the folders, index, and overview. Do not reset them on first use.
- If working with an incomplete copy, create missing folders and initialize empty index and overview files without fabricated entries.
- Ignore `.gitkeep` files when reading sources or counting pages. They only preserve empty folders in Git.
- Update the index after page changes and record completed operations in the log.
- If this wiki is inside a larger vault, include its folder prefix in links. Keep file operations within the wiki root.

## Domains and Tags

Domains are optional. Use the user's existing taxonomy; do not impose a fixed list.

If topic grouping would help and no taxonomy exists, propose a small set based on the actual sources. Obtain the user's agreement before applying a new taxonomy or recategorizing existing pages. A page may have multiple domains or none.

Use nested tags such as `domain/<topic>`, with slash separators rather than colons. Add only relevant tags. Tags do not require Dataview or other plugins.

## Page Format

Use this structure for wiki pages:

```markdown
---
title: "Page Title"
type: concept
tags: []
created: YYYY-MM-DD
updated: YYYY-MM-DD
sources: 0
---

# Page Title

One-sentence summary.

## Content

## Related
- [[wiki/concepts/related-topic|Related Topic]]

## Sources
- [[wiki/sources/source-title|Source Title]]
```

Replace placeholder values and links with actual content. Omit empty sections when they add no value.

- `type`: choose one of `entity`, `concept`, `source`, `query`, or `overview`.
- `tags`: relevant labels; an empty list is valid.
- `created`: preserve the original creation date.
- `updated`: use the date of the latest edit.
- `sources`: count distinct source documents supporting the page. Do not increment for repeated processing of the same source.

Use readable, stable filenames consistent with the wiki. For English titles, use kebab-case, such as `example-topic.md`. Avoid duplicate pages and filename collisions.

## Page Types

These categories describe a page's role, not the user's subject areas. Adapt section headings to the material.

| Type | Location | Suggested content |
| --- | --- | --- |
| Entity | `wiki/entities/` | Background, facts, relationships, timeline |
| Concept | `wiki/concepts/` | Definition, properties, explanation, examples, open questions |
| Source | `wiki/sources/` | Summary, claims, quotes, related entities and concepts, tensions, original source |
| Query | `wiki/queries/` | Question, answer, findings, caveats, sources used |
| Overview | `wiki/_overview.md` | Scope, current state, themes, key pages, open questions, recent activity |

Create entity and concept pages when they are useful for reuse or navigation. Do not create a page for every passing mention.

## Workflow: Ingest

When the user asks to process a source:

1. Read the source in full. If access is incomplete, explain the limitation before proceeding.
2. Follow the requested focus. If none is given and different angles would materially change the result, discuss the main points and ask which angle to emphasize.
3. Create or update its summary in `wiki/sources/`, linking to the original file in `raw/` and recording available author, date, and URL.
4. Update or create useful entity and concept pages. Reuse existing pages where possible.
5. Add links between related pages. Flag contradictions rather than silently replacing conflicting claims.
6. Update the overview if the new material changes the overall picture.
7. Update the index and its counts.
8. Prepend an `ingest` entry to the log, listing pages created and updated.

Distinguish source claims from your interpretation. Do not invent facts, quotes, citations, or missing metadata.

## Workflow: Query

1. Read the index and relevant pages.
2. Answer with links to supporting wiki and source pages.
3. Distinguish evidence, inference, disagreement, and missing information.
4. Ask whether to save the answer, unless the user already requested it.
5. If saving, create or update a query page and update the index.
6. Prepend a `query` entry to the log.

Match the answer format to the user's request. Do not treat unsupported claims as established knowledge.

## Workflow: Lint

When asked to check the wiki, look for:

- Unflagged contradictions and outdated claims.
- Orphan pages and useful entities or concepts lacking pages.
- Broken links, duplicate pages, and missing index entries.
- Incorrect metadata or source counts.
- Evidence gaps requiring additional sources.

Report issues by severity and offer fixes. Apply fixes when the user requests them. Prepend a `lint` entry to the log.

`/lint` is a workflow label; this template does not install a slash command.

## Cross-References

- Use Obsidian links such as `[[wiki/entities/entity-name|Display Name]]`.
- Link the first relevant mention of an existing page in each section.
- When creating a page, check related existing pages for useful links back.
- Keep the Related section focused on meaningful connections.
- Ensure generated links resolve from the actual vault root.

## Index Format

```markdown
# Wiki Index

_Last updated: YYYY-MM-DD — N sources, N pages_

## Overview
- [[wiki/_overview|Overview]] — wiki entry point

## Sources (N)
- [[wiki/sources/source-title|Source Title]] — summary

## Entities (N)
- [[wiki/entities/entity-name|Entity Name]] — description

## Concepts (N)
- [[wiki/concepts/concept-name|Concept Name]] — description

## Queries (N)
- [[wiki/queries/query-name|Query Title]] — question answered
```

List actual pages only, alphabetically within each section. Count all Markdown pages under `wiki/` in the total, including the overview. Count source-summary pages for the source total. Do not count the index, log, instructions, or raw documents as wiki pages.

## Log Format

Prepend new entries, newest first. Preserve earlier entries.

```markdown
## [YYYY-MM-DD] <operation> | <title>

Brief description of the operation and notable findings.
Pages created: list or none
Pages updated: list or none
```

Operations: `ingest`, `query`, `lint`, `schema-update`.

## Session Start

1. Read `CLAUDE.md`.
2. Read `index.md`.
3. Read the newest five log entries.
4. Continue with the user's request. Ask what they want to do only if no task was provided.

## Updating These Instructions

Change preferences, taxonomy, or workflows when requested by the user. Preserve established conventions unless the requested change requires migration. Record changes as `schema-update` entries in the log.

Version: `2.0` — General-purpose template with user-defined scope and optional domains.
