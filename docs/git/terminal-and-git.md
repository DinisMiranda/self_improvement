# Terminal commands: navigation and Git

*Basic commands to move around your machine in the terminal and to use Git. You're learning — go at your own pace.*

---

## Part 1 — Navigating the computer

The terminal works with **directories** (folders). You're always "inside" one. These commands help you see where you are and move around.

### `pwd` — Where am I?
- Shows the **full path** of the directory you're in.
- *Example:* if you see `.../self_improvement`, that's your current directory.

### `ls` — What's here?
- Lists files and directories in the current directory.
- **`ls -l`** — more details (size, dates).
- **`ls -a`** — includes hidden files (e.g. `.git`).

### `cd` — Change directory
| Command | What it does |
|---------|---------------|
| `cd folder_name` | Enter that folder (it must exist) |
| `cd ..` | Go up one level (parent directory) |
| `cd` | Go to your user home directory |
| `cd /full/path` | Go directly to that path |

> **Tip:** on macOS/Linux type the first letters of the name and press **Tab** — the terminal will complete it.

### `mkdir` — Create a directory
- **`mkdir new_folder_name`** — creates a directory with that name in the current directory.

### `clear` — Clear the screen
- Clears the terminal text. Does not delete files; just clears the display.

---

## Part 2 — Git (project versions)

Git stores **versions** of your project. You can go back if something goes wrong or see what changed.

### `git status` — What changed?
- Shows which branch you're on and which files were modified, added, or are untracked.
- *Use it whenever you want to know the project state.*

### `git init` — Start using Git
- Do this **once** per project. Creates the hidden `.git` directory and turns the project into a "Git project".

### `git add` — Stage files
- **`git add filename`** — stages that file.
- **`git add .`** — stages all changed files.
- "Stage" = mark to be included in the next "snapshot" (commit).

### `git commit` — Save a version
- **`git commit -m "Description of what you did"`** — saves the changes you staged, with a short message.
- *Example:* `git commit -m "Add prompts file"`.

### `git log` — View history
- Lists commits (saved versions), newest first.
- *Press **q** to exit.*

### `git diff` — See differences
- Shows line-by-line what changed in files not yet staged. Useful before committing.

### `git branch` — Branches
- **`git branch`** — lists branches (current one has `*`).
- **`git branch branch_name`** — creates a new branch. Useful for trying things without affecting main code.

### `git checkout` — Switch branch or restore file
- **`git checkout branch_name`** — switch to that branch.
- **`git checkout -- filename`** — discard changes in that file. *Warning: you lose unstaged changes.*

### `git pull` — Fetch from remote
- Fetches changes from GitHub (or elsewhere) and merges them into your local project.
- *Do this before starting work if someone else might have changed the repo.*

### `git push` — Push to remote
- After committing, **`git push`** sends your commits to GitHub. They're stored in the cloud.

---

## Quick summary

**Navigation:** `pwd` = where am I · `ls` = what's here · `cd` = change directory · `mkdir` = create directory

**Git:** `git status` = what changed · `git add` = stage · `git commit` = save version · `git pull` = fetch · `git push` = push

---

*When in doubt, try things in a test directory. These commands become natural with practice.*
