# quick-note (qn)

Lightning-fast thought capture from your terminal. Zero friction, auto-organized, searchable.

```bash
$ qn "API timeout issue in payment service"
✅ Saved → 2026-01-30.md

$ qn -t bug,urgent "Memory leak in sync process"
✅ Saved [bug, urgent] → 2026-01-30.md

$ qn -s "payment"
🔍 Found 3 note(s) matching "payment":

  2026-01-30 14:23:01  
  [WORK] API timeout issue in payment service
  ...
```

## Why

- **Zero friction** — capture thoughts without leaving the terminal
- **Auto-organized** — daily files, timestamps, context tags
- **Searchable** — full-text search across all notes instantly
- **No dependencies** — just Node.js, no npm install needed
- **Configurable** — works anywhere, respects your directory structure

## Install

```bash
# Clone and link
git clone https://github.com/clawdikson/quick-note.git
cd quick-note
chmod +x quick-note
sudo ln -sf "$(pwd)/quick-note" /usr/local/bin/qn
```

**Requires:** Node.js 18+

## Usage

```bash
# Capture a thought
qn "your note here"

# Tag it
qn -t meeting,action "Follow up with team on deployment"

# Search everything
qn -s "deployment"

# Recent notes
qn -l        # last 10
qn -l 5      # last 5

# Stats
qn --stats
```

## How it works

Notes are stored as clean markdown files:

```
~/.quick-notes/
├── 2026-01-28.md     # Daily file
├── 2026-01-29.md
├── 2026-01-30.md
└── all-notes.md      # Master searchable file
```

Each note entry:
```markdown
## 2026-01-30 14:23:01 #bug #urgent
[WORK] Memory leak in sync process
```

- **Timestamps** — auto-generated in your system timezone
- **Context tags** — `[WORK]`, `[PERSONAL]`, `[GENERAL]` detected from your current directory
- **Hash tags** — custom tags via `-t`

## Configuration

All config via environment variables (add to your `.bashrc` / `.zshrc`):

```bash
# Custom notes directory (default: ~/.quick-notes)
export QN_NOTES_DIR="$HOME/notes/quick"

# Auto-detect work directories (comma-separated patterns)
export QN_WORK_DIRS="monorepo,beena,company"

# Auto-detect personal directories
export QN_PERSONAL_DIRS="personal,clawd,dotfiles"
```

## Options

| Flag | Description | Default |
|------|-------------|---------|
| `"text"` | Save a note | — |
| `-t tags "text"` | Save with comma-separated tags | No tags |
| `-s "query"` | Search all notes | — |
| `-l [N]` | List recent N notes | 10 |
| `--stats` | Show capture statistics | — |
| `-v` | Version | — |
| `-h` | Help | — |

## Use cases

**CTO / Dev Lead:**
```bash
qn "Need to revisit auth flow — token refresh is flaky"
qn -t standup "Shipped invoice generation, need QA on PDF export"
qn -t decision "Going with Playwright over Puppeteer for IRAP recorder"
```

**Deep work protection:**
```bash
# Capture interrupting thoughts without context switching
qn "Check if AWS bill spike is from Lambda cold starts"
qn -t later "Read that article about prediction markets"
```

**Meeting notes:**
```bash
qn -t meeting,ayush "Agreed on April 7 IRAP milestone — need 3 more docs"
qn -t meeting,hiring "Full-stack dev: prioritize Node+React, 3yr exp minimum"
```

## License

MIT
