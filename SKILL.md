---
name: paperclip-github-ship-skill
description: Use when the user wants to install, configure, debug, or operate the GitHub Ship Paperclip plugin for GitHub Actions workflow preview, pull request creation, or merge flows.
---

# Paperclip GitHub Ship Skill

Use this skill when the task is specifically about the GitHub Ship Paperclip
plugin:

- installing the plugin into a Paperclip instance
- configuring the target GitHub repository or token reference
- previewing the deploy workflow template
- creating or merging pull requests through the plugin
- debugging why the plugin does not appear or does not work

Do not use this skill for generic GitHub help unrelated to the plugin.

## Quick Start

Plugin repository:

```text
https://github.com/picory/paperclip-github-ship
```

Local install:

```bash
git clone https://github.com/picory/paperclip-github-ship.git
cd paperclip-github-ship
pnpm install
pnpm build
pnpm paperclipai plugin install .
```

## Workflow

1. Confirm the user is working with `GitHub Ship`, not a Codex skill or a
   generic GitHub integration.
2. If the plugin is not installed, install it from the local clone or package
   source.
3. Save company-scoped repo config through the plugin action or UI.
4. Preview the workflow before making repo changes.
5. Use dry-run PR or merge actions first unless the user explicitly wants live
   execution.

## Required Config

Minimum useful config:

```json
{
  "owner": "org-or-user",
  "repo": "repo-name",
  "baseBranch": "main",
  "deployBranch": "main",
  "tokenRef": "paperclip_secret_ref"
}
```

Important:

- `tokenRef` should point to a Paperclip secret reference, not a raw token
  pasted into logs or prompts.
- `create-pr` and `merge-pr` default to dry-run behavior.
- live GitHub API calls require `execute: true`

## Common Commands

Build and verify the plugin:

```bash
pnpm install
pnpm typecheck
pnpm test
pnpm build
```

Install into a running Paperclip instance from the plugin repo:

```bash
pnpm paperclipai plugin install .
```

## Troubleshooting

- If the user tries to add the plugin through a `skill` UI, stop and explain
  that GitHub Ship is a Paperclip plugin, not a Codex skill.
- If the plugin installs but actions fail, check that the company has valid
  repo config and a resolvable `tokenRef`.
- If workflow preview is missing, verify the plugin is enabled and the company
  repo config exists.
- If live PR or merge calls fail, inspect GitHub token scopes and API errors
  before changing plugin logic.
