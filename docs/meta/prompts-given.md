# Prompts you gave (simple explanation)

*This is a summary of what you asked for in another repository. Since it was another project, you don't have the files in front of you — it's described in general terms: the kind of things you asked for.*

---

## In that session

You asked for two things:

1. How to make a repository **"professional"**.
2. A list of all the prompts you had given, in a file.

---

## What was done in the other repo

### Organization
- Clear structure: separate folders for code, config, and scripts.
- **.gitignore** so Git doesn't track unnecessary or sensitive files (e.g. passwords).

### Configuration
- App reading settings from a config file (e.g. .toml).
- An **example** file for others to copy.
- The real file with secrets **outside Git**.
- All of this documented in the README.

### Database and dependencies
- Database connection (MySQL) in one place, reusable.
- Project using **Poetry** to install dependencies and run scripts (instead of manual workarounds).
- Instructions to install Poetry when it wasn't installed.

### Tests
- Automated tests (**Pytest**) for important functions: loading config (good and bad cases) and functions that create sample data.
- Consistent types in code (e.g. `list` instead of `List` in older style).

### Professional project setup
- Complete **pyproject.toml** (authors, license, etc.).
- Documentation and comments in English.
- Each function with a clear description (**docstrings**): what it does, what it takes, what it returns.

### CI and coverage
- Tests running automatically on **GitHub Actions**.
- Measuring test **coverage** (what percentage of code is tested); in some modules the goal was 100%.

### GitHub
- Files like **CODEOWNERS** and **Dependabot** to keep dependencies updated.
- Commands to set the repo description and topics on GitHub.

### "Really professional"
At the end you asked for files that serious projects usually have:

| File / thing | What for |
|--------------|----------|
| SECURITY.md | How to report security issues |
| CONTRIBUTING.md | How to contribute to the project |
| CHANGELOG | Changes per version |
| Badges in README | Tests, license, etc. |
| Ruff (linter) | Code formatting and quality |
| GitHub templates | Open bugs and feature requests |

---

## In summary

In the other repo you asked for: **organization**, **secure config**, **tests**, **documentation**, **GitHub automation**, and files that make the project easier to maintain and share.

You can reuse these ideas in any similar project.
