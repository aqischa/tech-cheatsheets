# Git Fundamentals

> A practical cheatsheet for Git commands, workflows, and common troubleshooting.

---

## 1. What is Git?

Git is a **distributed version control system (VCS)** used to track changes in files and collaborate on software projects.

### Why Use Git?

- Track changes to code
- See who changed what and when
- Revert unwanted changes
- Work on features using branches
- Collaborate with outher developers
- Maintain different versions of a project

> **Git = Version control on your computer**  
> **Github = A platform for hosting Git repositories online**

---

## 2. Git vs GitHub

| Git | GitHub |
|---|---|
| Version control system | Git hosting platform |
| Runs locally | Runs online |
| Tracks file changes | Hosts Git repositories |
| Works without internet | Usually requires internet |
| Command-line tool | Web platform + Git features |

### Example

```text
    Your PC
       |
       | Git
       ↓
Local Repository
       |
       | git push
       ↓
    GitHub
       |
       ⊢ Repository
       ⊢ Pull Request
       ⊢ Issues
       ∟ GitHub Actions
```

---

## 3. Git Repository

A **repository (repo)** is a project tracked by Git.

It contains:
- Project files
- Commit history
- Branches
- Git configuration
- Tracking information

### Create a repository

```bash
git init
```

This creates a `.git` directory.

```text
project/
⊢ .git/
⊢ README.md
⊢ src/
∟ tests/
```

> `.git` contains the information Git uses to track your project.

---

## 4. Git Configuration

Check your Git identity:

```bash
git config --global user.name
git config --global user.email
```

Ser your identity:

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

View all configurations:

```bash
git config --list
```

> Your Git username/email is associated with your commits. It is not the same thing as your GitHub login credentials.

---

## 5. Git workflow

The basic Git workflow is:

```text
Working Directory
        |
        | git add
        ↓
   Staging Area
        |
        | git commit
        ↓
Local Repository
        |
        | git push
        ↓
Remote Repository
```

### The basic cycle

```bash
git status
git add .
git commit -m "Add feature"
git push
```

---

## 6. Check Repository Status

```bash
git status
```

Shows:
- Modified files
- Untracked files
- Staged files
- Current branch
- Changes that can be committed

### Example

```text
On branch main

Changes not staged for commit:
    modified: README.md

Untracked files:
    test.py
```

> `git status` is one of the most useful Git commands.  
> When unsure what state your repository is in, check `git status` first.

---

## 7. Add Changes to the Staging Area

Stage a specific file:

```bash
git add README.md
```

Stage multiple files:

```bash
git add file1.py file2.py
```

Stage everything:

```bash
git add .
```

### Workflow

```text
Modified file
      ↓
   git add
      ↓
Staged file
```

> `git add` does not commit your changes.  
> It prepares the changes for the next commit.

---

## 8. Commit changes

Create a commit:

```bash
git commit -m "Add networking cheatsheet"
```

A commit is a snapshot of staged changes.

### Good commit messages

```bash
git commit -m "Add Git fundamentals cheatsheet"
```

### Avoid bague messages

```bash
git commit -m "update"
git commit -m "changes"
git commit -m "stuff"
```

> A good commit message should describe what changed.

---

## 9. View Commit History

Basic history:

```bash
git log
```

Compact history:

```bash
git bash --oneline
```

Example:

```text
a82f91c Add Git cheatsheet
31d9c20 Update networking cheatsheet
8f1a2bd Initial commit
```

### Why use `--oneline`?

It gives a quick overview of the repository history.

---

## 10. View Changes

See unstaged changes:

```bash
git diff
```

See staged changes:

```bash
git diff --staged
```

### Difference

```text
    git diff
        ↓
Changes not staged

git diff --staged
        ↓
Changes already staged
```

---

## 11. Clone a Repository

Clone an existing repository:

```bash
git clone <repository-url>
```

Example:

```bash
git clone https://github.com/user/project.git
```

This downloads the repository to your computer.

```text
GitHub Repository
        |
        | git clone
        ↓
   Your Computer
```

---

## 12. Remote Repository

A remote repository is a repository hosted somewhere else, commonly GitHub.

Check remote:

```bash
git remote -v
```

Example:

```text
origin  https://github.com/user/project.git (fetch)
origin  https://github.com/user/project.git (push)
```

> `origin` is the conventional name for the main remote repository

---

## 13. Push Changes

Send local commits to the remote repository:

```bash
git push
```

For the first push of a new branch:

```bash
git push -u origin main
```

### Basic flow

```text
Local Repository
        |
        | git push
        ↓
GitHub Repository
```

> `git commit` saves changes locally  
> `git push` sends those commits to the remote repository

---

## 14. Pull Changes

Download changes from the remote repository and integrate them:

```bash
git pull
```

Typical workflow:

```text
    GitHub
       |
       | git pull
       ↓
Local Repository
```

Use `git pull` when the remote repository may contain changes you don't have locally.

---

## 15. Fetch vs Pull

`git fetch`

