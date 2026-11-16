# Branching Strategy

## Team workflow

`main` is the stable branch and contains reviewed, tested project code. Every feature starts from the latest `main` and is developed on its own branch. Developers keep changes focused, run the relevant checks before asking for review, and merge only after review and successful testing. This assignment demonstrates a direct merge locally; a shared team should use a pull request for review.

Before starting work, update `main`, then create and switch to the assigned feature branch:

```text
git switch main
git pull
git switch -c feature/<name>
```

Commit incremental, tested changes with descriptive messages. Before integration, sync the feature branch with `main` as appropriate for the team, resolve any conflicts on the feature branch or during merge, run the checks again, and merge the reviewed branch into `main`. Delete a feature branch after integration only when it is no longer needed.

## Developers and responsibilities

| Developer | Responsibility | Branch |
|---|---|---|
| Developer 1 | Login functionality | `feature/login` |
| Developer 2 | Registration functionality | `feature/signup` |
| Developer 3 | Dashboard functionality | `feature/dashboard` |
| Developer 4 | Profile functionality | `feature/profile` |

Each developer owns the implementation and tests for their assigned feature, coordinates shared-file changes with the team, and requests review before merging.

## Branch naming conventions

- Stable integration branch: `main`
- Feature branches: `feature/<short-description>` (for example, `feature/login`)
- Use lowercase words separated by hyphens when a description needs multiple words.
- Create feature branches from the current `main`; do not commit feature work directly to `main`.

## Commit message conventions

Use a short imperative description, optionally prefixed with a conventional type:

- `feat: add login page` for a user-facing capability
- `style: improve login page layout` for presentation-only changes
- `test: add login form checks` for tests
- `docs: document branching strategy` for documentation
- `fix: validate required login fields` for a bug fix

Keep commits focused and ensure each message describes the change. Avoid vague messages such as `update` or `changes`.

## Merge and conflict resolution

1. Confirm the feature is tested and request review (a pull request is recommended for team work).
2. Ensure the target branch is `main` and its worktree is clean. Merge the reviewed feature branch.
3. If Git reports a conflict, inspect the affected files and the conflict markers. Compare both branch versions and discuss intended behavior with the relevant owners.
4. Edit each conflicted file to retain the correct combined result, remove all `<<<<<<<`, `=======`, and `>>>>>>>` markers, and run tests or review the result.
5. Stage the resolved file(s) and complete the merge with a descriptive merge commit. Verify the commit graph and clean working tree.

Example commands for resolving a real merge conflict:

```text
git status
git diff -- README.md
# Edit README.md and remove the conflict markers.
git add README.md
git commit -m "merge: resolve README conflict and integrate feature"
git log --oneline --graph --all --decorate
```
