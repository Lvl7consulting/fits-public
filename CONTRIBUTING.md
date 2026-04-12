# Contributing to fits-public

## Local Setup

1. Clone the repository: `git clone https://github.com/Lvl7consulting/fits-public.git`

## Install Git Hooks

```
./scripts/install-hooks.sh
```

## Local Git Setup

Run these once after cloning:

```bash
git config pull.rebase true
git config core.autocrlf input
git config push.autoSetupRemote true
git config init.defaultBranch main
```

## Adding a New Release

1. Add a new entry to `changelog.md` in Keep a Changelog format:
   ```markdown
   ## [vX.Y.Z] - YYYY-MM-DD
   
   ### Added
   - ...
   
   ### Fixed
   - ...
   ```
2. Update `feeds/changelog.xml` with the new RSS item
3. Commit: `chore: release vX.Y.Z`

## Branch Naming

| Prefix | Use for |
|--------|---------|
| `chore/` | Releases and maintenance |
| `docs/` | Documentation updates |
| `ci/` | CI changes |

## PR Checklist

- [ ] `changelog.md` entry added in correct format
- [ ] `feeds/changelog.xml` updated with new RSS item
- [ ] XML is valid (run: `xmllint --noout feeds/changelog.xml`)
- [ ] Commit message follows Conventional Commits format
