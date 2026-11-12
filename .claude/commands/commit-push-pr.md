---
description: Stage, commit, push, and open a PR for the current change. Manual-only (has side effects).
argument-hint: [optional PR title]
disable-model-invocation: true
shell: powershell
allowed-tools: PowerShell(git add:*), PowerShell(git commit:*), PowerShell(git push:*), PowerShell(git status:*), PowerShell(git diff:*), PowerShell(git branch:*), PowerShell(git checkout:*), PowerShell(git rev-parse:*), PowerShell(gh pr create:*), Bash(git add *), Bash(git commit *), Bash(git push *), Bash(git status *), Bash(git diff *), Bash(git branch *), Bash(git checkout *), Bash(gh pr create *)
---

Current status:
!`git status -sb`

Change summary:
!`git diff --stat HEAD`

Current branch:
!`git branch --show-current`

---

Open a PR for the change above. The base branch for this repo is **`main`**.

1. **Branch safety:** if the current branch IS `main`, create and switch to a new feature branch first — `git checkout -b <short-kebab-name>` derived from the change. NEVER commit directly to `main`.
2. Stage deliberately with `git add` — don't blindly `git add -A`. Remember shared header/nav/footer markup is duplicated across pages; if you changed it, make sure ALL affected pages are staged together.
3. Commit with a concise imperative message summarizing the change. If $ARGUMENTS is provided, use it as the commit/PR title.
4. Push: `git push -u origin HEAD`.
5. Open the PR: `gh pr create --base main --fill` (use `--title`/`--body` if $ARGUMENTS or context gives a better title). Report the PR URL.

Do not force-push, amend, rebase, or reset — those are blocked and unnecessary. If `gh` isn't authenticated, stop and tell me to run `gh auth login`.