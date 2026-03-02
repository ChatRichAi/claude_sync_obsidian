# Claude Code → Obsidian Sync

> Turn every Claude Code session into a beautiful Obsidian note — automatically.

<p align="center">
  <img src="https://img.shields.io/badge/Claude_Code-Skill-blueviolet?style=for-the-badge&logo=anthropic" alt="Claude Code Skill">
  <img src="https://img.shields.io/badge/Obsidian-Vault_Sync-7C3AED?style=for-the-badge&logo=obsidian" alt="Obsidian">
  <img src="https://img.shields.io/badge/Output-Markdown_+_Canvas-blue?style=for-the-badge" alt="Dual Output">
  <img src="https://img.shields.io/badge/Projects-Auto_Detect-green?style=for-the-badge" alt="Auto Detect">
</p>

---

## The Problem

You use Claude Code to plan features, fix bugs, and build systems. But when the session ends, all that context — the decisions, the file changes, the reasoning — lives only in the terminal history. Gone.

## The Solution

**One command. Two outputs. Zero config per project.**

```
/sync-obsidian report
```

This produces:

| Output | Format | What You Get |
|--------|--------|--------------|
| **Markdown Note** | `.md` | Structured report with summary, file changes, design decisions, TODOs |
| **Visual Canvas** | `.canvas` | Interactive node graph with color-coded groups and connected flow |

Both files land in your Obsidian vault under `[Project] {auto-detected-name}/`, instantly searchable and linkable.

---

## Quick Start

### 1. Install the Skill

```bash
# Clone to your Claude Code skills directory
git clone https://github.com/ChatRichAi/claude_sync_obsidian.git ~/.claude/skills/sync-obsidian
```

### 2. Set Your Vault Path

Edit `~/.claude/skills/sync-obsidian/SKILL.md` — update **one line**:

```
OBSIDIAN_VAULT = /Users/you/Documents/Obsidian Vault
```

That's it. The project name is auto-detected from your git repo or directory name.

### 3. Use It

```bash
# In any Claude Code session, in any project:
/sync-obsidian report                # Sync a work report
/sync-obsidian plan                  # Sync the latest plan
/sync-obsidian report Auth Refactor  # With a custom title
```

---

## Auto Project Detection

No per-project configuration needed. The skill detects your project name automatically:

| Priority | Method | Example |
|----------|--------|---------|
| 1st | Git repo name | `my-app/` → `[Project] my-app/` |
| 2nd | Directory name | `~/code/my-app/` → `[Project] my-app/` |

Your vault organizes itself:

```
Obsidian Vault/
├── [Project] my-app/
│   ├── [Report] Auth Refactor (2026-03-02).md
│   ├── [Plan] Database Migration (2026-03-02).md
│   └── canvas/
│       ├── [Report] Auth Refactor (2026-03-02).canvas
│       └── [Plan] Database Migration (2026-03-02).canvas
├── [Project] my-api/
│   ├── [Report] Rate Limiting (2026-03-01).md
│   └── canvas/
│       └── ...
```

Directories are auto-created when needed.

---

## What Gets Synced

### Reports (`/sync-obsidian report`)

After you finish coding, refactoring, or debugging:

```
[Report] Auth Refactor (2026-03-02).md
```

Contains:
- **Summary** — 1-3 sentence overview
- **Completed Work** — what was built, with technical details
- **File Changes** — table of every file touched
- **Design Decisions** — why you chose approach A over B
- **Follow-up TODO** — next steps checklist

### Plans (`/sync-obsidian plan`)

After discussing and approving a plan:

```
[Plan] Database Migration (2026-03-02).md
```

Contains the full plan content from `.claude/plans/`, preserved with all technical details.

### Canvas Maps (Both)

Every sync also generates a `.canvas` file — an interactive visual map:

```
canvas/[Report] Auth Refactor (2026-03-02).canvas
```

- Color-coded groups: Summary (cyan) → Work (pink) → Files (purple) → Decisions (green) → TODO (orange)
- Connected edges showing the flow of work
- Sized to display all content without clipping

---

## Auto-Sync (Set and Forget)

Add auto-sync rules to `CLAUDE.md` and never think about syncing again.

**Option A: Global (all projects)** — add to `~/.claude/CLAUDE.md`:

**Option B: Per-project** — add to your project's `CLAUDE.md`:

Either way, paste this:

```markdown
## Auto Sync to Obsidian

### Plan Sync (Before Implementation)

When a plan discussion is complete, call `/sync-obsidian plan` FIRST
so you can review it in Obsidian before giving the green light.

Trigger: plan finalized, user shows approval intent, before implementation starts.

### Report Sync (After Implementation)

After completing substantive work, call `/sync-obsidian report` before the session ends.

Trigger: code files changed, plan implemented, important decisions made.

### Do NOT trigger when:
- Pure Q&A / casual chat
- Only read files, no modifications
- User explicitly says no sync needed
```

The full lifecycle: **Discuss → Sync plan → Review in Obsidian → Approve → Implement → Sync report**

Every productive Claude Code session automatically becomes a searchable Obsidian note.

---

## Why This Matters

| Without sync | With sync |
|-------------|-----------|
| Context dies with the terminal | Every session is a permanent, searchable note |
| "What did I change last week?" | Open Obsidian, search, done |
| Design decisions lost to scrollback | Explicit decision log with rationale |
| Manual note-taking breaks flow | Zero-friction, auto or one-command |
| Text-only records | Visual Canvas maps for spatial thinkers |
| Config per project | Auto-detect, works everywhere |

---

## Customization

### Naming Convention

The default naming uses bracket labels: `[Plan]`, `[Report]`, `[Project]`. You can customize these in `SKILL.md` to match your vault's conventions (e.g., Chinese brackets `「Plan」`, emoji prefixes, etc.).

### Canvas Layout

The Canvas sizing rules in `SKILL.md` are tuned to prevent content clipping. Key parameters you can adjust:

- **Node width**: 500-660px (default) — wider for longer content
- **Height formula**: `line_count × 35 + 60` — increase multiplier for larger fonts
- **Group padding**: 20px — increase for more breathing room
- **Group gap**: 80px — increase for sparser layouts

---

## Requirements

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) (CLI)
- [Obsidian](https://obsidian.md/) (any version)
- That's it. No plugins, no API keys, no build step.

---

## License

MIT

---

<p align="center">
  <i>Built with Claude Code. Synced with this skill. Meta? Yes.</i>
</p>
