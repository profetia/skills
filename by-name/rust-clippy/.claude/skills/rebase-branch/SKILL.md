---
name: rebase-branch
description: Instructions to rebase a branch in the Rust Clippy repository to the latest version of the `master` branch.
allowed-tools:
  - Bash(git fetch *)
  - Bash(git checkout *)
  - Bash(git rebase *)
---

Follow these steps to rebase a branch in the Rust Clippy repository to the latest version of the `master` branch:
1. Ensure that you have the latest version of the `master` branch from the `upstream` remote.
2. Switch to the branch that you want to rebase.
3. Rebase the branch onto the latest version of the `master` branch.
4. If there are any conflicts during the rebase, resolve them by editing the conflicting files. Use git to inspect what has been changed in the current branch and in the incoming branch. Try to resolve the conflicts after you understand the intent of the incoming changes and the intent of the current changes.
5. Make sure that all tests pass after resolving the conflicts and the codebase is formatted correctly. Note that if the branch implements a new lint, enhances an existing lint, or fixes a false negative, it is fine if the dogfood test fails, as long as there exists a subsequent commit to apply the relevant fix to Clippy itself.
6. After resolving all conflicts and ensuring that all tests pass, add the changes to the branch and continue the rebase process until all commits have been successfully applied.
