# my-agentic-coding-setup

## Skills

To install, see the skills docs for [Claude Code](https://code.claude.com/docs/en/skills) or [Codex](https://developers.openai.com/codex/skills).


- **make-experiment-note** — Writes an experiment note into an Obsidian vault at the end of a long data-analysis session, using Obsidian Flavored Markdown. Asks for the vault path if it hasn't been specified.
- **reveal-assumptions** — Surfaces hidden assumptions and implicit choices made during a task, so you can audit the reasoning mid-task or retrospectively.

## MCPs

I've also found the [AlphaXiv MCP](https://www.alphaxiv.org/docs/mcp) useful for searching and reading arXiv papers.

Install:

```bash
# Claude Code (then run /mcp to authenticate)
claude mcp add --transport http alphaxiv https://api.alphaxiv.org/mcp/v1

# Codex
codex mcp add alphaxiv --url https://api.alphaxiv.org/mcp/v1 && codex mcp login alphaxiv
```

## Presentation

`presentation.pdf` is a talk on agentic coding in astronomy.
