# Git Tags — Cheatsheet

Tags mark a specific commit as important — usually a release version. Unlike branches, a tag never moves: it permanently points to one commit.

---

## Two Types of Tags

| Type | What it stores | Use it for |
|------|----------------|------------|
| **Annotated** | Full object: author, date, message, optional GPG signature | Releases (recommended) |
| **Lightweight** | Just a name pointing to a commit | Temporary / private markers |

---

## Create

```bash
# Annotated tag on the current commit (recommended)
git tag -a v1.0.0 -m "Release version 1.0.0"

# Lightweight tag
git tag v1.0.0-light

# Tag a specific past commit by its hash
git tag -a v0.9.0 9fceb02 -m "Beta release"
```

## List & Inspect

```bash
git tag                  # List all tags
git tag -l "v1.*"        # List tags matching a pattern
git show v1.0.0          # Show tag details + the commit it points to
```

## Push (tags are NOT pushed by default!)

```bash
git push origin v1.0.0   # Push a single tag
git push origin --tags   # Push all tags at once
```

## Check Out

```bash
git checkout v1.0.0              # Inspect code at a tag (detached HEAD)
git checkout -b hotfix v1.0.0    # Branch off a tag to make changes
```

## Delete

```bash
git tag -d v1.0.0                  # Delete locally
git push origin --delete v1.0.0    # Delete on the remote
```

---

## Versioning Convention — Semantic Versioning

Format: `vMAJOR.MINOR.PATCH` (e.g. `v2.4.1`)

- **MAJOR** — breaking changes
- **MINOR** — new features (backward compatible)
- **PATCH** — bug fixes

---

## Remember

- A tag is a permanent bookmark; a branch is a moving pointer.
- Prefer **annotated** tags for anything you release.
- `git push` ignores tags — push them explicitly.
- To edit code at a tag, branch off it first.
