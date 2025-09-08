---
title: Comprehensive Git Reviewer
applyTo: '**'
---

# Introduction to Git

- Git is a free, open-source distributed version control system created by Linus Torvalds in 2005.
- It tracks changes to files, supports collaborative development, and enables rollback to previous states.
- Widely used for software, documentation, configuration, and content projects.
- Unlike traditional systems, Git works locally, provides rapid branching/merging, and enables full history access for
  every user.
- Key concepts:
    - Repository: Folder storing tracked files and change history.
    - Commit: Snapshot of the repository at a given time.
    - Branch: Independent line of development for features, fixes, or experiments.
    - Merge: Integrate changes from one branch to another.
    - Staging area (index): Prepares files for the next commit.
- Modern Git supports signed commits, performant storage, and continual
  improvements—see [Git Release Notes](https://github.com/git/git/blob/master/Documentation/RelNotes/2.51.0.txt) for
  official changelog.

# Version Control Systems: Distributed vs Centralized

## Centralized Version Control (CVCS)

- **Architecture:** Single central server hosts all project files and history (e.g. SVN, Perforce).
- **Workflow:** Developers check out from central repo, make changes, and commit back to server.
- **Pros:** Simple for small teams; easy to control access and enforce policies; one source of truth.
- **Cons:** Vulnerable to server downtime/data loss; single point of failure; limited offline work; scaling issues for
  very large teams.

## Distributed Version Control (DVCS)

- **Architecture:** Every developer has a full copy of the repository, including its history (e.g. Git, Mercurial).
- **Workflow:** Changes are made and committed locally (offline); synchronization happens via push/pull with remotes (
  repositories hosted elsewhere).
- **Pros:** Robust backup (since many full copies exist); complete offline capabilities; speed; flexible branching and
  merging; resilient to data loss; encourages parallel development.
- **Cons:** Slightly higher learning curve; initial clones require full download.

## Comparison Table

| Feature                | Centralized VCS (CVCS) | Distributed VCS (DVCS) |
|------------------------|-------------------------|------------------------|
| History Location       | Single server           | Every user             |
| Offline Development    | Limited/no              | Full                   |
| Branching/Merging      | Possible, often clunky  | Fast, seamless         |
| Collaboration Model    | Synchronous only        | Asynchronous possible  |  
| Data Loss Risk         | High (single point)     | Low (many copies)      |
| Scale to Large Teams   | Harder                  | Easier                 |
| Example Tools          | SVN, Perforce           | Git, Mercurial         |

## Best Practices

- Most modern open-source and enterprise projects use distributed systems (especially Git) for resilience, scalability,
  and developer productivity.
- Centralized systems persist for legacy, regulated, or niche use cases.
- Hybrid solutions with distributed clients and centralized hosting (e.g. GitHub, GitLab) combine the best features of
  both models.

For further details, see:

- [Git Fundamentals on freeCodeCamp](https://www.freecodecamp.org/news/learn-git-basics/)
- [GitHub Blog: What is Git?](https://github.blog/developer-skills/programming-languages-and-frameworks/what-is-git-our-beginners-guide-to-version-control/)
- [Devart: Centralized vs Distributed](https://blog.devart.com/centralized-vs-distributed-version-control.html)
- [BuiltIn Version Control Guide](https://builtin.com/articles/version-control-systems)

# Git Installation and Setup

## Download and Install

- **Official downloads:** [git-scm.com/downloads](https://git-scm.com/downloads)
- **Windows:** Download and run the installer. Options for Git Bash or Git CMD/Shell. Latest
  version [here](https://git-scm.com/download/win)
- **macOS:** Use Xcode Command Line Tools (`xcode-select --install`) or direct
  installer [here](https://git-scm.com/download/mac)
- **Linux:** `sudo apt-get install git` (Debian/Ubuntu), `sudo dnf install git` (Fedora), or
  see [instructions](https://git-scm.com/download/linux) for your distro
- **Verifying install:** `git --version` should show the installed version

## Initial Setup (applies to all OS)

- Set your user name and email:
  ```bash
  git config --global user.name "Your Name"
  git config --global user.email "your@email.com"
  ```
- Recommended: Set default branch name, colored UI, and credential helper:
  ```bash
  git config --global init.defaultBranch main
  git config --global color.ui auto
  git config --global credential.helper cache # or "osxkeychain"/"wincred"
  ```
- Check configuration:
  ```bash
  git config --list
  ```
- (Optional): Set up SSH key for GitHub/GitLab.
  See [GitHub SSH guide](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/about-ssh).

## Best practice:

- Choose the latest available version for bug fixes and security updates.
- Use a global config for identity, editor, and default branch across all repositories.

# Git Commands

Here are the most essential commands for daily Git workflows (2024 best practices):

| Command                          | Purpose/Description                    |
|----------------------------------|----------------------------------------|
| `git config`                     | Configure user info, aliases, settings |
| `git init`                       | Initialize a new repository            |
| `git clone <url>`                | Copy (download) an existing repo       |
| `git status`                     | Show changed files and branch info     |
| `git add <file(s)>`              | Stage files for commit                 |
| `git restore --staged <file(s)>` | Unstage changes (modern best practice) |
| `git commit -m "message"`        | Commit staged changes with a message   |
| `git log`                        | View commit history                    |
| `git diff`                       | Show uncommitted changes               |
| `git branch`                     | List, create, or delete branches       |
| `git checkout <branch>`          | Switch branches                        |
| `git restore <file>`             | Restore (discard changes in) a file    |
| `git merge <branch>`             | Merge another branch into current      |
| `git pull`                       | Fetch and merge from remote            |
| `git push`                       | Upload commits to remote repository    |

> **TIP:** Use `git help <command>` or check [official docs](https://git-scm.com/docs) for details.

### Modern Best Practices

- Prefer `main` as your new repository default branch.
- Use descriptive commit messages (see [best practice](https://cbea.ms/git-commit/)).
- Use branches for features, fixes, and experiments—avoid committing directly on main.
- Frequently pull from remote (with `git pull --rebase` for linear history if team agrees).
- Push small, frequent commits rather than large, infrequent ones.
- Clean up local and remote branches regularly if they are no longer needed.
- Enable GPG or SSH signing for secure commits if supported by your platform.

# Git Basics

## Creating a Repository

- Local: Run `git init` in your project directory. This creates a `.git` folder, enabling version control.
- GitHub/GitLab: Use web UI, `gh repo create`, or push a local repo to a remote with:
  ```bash
  git remote add origin <url>
  git push -u origin main
  ```
- Starting with a template or existing code? Make sure `.gitignore` is set before first commit.

## Cloning an Existing Repository

- To clone a remote repo (e.g., from GitHub):
  ```bash
  git clone https://github.com/user/repo.git
  ```
- You’ll get a full local copy with history and branches. Use `--depth 1` for shallow clone (no full history).

## Git Configuration

- View/edit settings with `git config --list`, and set with `git config [--local|--global|--system] ...`
- Best practice options:
  - `user.name` and `user.email`: identity for commits
  - `init.defaultBranch main`: use `main` as default branch
  - `color.ui auto`: colorized output
  - `core.editor`: set your favorite text editor for commits
  - `merge.conflictstyle zdiff3`: improved merge conflict output
  - `rebase.autostash true`: automatically stash locally modified files during rebase
- Aliases for efficiency (example):
  ```bash
  git config --global alias.slog 'log --oneline --decorate --graph --all'
  ```

## Staging and Unstaging

- **Staging**: Prepare changes for commit.
  - Add files: `git add <file>` (or `git add .` to stage everything)
  - Stage part of a file: `git add --patch <file>` for interactive staging
- **Unstaging**:
  - Old/legacy: `git reset <file>`
  - Modern: `git restore --staged <file>` (keeps changes, removes from staged area)
    - Useful to avoid accidentally committing files
- **Tip**: Staging is for assembling accurate, atomic commits—don’t stage partial or unrelated changes together.

## Committing Changes

- Save a snapshot of staged changes:
  ```bash
  git commit -m "A short, meaningful message"
  ```
- Best practices:
  - Write concise, imperative messages (“Add README” not “Added README”)
  - Limit to 50 characters in subject, wrap body at 72
  - Use the body for context, reference issues/PRs if relevant
  - Consider Conventional Commits ([spec](https://www.conventionalcommits.org/en/v1.0.0/)) for larger projects
  - Example:
    ```
    feat: add authentication flow

    Add JWT-based auth and signup screens to improve security. Resolves #42.
    ```
- Amend last commit (if needed): `git commit --amend`

## Checking Status

- View file states and branch details:
  ```bash
  git status
  ```
- Shows:
  - Untracked: files not under version control
  - Staged: files ready to commit
  - Modified: files changed since last commit
  - Branch and remote tracking info
- Best practice: Check status often before and after key actions (add, commit, pull, merge)

# Remote Repositories

## Adding a Remote Repository

- Add a remote (link a name to a remote URL):
  ```bash
  git remote add origin https://github.com/user/repo.git
  git remote add upstream https://github.com/other/source.git
  ```
- **Tip:** ‘origin’ is default for your repo; ‘upstream’ is used for forks or secondaries.
- View and verify remotes:
  ```bash
  git remote -v
  ```
- Change URL: `git remote set-url origin <new-url>`
- Remove remotes: `git remote remove <name>`

## Fetching, Pulling, Pushing

| Command            | Description                                                                                                                                                 |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `git fetch origin` | Download new data from the remote. Doesn’t change your work/branch. Use `git fetch` before merging.                                                         |
| `git pull`         | Fetch and merge remote branch into current one. Always review (`git status`, resolve conflicts) after, and consider `git pull --rebase` for linear history. |
| `git push`         | Upload your commits to remote branch. Default: `git push origin <branch>`                                                                                   |

- Prefer `git fetch` + `git merge` for awareness before incorporating remote changes.
- Pushing to default branch (main) may require permissions; push feature branches for PRs/merges.

## Managing Multiple Remotes

- List remotes: `git remote -v`
- Add as many as you need (e.g., fork = origin, upstream = public source, deploy = private server)
- Push to a specific remote:
  ```bash
  git push origin my-feature
  git push deploy release
  ```
- Fetch from all remotes: `git fetch --all`
- Use `git remote show <name>` for detailed remote config/status

## Authentication: SSH, Tokens, & Best Practices

- **SSH:** Strongly preferred for security and
  automation. [See this guide](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/about-ssh).
  - Generate SSH key: `ssh-keygen -t ed25519 -C "your@email.com"`
  - Add public key to GitHub/GitLab profile. Test with: `ssh -T git@github.com`
- **Personal Access Tokens (PATs):** Used for HTTPS authentication on GitHub/GitLab
  - Treat PATs like passwords; never share or commit them
  - Use environment variables or credential helpers for safety
  - PATs may require renewal/expiration (for compliance)
- **Best Practice:**
  - Avoid password auth (deprecated)
  - Use passphrases for private keys—use SSH agents for convenience
  - Set up 2FA on GitHub/GitLab
  - Remove unused remotes/keys/tokens promptly
  - Inspect history for accidental credential commits: `git log -p`
    and [BFG Repo-Cleaner](https://rtyley.github.io/bfg-repo-cleaner/) if needed

- For further
  details: [Git Remotes Guide](https://git-scm.com/book/en/v2/Git-Basics-Working-with-Remotes), [GitHub: Managing Remotes](https://docs.github.com/en/get-started/git-basics/managing-remote-repositories), [GitHub Authentication](https://docs.github.com/en/authentication)

# Undoing Changes in Git

## Unstaging Changes

- **Remove staged file from commit, keep changes:**
  ```bash
  git restore --staged <file>
  # Old/legacy: git reset <file>
  ```
- **Best practice:** Use 'restore --staged' for modern workflows; use 'git status' to confirm results.

## Discarding Local Changes

- **Undo changes in a file (not staged):**
  ```bash
  git restore <file>
  ```
- **Discard all unstaged changes in working directory:**
  ```bash
  git restore .
  ```
- **Discard staged and unstaged:**
  1. Unstage as above, then restore.
  2. **Danger:** `git reset --hard` resets both staged and unstaged changes (irreversible!).
- **Remove untracked files/dirs:**
  ```bash
  git clean -fd
  ```
  Use only if sure—removes all untracked files/dirs.

## Amending, Resetting, and Reverting Commits

- **Amend last commit (edit message or add files):**
  ```bash
  git commit --amend
  ```
- **Reset:**
  - **Soft:** Keep changes in working dir, move HEAD:
    ```bash
    git reset --soft <commit>
    ```
  - **Mixed (default):** Unstage, keep changes:
    ```bash
    git reset <commit>
    ```
  - **Hard:** Discard all local changes, set HEAD:
    ```bash
    git reset --hard <commit>
    ```
    **Danger!** Irreversible—lost work can't be recovered.
- **Revert:** Create new commit that undoes a previous commit (safe for published history):
  ```bash
  git revert <commit>
  ```
- **Best practice:**
  - Never use `reset --hard` or history-modifying commands on shared branches without consensus.
  - Use `revert` for undoing commits already pushed to a remote that others use.

## Deleting Branches

- **Delete local branch (merged):**
  ```bash
  git branch -d <branch>
  ```
- **Force delete local branch:**
  ```bash
  git branch -D <branch>
  ```
- **Delete remote branch:**
  ```bash
  git push origin --delete <branch>
  ```
- Regularly delete feature/hotfix branches after merging to keep history clean. Prune local refs with `git fetch -p`.

**References:**

- [Undoing Things](https://git-scm.com/book/en/v2/Git-Basics-Undoing-Things)
- [Git Restore vs Reset](https://martinheinz.dev/blog/109)
- [Deleting Branches Guide](https://blog.logrocket.com/delete-branch-git/)

# Excluding Files from Repository

## .gitignore Best Practices

- Add a `.gitignore` to every repository—define project-specific ignore rules.
- Common patterns to ignore:
  - IDE/editor folders (e.g., `.vscode/`, `.idea/`)
  - OS files (e.g., `.DS_Store`, `Thumbs.db`)
  - Dependency folders (`node_modules/`, `venv/`, `target/`)
  - Build/output directories (`dist/`, `out/`, `bin/`)
  - Secrets (`.env`, `*.key`, `*.pem`)
- Never rely solely on `.gitignore` for secrets—use dedicated secret management.
- Multiple `.gitignore` files allowed (root and subfolders); review global/user-level ignores with
  `git config --get core.excludesfile`.
- For already tracked files, updating `.gitignore` is not enough—remove with:
  ```bash
  git rm --cached <file>
  ```

## .gitkeep

- Not an official Git file, but widely used convention.
- Add `.gitkeep` (or any empty file) to force Git to track otherwise empty directories.
- Use `.gitignore` patterns to exclude temp/build content and `.gitkeep` to maintain scaffolding structure.

## Pitfalls

- Don't accidentally ignore key files needed for CI/CD/deploy.
- Double-check that patterns don't inadvertently block required files or leak sensitive ones.
- Use [gitignore.io](https://www.toptal.com/developers/gitignore) for quick language/tool-specific templates.

# Keeping a Clean GIT History

## Commit Strategies

- Make small, focused commits with clear messages.
- Prefer atomic changes (one logical change per commit).
- Write descriptive subject lines (imperative mood, <50 chars), wrap bodies at 72 chars.
- Follow project conventions (e.g., [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/)).
- Rebase (rather than merge) for linear history if team/project agrees; avoid rewriting shared history without
  consensus.
- Squash multiple WIP/fixup commits before merging:
  ```bash
  git rebase -i main
  ```
- Use: `pick` to keep, `squash` or `fixup` to combine commits, `edit` to refine.
- Clean up unnecessary branches after merging/squashing.

## Review Etiquette

- Review all changes in PRs/MRs before merging.
- Resolve merge conflicts locally and confirm results.
- Avoid force-pushing (`git push --force`) to branches used by others—use `--force-with-lease` if needed.
- Use hooks/automation for linting and tests on every commit or PR.
- Document context for key commits (refs, links, comments).

## Tools & Resources

- `git log --oneline --decorate --graph --all` for a visual history graph
- [Interactive Rebase](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)
- [Best practices summary](https://daily.dev/blog/git-best-practices-effective-source-control-management)
- [Squashing Explained](https://medium.com/@kyledeguzmanx/squashing-commits-how-to-maintain-git-commit-history-like-a-pro-69a9ba27ca54)

# Branches and Merging

## Branch Creation

- Create new branch from current base (main/master):
  ```bash
  git branch <branch-name>
  # Or create and switch in one step:
  git switch -c <branch-name>
  ```
- **Naming Best Practices:**
  - Use prefixes (feature/, bugfix/, hotfix/, release/) for clarity, e.g. `feature/login-ui`
  - Use hyphens, reference tickets (e.g. `bugfix/PROJ-123-typo-fix`) when relevant
  - Keep branch names short, descriptive, and consistent
- Branching strategies:
  - **Feature branching** (common): each new feature/fix gets a branch
  - **Trunk-based**: short-lived branches, frequent merges to main
  - **GitFlow**, **Release Flow**, etc. for larger teams/projects

## Switching Branches

- Use new command (recommended):
  ```bash
  git switch <branch-name>
  ```
- To create and switch:
  ```bash
  git switch -c <new-branch>
  ```
- (Legacy, still available): `git checkout <branch>`
- If you have uncommitted changes that prevent switching:
  - Stash them (`git stash`), then switch
  - Or use `git switch --discard-changes <branch>` (danger, discards all local changes)

## Merging Branches

- Merge another branch into current:
  ```bash
  git merge <other-branch>
  ```
- Simple merge (fast-forward): happens if there are no diverging commits
- Three-way merge: if both branches have changes
- For linear project history (if team agrees), consider rebasing instead: `git rebase <branch>`
- Always make sure current branch is up to date before merging (use `git fetch` and optionally `git pull --rebase`)
- Clean up merged feature branches after merging to main to keep history tidy

## Resolving Merge Conflicts

- If files changed on both branches, Git marks conflicts in affected files:
  ```
  <<<<<<< HEAD
  your current branch changes
  =======
  changes from merged branch
  >>>>>>> feature/other-branch
  ```
- Fix each marked section, decide what code to keep. Then stage changes:
  ```bash
  git add <file-with-conflict>
  git merge --continue
  ```
- See all conflicts:
  ```bash
  git status
  ```
- Use merge tools for complex conflicts:
  ```bash
  git mergetool
  ```
  - VS Code and many IDEs include graphical merge editors
- Avoid conflicts by:
  - Pulling/rebasing latest main before long-lived feature branches are merged
  - Keeping branches short-lived and focused
- For advanced workflows,
  see: [GitHub Docs: About Merge Conflicts](https://docs.github.com/articles/about-merge-conflicts), [Resolving Conflicts Guide](https://www.git-scm.com/docs/git-mergetool)
