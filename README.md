# yuzhou-agent-toolkit

Yuzhou's centralized home for custom-developed skills, MCP servers, and other
tooling for AI coding agents (Claude Code, Codex, and others).

## Claude Code plugin marketplace

This repo also serves as a Claude Code plugin marketplace.

### Install

Add the marketplace once:

```
/plugin marketplace add Yuzhouboat/yuzhou-agent-toolkit
```

Then install any listed plugin, at whichever scope fits:

```
/plugin install issue-fixer -s user       # available in every project on this machine
/plugin install issue-fixer -s project    # scoped to the current repo (writes .claude/settings.json,
                                           # committable so teammates get it too)
```

Scope defaults to `user` if `-s` is omitted. Check what's installed with `/plugin list`, and
`/plugin details <name>` shows a plugin's skills/agents/commands and estimated token cost before
you install it.

`address-pr-comment` and `ask-database` live in private repos. Installing them clones over SSH
using your own git credentials, so they only install for accounts with access to those repos —
anyone else adding this marketplace will be able to install `issue-fixer` and `mailbox-triage`
but not those two.

Every plugin here was verified with `claude plugin validate --strict` (manifest correctness) and
a real `claude plugin install` at both `user` and `project` scope (confirming each resolves to
exactly the one skill it declares) before being listed.

### Plugins

- **issue-fixer** — fixes GitHub issues end-to-end: investigates, implements a fix, and opens a PR. Source: [Yuzhouboat/issue-fixer](https://github.com/Yuzhouboat/issue-fixer).
- **mailbox-triage** — triages an email inbox (Exchange or Gmail) with automated classification, filing, and session draft reports. Source: [Yuzhouboat/Mailbox-Triage](https://github.com/Yuzhouboat/Mailbox-Triage).
- **address-pr-comment** — works through a GitHub PR's outstanding review feedback: fetch, fix, reply, resolve. Source: [Yuzhouboat/GithubAgentReview](https://github.com/Yuzhouboat/GithubAgentReview) (private).
- **ask-database** — answers data questions with read-only SQL and a private GitHub-backed Markdown table-memory vault. Source: [Yuzhouboat/ask-database-skill](https://github.com/Yuzhouboat/ask-database-skill) (private).

### Adding a plugin

Add an entry to `.claude-plugin/marketplace.json`'s `plugins` array, pointing `source` at the plugin's repo (`github:<owner>/<repo>`).

## Codex plugin marketplace

The same plugins are also catalogued for Codex in `.agents/plugins/marketplace.json`, following
the same convention as [orim-agent-marketplace](https://github.com/Yuzhouboat/orim-agent-marketplace).
Each plugin repo carries its own `.codex-plugin/plugin.json` manifest alongside its
`.claude-plugin/plugin.json` one, so the same source repos serve both agents.

### Install

```bash
codex plugin marketplace add git@github.com:Yuzhouboat/yuzhou-agent-toolkit.git
codex plugin add issue-fixer@yuzhou-agent-toolkit
codex plugin add mailbox-triage@yuzhou-agent-toolkit
codex plugin add address-pr-comment@yuzhou-agent-toolkit
codex plugin add ask-database@yuzhou-agent-toolkit
```

GitHub access and an SSH key registered to an authorized account are required for the two private
repos (`address-pr-comment`, `ask-database`). Start a new Codex session after installation.

Verified with a real `codex plugin marketplace add` + `codex plugin add` for all four plugins
(`codex-cli` 0.153.4), including the two private repos over SSH — each resolves to its
`skills/<name>/SKILL.md` correctly.

**There is no project-scope install for Codex plugins.** Unlike Claude Code's `-s user|project`,
`codex plugin add` has no scope flag, and running it from inside a project directory installs to
the exact same place as running it anywhere else: `~/.codex/plugins/cache/<marketplace>/<plugin>/<version>`,
tracked in a flat, global `[plugins."<name>@<marketplace>"]` table in `~/.codex/config.toml`. The
`[projects."<path>"]` table in that same file only tracks sandbox trust level, not plugins — it's
unrelated. So for Codex, "installed" always means machine-wide; there's no repo-scoped equivalent
to commit and share with teammates the way `.claude/settings.json` does for Claude Code.
