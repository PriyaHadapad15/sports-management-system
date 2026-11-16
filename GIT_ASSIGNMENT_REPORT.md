# Git Fundamentals and Branching Strategy — Assignment Report

## 1. Aim

To initialize a small project repository, document a four-developer branching workflow, develop a login page on a feature branch, create and resolve a real merge conflict, and verify the resulting Git history.

## 2. Objectives

- Initialize an isolated Git repository and use `main` as its stable branch.
- Set repository-local author identity without changing global Git settings.
- Document four developers, their feature branches, commit conventions, and merge procedure.
- Implement a simple login page in focused feature commits.
- Make competing edits to the same README line, observe Git's real conflict, resolve it, and merge the feature.
- Verify branches, history, conflict-marker removal, and repository cleanliness.

## 3. Software and tools used

- Git, invoked from PowerShell in the VS Code workspace.
- VS Code workspace at `C:\Users\priya\OneDrive\Desktop\devops`.
- HTML, CSS, and browser-native form validation for the login demonstration.

The project is isolated in `Git-Team-Project`; the containing directory is under a pre-existing parent repository, which was left unchanged. The repository-local Git name and email were set to the values already present in the global configuration. The global configuration was not changed. No remote was configured and nothing was pushed.

## 4. Branching strategy

`main` is the stable integration branch. Each developer starts a separate feature branch from `main`, makes focused commits, tests the changes, and requests review before merging. See [BRANCHING.md](./BRANCHING.md) for the full team assignments and conventions:

| Developer | GitHub username | Responsibility | Branch |
|---|---|---|---|
| Developer 1 | `shrushtib08` | Login functionality | `feature/login` |
| Developer 2 | `tauqeer971` | Registration functionality | `feature/signup` |
| Developer 3 | `Rakshitham15` | Dashboard functionality | `feature/dashboard` |
| Developer 4 | `PriyaHadapad15` | Profile functionality | `feature/profile` |

During the initial Git fundamentals demonstration only `feature/login` was created. In the follow-up completion, all four assignment branches were used and merged into `main`. The local demonstration commits were made using the repository's configured Git identity; listing GitHub usernames documents intended ownership and does not claim that each account authored commits or has repository access.

## 5. Step-by-step implementation

1. Created `Git-Team-Project`, ran `git init`, renamed the branch to `main`, and configured repository-local identity from the existing global values.
2. Added `README.md` and created the initial commit, `Initial commit: create project repository`.
3. Added `BRANCHING.md` and committed the team workflow as `docs: define team branching strategy`.
4. Created and switched to `feature/login`. Added a labeled username/password form, a submit button, browser-required field validation, and a client-side demonstration message. Changed the README status line on this branch and committed as `feat: add login page`.
5. Improved the login page layout with responsive-friendly CSS and committed as `style: improve login page layout`.
6. Switched to `main`, changed the exact same README status line to a different project status, and committed as `docs: update project readiness status`.
7. Merged with `git merge --no-commit --no-ff feature/login`. Git reported a content conflict in `README.md`; the actual output and conflicted diff are included below.
8. Replaced the conflict block with a combined, accurate status, staged `README.md`, and completed the merge as `merge: integrate login feature and resolve README conflict`.
9. Ran the requested branch, status, and history commands, then checked the project files, login form elements, merge ancestry, conflict markers, whitespace, and clean worktree.

## 6. Important Git commands and explanations

The following Git operations were **executed** in the project directory (represented here as `$project`, resolved to `C:\Users\priya\OneDrive\Desktop\devops\Git-Team-Project`):

```text
git -C $project init
git -C $project branch -M main
git -C $project config --local user.name <existing-global-name>
git -C $project config --local user.email <existing-global-email>
git -C $project add README.md
git -C $project commit -m "Initial commit: create project repository"
git -C $project add BRANCHING.md
git -C $project commit -m "docs: define team branching strategy"
git -C $project switch -c feature/login
git -C $project add README.md login.html
git -C $project commit -m "feat: add login page"
git -C $project add login.html
git -C $project commit -m "style: improve login page layout"
git -C $project switch main
git -C $project add README.md
git -C $project commit -m "docs: update project readiness status"
git -C $project merge --no-commit --no-ff feature/login
git -C $project status --short
git -C $project diff -- README.md
git -C $project add README.md
git -C $project commit -m "merge: integrate login feature and resolve README conflict"
git -C $project branch
git -C $project status
git -C $project log --oneline
git -C $project log --oneline --graph --all --decorate
git -C $project diff --check
git -C $project merge-base --is-ancestor feature/login main
```

`git -C` runs each command against the assignment repository rather than the parent repository. `git init` creates the repository; `git branch -M` renames the initial branch; `git switch -c` creates and checks out a feature branch; `git add` stages selected changes; and `git commit` records them. `git merge --no-commit --no-ff` attempts a non-fast-forward merge but pauses before creating its commit, allowing the conflict to be inspected and fixed explicitly. `git log --oneline --graph --all --decorate` visualizes commits and branch pointers.

**Commands documented as team examples, not executed:** the branching guide shows `git pull` for updating from a remote and example `git status`, `git diff`, `git add`, and `git commit` commands for a future conflict workflow. No remote existed, so `git pull` was not run. The merge used actual `git status --short` and `git diff -- README.md` commands, and was completed manually; no push or automatic conflict resolution was used.

## 7. Merge conflict explanation and resolution

