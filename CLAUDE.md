# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

This is the **VS Code User settings repo** (`dotvscode`), versioning the contents of `~/Library/Application Support/Code/User/`. It tracks three config files:

- `settings.json` — all editor preferences, language-specific overrides, vim keybindings
- `keybindings.json` — native VS Code keybindings (non-vim)
- `chatLanguageModels.json` — AI model configuration

The `.gitignore` uses allow-by-default (excludes `globalStorage/`, `snippets/`, `workspaceStorage/`, `History/`, `sync/`).

## Branch strategy

Each branch targets a specific environment:

| Branch    | Environment   |
| --------- | ------------- |
| `master`  | base/shared   |
| `apple`   | macOS         |
| `windows` | Windows       |
| `cursor`  | Cursor editor |

Platform-specific settings live on their respective branch. Cross-platform changes should start on `master` and be merged/cherry-picked.

## Key settings architecture

**Vim layer (`settings.json`)**

- Leader key is `<space>`
- `<leader>w{h,j,k,l}` — focus editor group (vim-style pane navigation)
- `<leader>w{v,s}` — vertical/horizontal split
- `<leader>w{d}` — close active editor
- `<leader>f{n,s}` — new file, save
- `<leader>g{f}`, `<leader>g{co}` — git fetch, checkout
- `<leader>d{b,s,<space>}` — debugger breakpoint, select, start
- `gs` — change all occurrences (normal mode)
- Passes `<C-b>`, `<C-k>`, `<C-j>`, `<C-w>`, `<C-o>` through to VS Code (not captured by vim)

**Native keybindings (`keybindings.json`)**

- `ctrl+;` is the chord prefix for most workbench actions (replaces `shift+cmd+*` defaults)
- `ctrl+; {e,f,x,g,p,t,z,c,space}` — explorer, search, extensions, SCM, projects, terminal, zen, Claude, command palette
- `ctrl+j/k` — vim-style navigation in quick open, suggestion box, lists

## Git notes

- GPG signing is enabled — commits will fail without a running GPG agent.
- `master` has `pushRemote = no_push` — do not push directly.
- Do not commit or push unless explicitly asked.
