# LLM Wiki in Obsidian

A ready-to-use Markdown vault for building a personal knowledge base with an LLM. You choose the sources and topics; the LLM organizes pages, connects ideas, and maintains references.

## Quick start

1. Install [Obsidian](https://obsidian.md/) and an LLM tool with local file access, such as Claude Code.
2. Clone this repo, or use **Code → Download ZIP**.

```sh
git clone https://github.com/bangyou0912/llm-wiki-in-Obsidian.git
cd llm-wiki-in-Obsidian
```

3. In Obsidian, choose **Open folder as vault** and select this folder. See the [official vault guide](https://obsidian.md/help/manage-vaults).
4. Open the same folder in your LLM tool.
5. Add a Markdown or text document to `raw/`, then send:

```text
Read CLAUDE.md, index.md, and the latest 5 log entries.
Ingest raw/my-document.md using the Ingest workflow.
Focus on the main ideas and reusable knowledge.
Update related pages, the index, overview, and log.
Never modify raw/. Tell me if you cannot read the complete source.
```

Replace `my-document.md` with your filename. Open `index.md` to review the results against the original.

The folders, index, and overview are already initialized. No setup script, plugins, API keys, or predefined topic categories are included. LLM access must be configured separately; PDF and web support depend on your tool.

## Structure

```text
.
├── CLAUDE.md          # LLM workflows and conventions
├── index.md           # Start here
├── log.md             # Activity history, newest first
├── raw/               # Your original sources
│   └── assets/        # Images and attachments
└── wiki/
    ├── _overview.md   # Knowledge base overview
    ├── entities/      # People, organizations, products, events
    ├── concepts/      # Ideas and methods
    ├── sources/       # Source summaries
    └── queries/       # Saved answers
```

Empty folders contain `.gitkeep` files so Git preserves them.

## Everyday use

Start each new LLM session by asking it to read `CLAUDE.md`, `index.md`, and the latest 5 log entries.

**Ask a question**

```text
Using the wiki, answer: [your question].
Cite supporting pages and sources. Distinguish evidence from inference.
Ask whether I want to save the answer in wiki/queries/.
```

**Check the wiki**

```text
Follow the Lint workflow in CLAUDE.md.
Report broken links, contradictions, stale claims, and missing index entries.
Record the findings in log.md.
```

## Customize

- Set your scope, language, and optional domain tags in [CLAUDE.md](./CLAUDE.md).
- Use a standalone vault initially. Inside another vault, include the containing folder's prefix in generated links.
- Review generated content and references before relying on them.
- For backups, use your own repository and change `origin` before pushing. Keep private sources out of public repositories. Local Obsidian settings are ignored by Git.