The feature and main branches edited the same README status line differently. Git confirmed an actual content conflict:

```text
Auto-merging README.md
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
Merge command exit code: 1 (1 is expected for this conflict)
--- Conflict status ---
UU README.md
A  login.html
```

The actual combined diff before resolution showed the competing branch changes and conflict markers:

```diff
@@@ -4,4 -4,4 +4,8 @@@
  
  Git-Team-Project is a small web project used to demonstrate team Git workflows, feature branches, meaningful commits, and merge-conflict resolution.
  
+<<<<<<< HEAD
 +Current status: Core project is ready for feature development.
+=======
 +Current status: Login feature is in development.
+>>>>>>> feature/login
```

I manually replaced the entire conflict block with:

```text
Current status: The login feature is merged and the project is ready for continued development.
```

Then I staged `README.md` and created the merge commit. A final check found no `<<<<<<<`, `=======`, or `>>>>>>>` conflict markers. This was a real merge conflict produced by Git, not a simulated example.

## 8. Sample Git history

The following is the **actual** output captured after the feature merge and before this report's follow-up commit:

```text
*   4a60751 (HEAD -> main) merge: integrate login feature and resolve README conflict
|\  
| * 2599585 (feature/login) style: improve login page layout
| * e25b048 feat: add login page
* | d756ee1 docs: update project readiness status
|/  
* f4914f4 docs: define team branching strategy
* b6c81c4 Initial commit: create project repository
```

The feature-branch history was also verified:

```text
2599585 style: improve login page layout
e25b048 feat: add login page
f4914f4 docs: define team branching strategy
b6c81c4 Initial commit: create project repository
```

## 9. Final result

The completed project contains:

```text
Git-Team-Project/
├── README.md
├── BRANCHING.md
├── GIT_ASSIGNMENT_REPORT.md
├── index.html
├── styles.css
├── login.html
├── signup.html
├── dashboard.html
└── profile.html
```

Four-developer feature implementation completed after the original Git demonstration:

| Developer | Branch | Feature commit | Delivered work |
|---|---|---|---|
| Developer 1 (`shrushtib08`) | `feature/login` | `7f6c74b` | Integrated login page with shared styling and portal navigation; clearly labels authentication as a demo. |
| Developer 2 (`tauqeer971`) | `feature/signup` | `4171fa5` | Added a registration form with required fields, email validation, matching-password validation, and no credential storage. |
| Developer 3 (`Rakshitham15`) | `feature/dashboard` | `ce05fb7` | Added sample sports activities, summary counts, and a working sport filter. |
| Developer 4 (`PriyaHadapad15`) | `feature/profile` | `968c1c2` | Added editable profile preview with browser-local save and clear actions. |

Each feature branch was merged into `main` with a non-fast-forward merge commit. The branch names remain available locally. These are contributions implemented in one local environment under its configured Git identity, not independently authenticated commits by the listed GitHub accounts.

The final integration commands executed were:

```text
git switch main
git merge --no-ff feature/login -m "merge: integrate login portal feature"
git merge --no-ff feature/signup -m "merge: integrate team registration feature"
git merge --no-ff feature/dashboard -m "merge: integrate team activity dashboard"
git merge --no-ff feature/profile -m "merge: integrate member profile feature"
```

Final integration commit graph (actual output before this report's follow-up documentation update):

```text
*   39b99eb (HEAD -> main) merge: integrate member profile feature
|\  
| * 968c1c2 (feature/profile) feat: add editable member profile
* |   7f5672e merge: integrate team activity dashboard
|\ \  
| * | ce05fb7 (feature/dashboard) feat: add filtered team activity dashboard
| |/  
* |   4a80c8c merge: integrate team registration feature
|\ \  
| * | 4171fa5 (feature/signup) feat: add validated team registration form
| |/  
*   bac7c69 merge: integrate login portal feature
|\  
| * 7f6c74b (feature/login) feat: integrate login with sports portal
|/  
* eabbb8e feat: add sports portal home and shared styles
```

The signup and login forms demonstrate client-side validation only. The dashboard uses static sample data. The profile stores non-password demo details in browser local storage. The project does not include backend services, real accounts, authentication, or a live team calendar.

The completed pages were also exercised in the integrated browser: the dashboard initially showed five activities and filtered to two running activities; the signup form rejected mismatched passwords and accepted matching values; the profile saved values across a page reload and cleared them when requested; and the login form displayed its demo-only response. Test profile data was cleared after the check.

Verification results:

- The nested repository is initialized and `main` exists.
- `feature/login` exists and is merged into `main`; the login branch is an ancestor of `main`.
- All four developer feature branches are documented.
- The feature has two focused commits: `feat: add login page` and `style: improve login page layout`.
- Git produced and displayed a real README content conflict, which was manually resolved.
- No conflict markers remain; `git diff --check` passes and the worktree was clean after the merge.
- The login HTML contains username and password fields, a submit button, required-field validation, and a demo submission handler. Authentication is not connected to a backend.

No separate automated test suite or authentication service was present. The final focused checks verified the form structure and submit handler along with repository state; they are not represented as a pre-merge automated test run.

## 10. Conclusion

The assignment demonstrates repository initialization, local identity configuration, a documented team branching strategy, focused feature commits, an actual Git-generated merge conflict, manual conflict resolution, and a readable commit graph. The repository was kept local, and the parent workspace repository and global Git settings were not changed.
