# Git Branching & Advanced Workflow

> A practical cheatsheet for branches, merging, conflicts, rebasing, and safely undoing Git changes.

---

## 1. What is a Git Branch?

A **branch** is a seperate line of development in a Git repository.

Branches allow you to work on features, fixes, or experiments without directly changing the main branch.

```text
main
|
⊢ feature/login
|
⊢ feature/api-testing
|
∟ bugfix/server-check
```

### Why use branches?
- Keep `main` stable
- Develop features independently
- Fix bugs without affecting other work
- Allow multiple developers to work simultaneously
- Prepare changes for Pull Requests

> Think of a branch as a seperate workspace for your changes.

---

## 2. Main Branch

The main branch is usually the primary branch of a repository.

Common names:

```text
main
master
```

Modern repositories commonly use:

```text
main
```

Example:

```text
main
|
⊢ feature/login
⊢ feature/payment
∟ bugfix/api-error
```

> You generally should avoud making experimental changes directly on `main` when working in a team.

---

## 3. View Branches

View local branches:

```bash
git branch
```

View local and remote branches:

```bash
git branch -a
```

View remote branches:

```bash
git branch -r
```

Example:

```text
* main
  feature/api-testing
  feature/login
```

> `*` indicates the branch you are currently on.

---

