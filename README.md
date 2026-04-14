# dotvscode

My VS Code user settings — editor preferences, vim keybindings, and native shortcuts, versioned across environments.

## What's tracked

| File | Purpose |
| ---- | ------- |
| `settings.json` | Editor preferences, vim layer, language overrides |
| `keybindings.json` | Native VS Code keybindings |
| `chatLanguageModels.json` | Custom AI model configuration |

## Branches

Each branch targets a specific environment:

| Branch | Environment |
| ------ | ----------- |
| `apple` | macOS |
| `windows` | Windows |
| `cursor` | Cursor editor |

Platform-specific settings live on their respective branch. `apple` is the upstream default.

## Keybinding philosophy

Two layers work together:

- **Vim layer** (`vscodevim.vim`) — leader-key driven, `<space>` as leader. Handles editor navigation, splits, file management, git, debugger, and tasks without leaving the keyboard home row.
- **Native layer** (`keybindings.json`) — `ctrl+;` as the chord prefix for all workbench actions. macOS defaults (`shift+cmd+*`) are explicitly unbound to avoid conflicts.

### Vim layer highlights

| Binding | Action |
| ------- | ------ |
| `<leader>w{h,j,k,l}` | Focus left/below/above/right editor group |
| `<leader>w{v,s}` | Split right / split down |
| `<leader>wm{l,h,k,j}` | Move editor to adjacent group |
| `<leader>wd` | Close active editor |
| `<leader>f{n,s}` | New file / save |
| `<leader>;;` | Toggle line comment |
| `[<space>` / `]<space>` | Insert blank line above / below |
| `<leader>g{f,co}` | Git fetch / checkout |
| `<leader>ghp` | Open GitHub PR panel |
| `<leader>d{b,s,<space>}` | Breakpoint / select debugger / start |
| `<leader>ts` | Run task |
| `gs` | Change all occurrences |

### Native chord map (`ctrl+;`)

| Chord | Action |
| ----- | ------ |
| `ctrl+; space` | Command palette |
| `ctrl+; e` | Explorer |
| `ctrl+; f` | Search |
| `ctrl+; g` | Source Control |
| `ctrl+; p` | Project Manager |
| `ctrl+; t` | Terminal |
| `ctrl+; z` | Zen mode |
| `ctrl+; c` | Claude |
| `ctrl+; w` | Switch window |
| `ctrl+; x` | Extensions |
| `ctrl+; 1/2/3` | Jump to editor by index |

## Required extensions

| Extension | Purpose |
| --------- | ------- |
| `vscodevim.vim` | Vim emulation |
| `alefragnani.project-manager` | Project switching |
| `GitHub.copilot` | Inline AI suggestions |
| `anthropic.claude-vscode` | Claude sidebar |
| `GitHub.vscode-pull-request-github` | PR panel |
| `esbenp.prettier-vscode` | Formatter for JSON / TypeScript |
| `redhat.vscode-yaml` | YAML / Docker Compose formatter |
| `golang.go` | Go language support |
| `PKief.material-icon-theme` | Icon theme |
| `eamodio.gitlens` | Git blame and AI model integration |

## License

Copyright (c) 2020 Alejandro Ricoveri

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
