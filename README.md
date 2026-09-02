# claude-marketplace

Yuzhou's Claude Code plugin marketplace.

## Install

```
/plugin marketplace add Yuzhouboat/claude-marketplace
```

Then install any listed plugin:

```
/plugin install issue-fixer
```

## Plugins

- **issue-fixer** — fixes GitHub issues end-to-end: investigates, implements a fix, and opens a PR. Source: [Yuzhouboat/issue-fixer](https://github.com/Yuzhouboat/issue-fixer).

## Adding a plugin

Add an entry to `.claude-plugin/marketplace.json`'s `plugins` array, pointing `source` at the plugin's repo (`github:<owner>/<repo>`).
