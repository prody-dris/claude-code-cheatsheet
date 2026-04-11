# Agent Workbench

A source-verified, single-page field manual for users of agentic coding CLIs.

**Live:** https://prody-dris.github.io/claude-code-cheatsheet/

## What this is

One HTML page your AI can read. It covers how to run a session well, which slash commands exist, which hooks and skills are available, and how to translate concepts between Claude Code, Codex, Cursor, Gemini CLI, and Copilot CLI.

Claude Code is the primary reference — it's the most mature implementation and it shapes how the other tools are converging. Other CLIs are mapped section-by-section so users of those tools can learn the same disciplines without switching pages.

## Who it's for

- Anyone running Claude Code, Codex, Cursor, Gemini CLI, or GitHub Copilot CLI for real work
- Teams onboarding new members to agentic workflows
- People who want their agents to learn best practices without burning tokens scraping the internet

## How to use it

Point your agent's project-instructions file at the live URL. Examples:

```text
# CLAUDE.md  (Claude Code)
Read https://prody-dris.github.io/claude-code-cheatsheet/ at session start and apply these practices.

# AGENTS.md  (Codex)
Read https://prody-dris.github.io/claude-code-cheatsheet/ and follow the Codex column of the porting matrix.

# GEMINI.md  (Gemini CLI)
Read https://prody-dris.github.io/claude-code-cheatsheet/ for session discipline and hooks equivalents.

# copilot-instructions.md  (Copilot CLI)
Read https://prody-dris.github.io/claude-code-cheatsheet/ and apply the CLAUDE.md discipline and hook triad sections.
```

## Content rule: verify or remove

This page has shipped invented features twice in its history. A fabricated "Channels" description and a fictional "Computer Use" entry. Both were caught and reverted.

Because of that, the page now runs on a strict rule: **every feature claim has a citation.** A version tag from the official Claude Code [CHANGELOG](https://github.com/anthropics/claude-code/blob/main/CHANGELOG.md), or a direct link to the [Claude Code docs](https://code.claude.com/docs/en/overview), or it does not ship. Anything unverified gets removed, not speculated.

## Design constraints

- Single page. No routing, no client-side JavaScript, no framework.
- Light background, minimal visual noise, quiet accents. Readable on any screen.
- Source-dense but scannable. Every section answers a question.
- Content first. Design serves content, not the other way round.
- Prints cleanly. Useful as a one-page PDF reference.

## Update protocol

When updating this page, do not freehand a "what's new" section from memory. Work in order:

1. **Pull the official CHANGELOG.** `gh api repos/anthropics/claude-code/contents/CHANGELOG.md --jq '.content' | base64 -d`
2. **Cross-check the commands reference** at https://code.claude.com/docs/en/commands. Removed commands must be removed here too.
3. **Extract durable, user-relevant changes.** Skip internal fixes, edge-case fixes, and CHANGELOG line-noise. Keep features, new commands, hook events, meaningful default changes.
4. **Translate each capability into workflow consequences.** What should a user do differently now?
5. **Cite every claim.** Version tag (`v2.1.X`) for CHANGELOG entries, direct link for docs pages. No citation → no ship.
6. **Commit on a feature branch, open a PR.** Even for content-only changes.

There is a Claude Code slash command that automates this workflow: `/agent-workbench-update`. See `~/.claude/commands/agent-workbench-update.md` in the maintainer's home dir.

## Repo layout

```
claude-code-cheatsheet/
├── index.html       # the one page, self-contained
└── README.md        # this file
```

That's it. No build step, no dependencies, no framework.

## Contributing

Feature additions require a verified source. Design changes should preserve the light, minimal aesthetic. Open a PR with a clear rationale — content changes get reviewed the same as code changes.

## License

MIT. Use it however helps you run agents better.

---

Maintained by [Nihaan Mohammed](https://github.com/prody-dris). Built with Claude Code.
