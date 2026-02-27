# Conventional Commits — prefixes for Git messages

*A practical, widely used convention for commit messages. Helps read history and generate changelogs.*

---

## Format

```
<type>(optional-scope): <short summary>
```

| Part | Meaning |
|------|---------|
| **type** | The kind of change (prefix). |
| **scope** (optional) | The area/module affected (e.g. api, auth, docs). |
| **summary** | Short summary, imperative present tense ("add", "fix", "update"). |

### Full format examples

- `feat(api): add endpoint for user profiles`
- `fix(auth): handle expired refresh token`
- `docs(readme): add local setup instructions`

---

## Most used prefixes (types)

### `feat:`
**When:** you add a new feature (user-facing or API).

- `feat: add export to CSV`
- `feat(ui): add dark mode toggle`

### `fix:`
**When:** you fix a bug.

- `fix: prevent crash on empty input`
- `fix(parser): handle trailing commas`

### `docs:`
**When:** documentation-only changes.

- `docs: update installation steps`
- `docs(api): document pagination parameters`

### `style:`
**When:** formatting that doesn't change behavior (whitespace, lint, etc.).

- `style: format code with ruff`
- `style(css): reorder imports`

### `refactor:`
**When:** you restructure code without changing external behavior. Not a bug fix, not a new feature.

- `refactor: extract validation helper`
- `refactor(core): simplify config loading`

### `perf:`
**When:** performance improvements.

- `perf: reduce query allocations`
- `perf(db): batch writes to reduce latency`

### `test:`
**When:** you add or update tests.

- `test: add regression tests for login`
- `test(api): cover pagination edge cases`

### `build:`
**When:** changes to build tooling or dependencies (pyproject.toml, Docker, bundlers, etc.).

- `build: bump numpy to 2.x`
- `build(docker): optimize image layers`

### `ci:`
**When:** CI/CD config changes (GitHub Actions, pipelines, caches).

- `ci: add mypy job`
- `ci(github): cache poetry downloads`

### `chore:`
**When:** maintenance tasks that don't change the product (scripts, repo hygiene, configs).

- `chore: update pre-commit hooks`
- `chore(scripts): add cleanup utility`

### `revert:`
**When:** you revert a previous commit (Git can generate this message automatically).

- `revert: feat(api): add endpoint for user profiles`

---

## Scopes (optional)

Scopes make history easier to read in larger repos.

*Examples:*
- `feat(auth): add 2FA setup flow`
- `fix(cli): handle missing config file`
- `docs(architecture): describe data pipeline`

---

## Breaking changes

When a commit introduces a breaking change:

**Option A:** Add `!` after type/scope

- `feat!: change config file format`
- `refactor(api)!: rename response fields`

**Option B:** Use a footer in the message

```
feat(api): change response schema

BREAKING CHANGE: `user_id` renamed to `id`.
```

---

## Good commit message examples

| Commit | Situation |
|--------|-----------|
| `feat(rssi): add bayesian filter step` | New feature in rssi module |
| `fix(time): make DST boundary tests pass` | Fix in time module |
| `refactor(storage): isolate dynamodb client creation` | Refactor without changing behavior |
| `perf(pipe): reduce dataframe copies` | Performance improvement |
| `ci: run tests on python 3.11 and 3.12` | CI change |
| `docs: add troubleshooting section` | Documentation only |

---

## Simple rules that work

1. **Short summary** — ideally ≤ 72 characters.
2. **Imperative verbs** — "add", "fix", "remove", "update".
3. **One commit = one logical change** (when possible).
4. Prefer **`refactor:`** over **`chore:`** when you're changing code structure.
5. **`build:`** for dependencies and toolchain; **`ci:`** for pipelines and CI actions.
