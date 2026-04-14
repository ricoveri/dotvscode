# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

This is the **VS Code User settings repo** (`dotvscode`), versioning the contents of `~/Library/Application Support/Code/User/`. It tracks three config files:

- `settings.json` — all editor preferences, language-specific overrides, vim keybindings
- `keybindings.json` — native VS Code keybindings (non-vim)
- `chatLanguageModels.json` — AI model configuration (currently empty; placeholder for custom model entries)

The `.gitignore` uses **allow-by-default** (only the three files above are tracked; everything else — `globalStorage/`, `snippets/`, `workspaceStorage/`, `History/`, `sync/` — is excluded).

## Branch strategy

Each branch targets a specific environment:

| Branch    | Environment   |
| --------- | ------------- |
| `apple`   | macOS         |
| `windows` | Windows       |
| `cursor`  | Cursor editor |

Platform-specific settings live on their respective branch. `apple` is the upstream default (`origin/HEAD`). The current working branch is `apple`.

## Required extensions

These extensions must be installed for the full keybinding and settings configuration to work:

| Extension ID | Purpose |
| ------------ | ------- |
| `vscodevim.vim` | Vim emulation — the entire vim layer depends on this |
| `alefragnani.project-manager` | Powers `ctrl+; p` and `<leader>ps` |
| `GitHub.copilot` / `GitHub.copilot-chat` | Copilot inline suggestions and chat |
| `anthropic.claude-vscode` | `ctrl+; c` opens Claude sidebar |
| `GitHub.vscode-pull-request-github` | `<leader>ghp` focuses the PR panel |
| `esbenp.prettier-vscode` | Default formatter for JSON, TypeScript, TSX |
| `redhat.vscode-yaml` | Formatter for YAML and Docker Compose |
| `golang.go` | Go language server and formatter |
| `PKief.material-icon-theme` | Icon theme |
| `eamodio.gitlens` | GitLens AI model integration |

## Key settings architecture

### Vim layer (`settings.json`)

Leader key is `<space>`. The vim extension is pinned to affinity `1` for performance.

**Ctrl keys passed through to VS Code** (not captured by vim): `<C-b>`, `<C-j>`, `<C-k>`, `<C-w>`, `<C-o>`

**Normal mode bindings**

| Binding | Action |
| ------- | ------ |
| `<leader>wh/j/k/l` | Focus left/below/above/right editor group |
| `<leader>wv` | Split editor right (vertical split) |
| `<leader>ws` | Split editor down (horizontal split) |
| `<leader>wd` | Close active editor |
| `<leader>wml/h/k/j` | Move editor to right/left/above/below group |
| `gs` | Change all occurrences (`editor.action.changeAll`) |
| `<leader>;;` | Toggle line comment |
| `<leader>;f` | Insert a FIXME comment (via macros extension) |
| `[<space>` / `]<space>` | Insert blank line above / below (vim-unimpaired style) |
| `<leader>fn` | New untitled file |
| `<leader>fs` | Save file |
| `<leader>ps` | Save current workspace as a project (project-manager) |
| `<leader>db` | Toggle breakpoint |
| `<leader>ds` | Select and start debugger |
| `<leader>d<space>` | Start debugger |
| `<leader>ts` | Run task |
| `<leader>gf` | Git fetch all |
| `<leader>gco` | Git checkout |
| `<leader>ghp` | Open GitHub Pull Requests panel |

**Visual mode bindings**

| Binding | Action |
| ------- | ------ |
| `<leader>;` | Toggle line comment on selection |

### Native keybindings (`keybindings.json`)

`ctrl+;` is the chord prefix for workbench actions. This replaces `shift+cmd+*` macOS defaults, which are all explicitly unbound so they don't conflict.

**`ctrl+;` chord map**

| Chord | Action |
| ----- | ------ |
| `ctrl+; space` | Command palette |
| `ctrl+; e` | Explorer |
| `ctrl+; f` | Search |
| `ctrl+; g` | Source Control (SCM) |
| `ctrl+; p` | Project Manager — list projects |
| `ctrl+; t` | Toggle terminal |
| `ctrl+; z` | Toggle Zen mode |
| `ctrl+; c` | Open Claude sidebar |
| `ctrl+; w` | Quick switch window |
| `ctrl+; x` | Extensions |
| `ctrl+; 1/2/3` | Switch to editor at index 1/2/3 |

**Other native bindings**

| Binding | Context | Action |
| ------- | ------- | ------ |
| `ctrl+b` | — | Toggle sidebar |
| `ctrl+j` | — | Toggle bottom panel |
| `ctrl+w` | — | Close active editor |
| `ctrl+o` | macOS | Open file/folder |
| `ctrl+p` | — | Quick open (file picker) |
| `ctrl+[` | — | Blur — remove focus from any input |
| `ctrl+shift+o` | — | Go to symbol |
| `ctrl+enter` | SCM input | Accept commit message |
| `ctrl+.` | Editor | Quick fix |
| `ctrl+j/k` | Quick open | Navigate list down/up |
| `ctrl+j/k` | Suggestion widget | Navigate suggestions down/up |
| `ctrl+j/k` | List/tree focus | Move focus down/up |
| `ctrl+h/l` | List/tree focus | Collapse/expand tree node |
| `shift+cmd+h/j/k/l` | Editor focus | Decrease/increase view width/height (via Karabiner remapping) |

**Unbinding strategy**: about half the entries in `keybindings.json` are negative bindings (`"-command"`) that remove macOS defaults (`shift+cmd+p`, `shift+cmd+f`, `shift+cmd+e`, `shift+cmd+x`, `cmd+.`, `ctrl+cmd+i`, `f1`, etc.) so they don't conflict with the vim or chord system.

## Language-specific overrides

| Language | Formatter | Notes |
| -------- | --------- | ----- |
| JSON | Prettier | tabSize 4 |
| JSONC | Built-in (`vscode.json-language-features`) | — |
| YAML | — | `formatOnSave` and `formatOnPaste` disabled |
| Docker Compose | redhat.vscode-yaml | language server disabled |
| Terraform | Terraform language server | external binary |
| Python | — | path set to `/usr/bin/python3` |
| Go | `golang.go` | `golangci-lint` on save (workspace scope) |
| TypeScript / TSX | Prettier | `updateImportsOnFileMove` always |

## Git notes

- GPG signing is enabled — commits will fail without a running GPG agent.
- `master` has `pushRemote = no_push` — do not push directly.
- Do not commit or push unless explicitly asked.
