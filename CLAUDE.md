# CLAUDE.md — fits-public

## Project Overview

Public changelog and RSS feed repository for FITS (Framework for IT Security). Publishes release notes and version history for the FITS GRC platform. Provides a Markdown changelog and an RSS/Atom XML feed for subscribers.

- **Language / Runtime**: Markdown, XML (no build system)
- **Framework**: Static files, GitHub Pages
- **Architecture**: Flat file structure — changelog.md + feeds/changelog.xml
- **Package / Namespace**: `Lvl7consulting/fits-public`

---

## Required Skills — ALWAYS Invoke These

These skills **must** be invoked when the relevant situation arises. Never skip them.

| Situation | Skill |
|-----------|-------|
| Before any new feature or screen | `superpowers:brainstorming` |
| Planning multi-step changes | `superpowers:writing-plans` |
| Writing or fixing core logic | `superpowers:test-driven-development` |
| First sign of a bug or failure | `superpowers:systematic-debugging` |
| Before completing a feature branch | `superpowers:requesting-code-review` |
| Before claiming any task done | `superpowers:verification-before-completion` |
| Working on UI / frontend | `frontend-design:frontend-design` |
| After implementing — reviewing quality | `simplify` |

---

## Architecture

```
fits-public/
├── changelog.md         ← Human-readable release notes (Markdown)
├── feeds/
│   └── changelog.xml    ← RSS feed for subscribers
└── fits-public/         ← Nested copy (mirror structure)
    ├── changelog.md
    └── feeds/
        └── changelog.xml
```

### Rules
- `changelog.md` entries follow the format: `## [vX.Y.Z] - YYYY-MM-DD`
- RSS feed must be kept in sync with changelog.md on every release
- No build step required — files are served directly via GitHub Pages

---

## Coding Conventions

- [ ] Changelog entries use Keep a Changelog format
- [ ] Version tags follow semantic versioning: `vMAJOR.MINOR.PATCH`
- [ ] RSS feed updated simultaneously with changelog.md

---

## Engineering Principles

### DRY · KISS · YAGNI
- Keep the changelog format consistent — one entry per version
- Don't add complexity that isn't needed

### Commit hygiene
- Follow Conventional Commits: `chore: ...` / `docs: ...`
- The `commit-msg` hook enforces this automatically

---

## Build Commands

```bash
# No build commands — static files only
# Validate XML feed:
xmllint --noout feeds/changelog.xml
```

---

## Key Files

| File | Purpose |
|------|---------|
| `CLAUDE.md` | This file — project conventions and session startup |
| `changelog.md` | Main release notes file |
| `feeds/changelog.xml` | RSS feed |
| `.github/workflows/ci.yml` | Validate XML on PRs |
| `.githooks/commit-msg` | Conventional Commits enforcement |
| `scripts/install-hooks.sh` | One-time hook installer |

---

## Starting a New Session

1. Read this file
2. Check `changelog.md` for the current version
3. Follow the Required Skills table — every skill is mandatory, not optional