Downloads information about remote changes without automatically integrating them.

```bash
git fetch
```

```text
Remote Repository
        |
        | git fetch
        ↓
    Local Git
        |
        ∟ Your files remain unchanges
```

`git pull`

Fetches remote changes and integrate them into your current branch.

```bash
git pull
```

```text
Remote Repository
        |
        | fetch
        ↓
    Local Git
        |
        | integrate
        ↓
  Current Branch
```

### Quick comparison

| Command | Downloads remote changes | Changes working files |
|---|---|---|
| `git fetch` | Yes | No |
| `git pull` | Yes | Usually yes |

> Use `fetch` when you want to inspect changes first.  
> Use `pull` when you're ready to integrate them.

---

## 16. Git Branches

A branch is an independent line of development.

Example:

```text
main
|
⊢ feature/login
|
⊢ feature/api-testing
|
∟ bugfix/server-check
```

Branches allow you to work on changes without directly modifying `main`.

---

## 17. View Branches

View local branches:

```bash
git branch
```

View local and remote branches:

```bash
git branch -a
```

Example:

```text
* main
  feature/api-testing
  feature/login
```

> `*` shows your current brnach.

---

## 18. Create a Branch

Create a new brnach:

```bash
git branch feature/api-testing
```

Create and switch to it:

```bash
git switch -c feature/api-testing
```

Older equivalent:

```bash
git checkout -b feature/api-testing
```

### Recommended

```bash
git switch -c feature/api-testing
```

`git switch` is specifically designed for branch switching and is wasier to understand than using `checkout` for everything.

---

## 19. Switch Branches

```bash
git switch main
```

Switch to another branch:

```bash
git switch feature/api-testing
```

Check your current branch:

```bash
git branch
```

---

## 20. Basic Branch Workflow

```text
        main
          |
          | git switch -c feature/login
          ↓
    feature/login
          |
          ⊢ make changes
          ⊢ git add
          ⊢ git commit
          |
          ↓
    Pull Request
          |
          ↓
        main
```

> **Typical idea:**  
> Create branch → Make changes → Commit → Push → Pull Request → Merge

---

## 21. .gitignore

`.gitignore` tells Git which file or directories should not be tracked.

Example:

```text
.venv/
__pycache__/
.env
*.log
```

### Example Python project

```text
project/
⊢ .gitignore
⊢ requirements.txt
⊢ src/
∟ tests/
```

Example `.gitignore`:

```gitignore
.venv/
__pycache__/
*pyc
.env
```

> Never commit sensitive information such as passwords, API keys, tokens, or private credentials.

---

## 22. Git Quick Reference

| Task | Command |
|---|---|
| Initialize repo | `git init` |
| Clone repo | `git clone <url>` |
| Check status | `git status` |
| Stage file | `git add <file>` |
| Stage everything | `git add .` |
| Commit | `git commit -m "message"` |
| View history | `git log` |
| Short history | `git log --oneline` |
| View changes | `git diff` |
| View stagd changes | `git diff --staged` |
| View remote | `git remote -v` |
| Download + integrate | `git pull` |
| Download only | `git fetch` |
| Push | `git push` |
| List branches | `git branch` |
| Create branch | `git branch <name>` |
| Create + switch branch | `git switch -c <name>` |
| Switch branch | `git switch <name>` |

---

## 23. Basic Troubleshooting Mindset

When something goes wrong with Git:

```text
1. Check your current state
            ↓
        git status

2. Check your branch
            ↓
        git branch

3. Check your changes
            ↓
        git diff

4. Check your history
            ↓
        git log --oneline

5. Check your remote
            ↓
        git remote -v
```

### Remember
> Don't immediately run random Git commands when something goes wrong.  
> First understand the current state of the repository.

---

## 24. Common Git Problems

### "I forgot which branch I'm on"

```bash
git branch
```

or:

```bash
git status
```

---

### "I made changes but don't see them in the commit"

Check:

```bash
git status
```

Then stage them:

```bash
git add <file>
```

---

### "I committed but GiHub doesn't show any changes"

Check:

```bash
git status
```

Then:

```bash
git push
```

---

### "Git says my branch is behind"

Get the latest remote changes:

```bash
git pull
```

---

### "I don't know which remote repository I'm connected to"

```bash
git remote -v
```

---

## 25. Git Mental Model

Think of Git as **three main areas**:

```text
┌─────────────────────┐
│  Working Directory  │
│                     │
│  Your file changes  │
└──────────┬──────────┘
           │
        git add
           ↓
┌─────────────────────┐
│   Staging Area      │
│                     │
│ Changes selected    │
│ for next commit     │
└──────────┬──────────┘
           │
      git commit
           ↓
┌─────────────────────┐
│ Local Repository    │
│                     │
│ Commit history      │
└──────────┬──────────┘
           │
       git push
           ↓
┌─────────────────────┐
│ Remote Repository   │
│      (GitHub)       │
└─────────────────────┘
```

### Core idea

```text
edit
↓
git add
↓
git commit
↓
git push
```

---
