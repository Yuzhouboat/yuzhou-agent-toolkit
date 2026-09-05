# yuzhou-agent-toolkit

Yuzhou's centralized home for custom-developed skills, MCP servers, and other
tooling for AI coding agents (Claude Code, Codex, and others).

## Claude Code plugin marketplace

This repo also serves as a Claude Code plugin marketplace.

### Install

```
/plugin marketplace add Yuzhouboat/yuzhou-agent-toolkit
```

Then install any listed plugin:

```
/plugin install issue-fixer
```

### Plugins

- **issue-fixer** — fixes GitHub issues end-to-end: investigates, implements a fix, and opens a PR. Source: [Yuzhouboat/issue-fixer](https://github.com/Yuzhouboat/issue-fixer).
- **mailbox-triage** — triages an email inbox (Exchange or Gmail) with automated classification, filing, and session draft reports. Source: [Yuzhouboat/Mailbox-Triage](https://github.com/Yuzhouboat/Mailbox-Triage).
- **address-pr-comment** — works through a GitHub PR's outstanding review feedback: fetch, fix, reply, resolve. Source: [Yuzhouboat/GithubAgentReview](https://github.com/Yuzhouboat/GithubAgentReview) (private).
- **ask-database** — answers data questions with read-only SQL and a private GitHub-backed Markdown table-memory vault. Source: [Yuzhouboat/ask-database-skill](https://github.com/Yuzhouboat/ask-database-skill) (private).

### Adding a plugin

Add an entry to `.claude-plugin/marketplace.json`'s `plugins` array, pointing `source` at the plugin's repo (`github:<owner>/<repo>`).
