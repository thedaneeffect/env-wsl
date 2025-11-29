# Development Environment Setup

Automated development environment for macOS and WSL with GPG commit signing and encrypted secrets management.

## Quick Start

```bash
bash <(curl -fsSL https://raw.githubusercontent.com/thedaneeffect/dotfiles/main/bootstrap.sh)
```

Or clone and run:

```bash
git clone https://github.com/thedaneeffect/dotfiles.git
cd dotfiles
./setup.sh
```

Setup prompts for optional secrets storage configuration (Cloudflare Worker URL + passphrase).

## What Gets Installed

### Core Environment

| Component | Purpose | Source |
|-----------|---------|--------|
| **Zsh** | Default shell with Oh-My-Zsh framework | Homebrew |
| **Starship** | Cross-shell prompt with git integration | mise |
| **Helix** | Modern terminal editor | mise |
| **Zellij** | Terminal multiplexer | mise |
| **Claude CLI** | AI assistant for command line | Direct install |
| **Secrets CLI** | AES-256 encrypted secrets sync via Cloudflare Workers | Custom script |

### Modern CLI Tools (via mise)

All managed via `.config/mise/config.toml` with automatic version updates:

| Tool | Replaces | Purpose |
|------|----------|---------|
| **ripgrep** | grep | Fast recursive search, respects .gitignore |
| **fd** | find | Simple and fast file finding |
| **bat** | cat | Syntax-highlighted file viewing |
| **eza** | ls | Modern ls with colors and git status |
| **delta** | diff | Beautiful git diffs with syntax highlighting |
| **sd** | sed | Simple find and replace |
| **dust** | du | Disk usage visualization |
| **fzf** | - | Fuzzy finder for files and commands |
| **zoxide** | cd | Smart directory jumping based on frecency |
| **jq** | - | JSON processor and query tool |
| **yq** | - | YAML processor and query tool |
| **gh** | - | GitHub CLI for issues, PRs, repos |
| **glow** | - | Markdown renderer for terminal |
| **grex** | - | Generate regex from examples |
| **ast-grep** | - | Structural code search and replace |
| **tlrc** | man | Fast tldr client (tealdeer) for simplified man pages |
| **procs** | ps | Modern process viewer |
| **usql** | - | Universal SQL client (PostgreSQL, SQLite) |

### Development Tools (via mise)

| Tool | Purpose |
|------|---------|
| **go** | Go programming language (latest) |
| **rust** | Rust toolchain with cargo |
| **bun** | Fast JavaScript runtime and package manager |
| **zig** | Zig programming language |
| **air** | Live reload for Go development |
| **gofumpt** | Stricter gofmt formatter |
| **golangci-lint** | Go linter aggregator |
| **golines** | Go code formatter for long lines |

### Language Servers (via mise)

Installed for Helix editor integration:

- **gopls** - Go language server
- **zls** - Zig language server
- **bash-language-server** - Bash/shell scripting
- **typescript-language-server** - TypeScript/JavaScript
- **yaml-language-server** - YAML files
- **marksman** - Markdown files
- **taplo** - TOML files
- **docker-language-server** - Dockerfiles
- **vscode-langservers-extracted** - HTML, CSS, JSON, ESLint
- **golangci-lint-langserver** - Go linting integration
- **dlv** - Go debugger (Delve)

### Homebrew Packages

Direct installations (not in mise):

| Package | Purpose |
|---------|---------|
| **gum** | Glamorous shell scripts and TUI components |
| **gnupg** | GPG encryption for commit signing |
| **btop** | System resource monitor |
| **zsh** | Shell (also installs Oh-My-Zsh framework) |

Additional utilities installed as Homebrew dependencies: lazydocker, lazygit, git-filter-repo, graphviz, and others (106 formulas total).

### Fonts

Input Mono font family (all weights and variants) installed to:
- **macOS**: `~/Library/Fonts`
- **WSL**: Windows fonts directory via PowerShell

Automatically configures git, GPG signing, shell aliases, and syncs settings across machines.

## Tool Management

