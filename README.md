# LLM Wiki in Obsidian

Build a personal knowledge base with Obsidian and an LLM. Add sources, let the LLM organize and connect them, then browse your wiki or ask questions with source references.

[CLAUDE.md](./CLAUDE.md) defines the page formats and workflows. This repo is a Markdown template; no Obsidian plugins are required.

## Requirements

- [Obsidian](https://obsidian.md/)
- An LLM tool with local file access, such as Claude Code
- Git (optional)

## Quick start

### 1. Download the repo

Use **Code → Download ZIP**, or clone it:

```sh
git clone https://github.com/bangyou0912/llm-wiki-in-Obsidian.git
cd llm-wiki-in-Obsidian
```

### 2. Open it in Obsidian

Choose **Open folder as vault** and select the repo folder containing `CLAUDE.md`. Use the same folder in your LLM tool.

Start with a standalone vault to keep link paths working. The `10 LLM-Wiki/` name in `CLAUDE.md` is an example, not an extra folder to create.

See [Obsidian's vault guide](https://obsidian.md/help/manage-vaults) for details.

### 3. Initialize the wiki

Send this to your LLM:

```text
Read CLAUDE.md, index.md, log.md, and wiki/_overview.md.
Create missing folders: raw/assets/, wiki/entities/, wiki/concepts/,
wiki/sources/, and wiki/queries/.
Initialize the index and overview if empty, using actual page counts
and zero sources. Record initialization as schema-update in log.md.
Keep new log entries at the top and preserve existing content.
Do not modify raw/ or CLAUDE.md.
```

The resulting structure:

```text
.
├── CLAUDE.md          # LLM instructions
├── index.md           # Page catalog
├── log.md             # Activity history
├── raw/               # Original sources; never edited by the LLM
│   └── assets/        # Images and attachments
└── wiki/
    ├── _overview.md   # Wiki overview
    ├── entities/      # People, organizations, products
    ├── concepts/      # Ideas and methods
    ├── sources/       # Source summaries
    └── queries/       # Saved answers
```

The supplied index, log, and overview start empty. Missing folders are created during initialization.

### 4. Add a source

Place a document in `raw/`, such as `raw/first-article.md`. Include its author, date, and original URL when available.

```text
Read CLAUDE.md, index.md, and the latest 5 log entries.
Read raw/first-article.md in full. Summarize its main points and ask
which angle I want to focus on before following the Ingest workflow.
Create a source summary, update related entity and concept pages,
flag contradictions, and add Obsidian links.
Update the index, log, and overview as needed.
Keep new log entries at the top. Never modify raw/.
If you cannot read the full source, tell me before proceeding.
```

Start with Markdown or plain text. PDF, image, and web access depend on your LLM tool.

### 5. Review the results

Open `index.md` in Obsidian and follow links to the generated pages. Check summaries against the originals, verify references, and confirm links work.

## Everyday use

Start each new LLM session by asking it to read `CLAUDE.md`, `index.md`, and the latest 5 log entries.

**Ask a question**

```text
Using the wiki, answer: [your question].
Read relevant pages, cite sources, and distinguish supported claims
from inference. Say when evidence is missing.
Ask whether I want to save the answer in wiki/queries/.
```

**Check the wiki**

```text
Follow the Lint workflow in CLAUDE.md.
Check for contradictions, stale claims, broken links, orphan pages,
and missing index entries. Report issues before fixing them.
Record the check in log.md, with the newest entry first.
```

## Notes

- Customize domains and conventions in `CLAUDE.md`. Use tags such as `domain/ai`.
- Inside an existing vault, update link paths to include the template's folder prefix.
- For Git backups, use your own repository and change `origin` before pushing. Keep private sources out of public repositories.