This repository uses [mise](https://mise.jdx.dev/) for unified tool version management.

### Installation

mise is automatically installed by `setup.sh`. To install manually:

```bash
curl https://mise.jdx.dev/install.sh | sh
```

### Usage

All tools and versions are defined in `.mise.toml`. To install all tools:

```bash
mise install
```

To update all tools to their latest versions:

```bash
mise upgrade --bump
```

To check for outdated tools:

```bash
mise outdated
```

### Tool Versions

Most tools are pinned to `latest` for automatic updates. To pin a specific version, edit `.mise.toml`:

```toml
[tools]
go = "1.23.3"  # Pin specific version
bun = "latest"  # Always use latest
```

### Per-Project Tool Versions

mise supports per-project tool versions. In any project, create a `.mise.toml`:

```toml
[tools]
go = "1.21.0"  # Project-specific Go version
node = "20.0.0"
```

mise will automatically activate these versions when you enter the directory.

## Configurations

All configurations are automatically symlinked during setup from this repository to your home directory.

### Shell Configuration (.zshrc)

**Environment**:
- XDG Base Directory compliance
- EDITOR set to `hx` (Helix)
- Extended PATH: `~/.local/bin`, `~/.local/share/cargo/bin`, `~/go/bin`
- History: 20,000 saved commands with deduplication

**Aliases** (navigation):
- `..` → `cd ..`
- `...` → `cd ../..`
- `ls`, `ll`, `la`, `tree` → eza variants

**Aliases** (git shortcuts):
- `gst` → `git status`
- `ga` → `git add`
- `gc` → `git commit`
- `gd` → `git diff`
- `gds` → `git diff --staged`
- `gl` → `git log`
- `gcob` → fuzzy branch checkout (fzf)
- `glf` → fuzzy log viewer (fzf)

**Aliases** (mise shortcuts):
- `mi` → `mise`
- `mii` → `mise install`
- `miu` → `mise upgrade`
- `mis` → `mise use`
- `mil` → `mise list`
- `mio` → `mise outdated`

**Aliases** (utilities):
- `rc` → edit shell config in $EDITOR
- `myip` → get public IP address
- `ports` → show listening ports
- `bootstrap` → re-run setup from secrets server

**Integrations**:
- Homebrew (auto-detected across macOS/Linux)
- mise (tool version management)
- Bun (JavaScript runtime)
- Starship (prompt)
- fzf (fuzzy finder)
- zoxide (smart cd)

### Helix Editor (.config/helix/config.toml)

- **Theme**: gruvbox
- **Line numbers**: relative
- **Auto-save**: enabled
- **Completion**: triggers after 1 character
- **Idle timeout**: 0 (instant responsiveness)
- **True color**: enabled
- **Bufferline**: shows multiple buffers
- **Rulers**: at columns 80 and 120
- **Cursor**: bar in insert mode, block in normal mode
- **File picker**: shows hidden files
- **LSP**: messages displayed
- **Whitespace**: visible (tabs as `>`, newlines as `¬`)
- **Indent guides**: enabled with `┆` character

### Zellij Terminal Multiplexer (.config/zellij/config.kdl)

- **Theme**: gruvbox-dark
- **Default mode**: normal (use Alt+g to lock)
- **Pane frames**: disabled
- **Startup tips**: disabled
- **Keybindings**: Custom with tmux compatibility (Ctrl+b prefix)
- **Navigation**: Vim-style (hjkl) and arrow keys
- **Tabs**: Alt+t for tab mode, Alt+1-9 for quick switching
- **Panes**: Alt+p for pane mode, Ctrl+n for new pane
- **Resize**: Alt+n for resize mode
- **Search**: Alt+s for scroll/search mode

### Git Configuration (.gitconfig)

**User**:
- Name: dane
- Email: dane@medieval.software
- GPG signing key: 7B5FC82E53B5ABE6 (auto-imported from secrets)

**Settings**:
- Default branch: `main`
- Auto-setup remote on push
- GPG commit signing: enabled
- Editor: `hx` (Helix)
- Pager: `delta` with navigation
- Diff algorithm: histogram
- Merge conflict style: zdiff3
- Branch sorting: by commit date (newest first)
- Auto-prune on fetch
- Rerere: enabled (reuse recorded resolutions)

**Git Aliases**:
- `st` → status
- `co` → checkout
- `br` → branch
- `lg` → log --graph --oneline --decorate
- `cm` → commit -m
- `amend` → commit --amend --no-edit
- `uncommit` → reset --soft HEAD~1
- `unstage` → reset HEAD --
- `last` → log -1 HEAD
- `branches` → branch -a
- `remotes` → remote -v
- `contributors` → shortlog -sn

### Tealdeer (tldr client) (.config/tealdeer/config.toml)

- **Auto-update**: enabled (every 30 days)
- **Compact mode**: disabled (full examples)
- **Pager**: disabled (direct output)
- **Title**: hidden
- **Styling**: Custom colors (cyan commands/code, green example text)

### Claude CLI (.claude/)

- **Model**: sonnet (Claude Sonnet 4.5)
- **Always thinking**: enabled
- **Custom instructions**: Environment-specific tool usage guidelines (CLAUDE.md)

### iTerm2 (macOS only)

Preferences symlinked from `Library/Preferences/com.googlecode.iterm2.plist`:
- Custom color schemes and fonts
- Keybindings and profiles
- Restart iTerm2 after setup for changes to take effect

### Windows Terminal (WSL only)

Settings merged from `configs/windows-terminal.json`:
- Font configuration
- Color schemes
- Profile settings

## Secrets Management

AES-256 encrypted storage via Cloudflare Workers. Data is encrypted client-side before upload.

### Commands

| Command | Purpose |
|---------|---------|
| `secrets add <file>` | Track a file |
| `secrets push` | Encrypt and upload |
| `secrets pull` | Download and decrypt |
| `secrets list` | Show local and remote files |
| `secrets groups` | List all groups |
| `secrets delete <group>` | Remove a group |

### Named Groups

```bash
secrets add ~/.ssh/github_key -g github
secrets push github
secrets pull github
```

### Security Model

1. Client-side AES-256-CBC encryption before upload
2. PBKDF2 key derivation from passphrase
3. Encrypted storage in Cloudflare KV
4. HTTPS transport security
5. Bearer token authentication

Data remains encrypted even with full Cloudflare account access.

### Worker Deployment

```bash
npm install -g wrangler
cd worker
wrangler login
wrangler kv:namespace create SECRETS
# Update wrangler.toml with KV namespace ID
wrangler secret put SECRET_PASSPHRASE
wrangler deploy
```

## Backup and Restore

### iTerm2 Settings (macOS)

Backup current iTerm2 preferences:
```bash
./scripts/backup-iterm.sh
```

Settings are automatically symlinked during `./setup.sh`. Restart iTerm2 after setup.

### Fonts (macOS)

Backup Input Mono fonts:
```bash
./scripts/backup-fonts.sh
```

Fonts are automatically installed during `./setup.sh`.



## Keyboard Shortcuts

Configured via shell integrations (fzf, zoxide):

| Key | Action | Tool |
|-----|--------|------|
| `Ctrl+R` | Search command history | fzf |
| `Ctrl+T` | Fuzzy find files | fzf |
| `Alt+C` | Fuzzy find directories | fzf |
| `z <partial>` | Jump to directory by frecency | zoxide |
| `zi` | Interactive directory picker | zoxide |

## Requirements

| Requirement | Notes |
|-------------|-------|
| macOS or WSL | - |
| bash or zsh | Auto-detected |
| Internet | For dependencies |
| Windows Terminal | WSL only |
| Cloudflare account | Optional, for secrets storage |

## System-Specific Overrides

Additional shell configurations can be placed in `~/.config/zsh.d/`:
- Files with `.zsh` extension are automatically sourced
- Use for machine-specific settings (Docker, secrets, etc.)
- These override defaults from `.zshrc`

## Updates

```bash
bootstrap  # Re-download and run latest setup
```

This updates all snippets and reloads your shell configuration.

## File Structure

```
.
├── bootstrap.sh                             # One-liner installer
├── setup.sh                                 # Main installation script
├── secrets                                  # Secrets management CLI
├── .zshrc                                   # Zsh shell configuration
├── .gitconfig                               # Git configuration
├── .gitignore_global                        # Global gitignore patterns
├── .config/                                 # XDG config directory
│   ├── mise/config.toml                     # mise tool versions and config
│   ├── helix/config.toml                    # Helix editor settings
│   ├── zellij/config.kdl                    # Zellij terminal multiplexer
│   └── tealdeer/config.toml                 # tldr client styling
├── .claude/                                 # Claude CLI configuration
│   ├── CLAUDE.md                            # Custom instructions
│   └── settings.json                        # Claude settings
├── Library/Preferences/                     # macOS preferences
│   └── com.googlecode.iterm2.plist          # iTerm2 settings
├── configs/
│   └── windows-terminal.json                # Windows Terminal settings (WSL)
├── fonts/                                   # Input Mono font family
│   └── *.ttf                                # TrueType fonts
├── scripts/                                 # Helper scripts
│   ├── backup-fonts.sh                      # Export fonts from system
│   ├── backup-iterm.sh                      # Export iTerm2 preferences
│   └── install_fonts.ps1                    # Windows font installer (WSL)
└── worker/                                  # Cloudflare Worker for secrets
    ├── index.js                             # Worker implementation
    ├── wrangler.toml                        # Deployment config
    └── README.md                            # Worker documentation
```
