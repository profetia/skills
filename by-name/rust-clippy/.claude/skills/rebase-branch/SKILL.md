---
name: rebase-branch
description: Instructions to rebase a branch in the Rust Clippy repository to the latest version of the `master` branch.
allowed-tools:
  - Bash(git fetch *)
  - Bash(git checkout *)
  - Bash(git rebase *)
  - Bash(git add *)
  - Bash(git rm *)
  - Bash(git diff *)
  - Bash(git show *)
  - Bash(git log *)
  - Bash(git status)
  - Bash(git commit *)
  - Bash(cargo check *)
  - Bash(cargo test *)
  - Bash(cargo uibless *)
  - Bash(grep *)
---

Follow these steps to rebase a branch in the Rust Clippy repository to the latest version of the `master` branch:
1. Ensure that you have the latest version of the `master` branch from the `upstream` remote.
2. Switch to the branch that you want to rebase.
3. Rebase the branch onto the latest version of the `master` branch.
4. When a conflict occurs during the rebase, for **each** conflicting commit:
   a. Resolve the conflicts by editing the conflicting files. Use `git show <commit>` to inspect what the incoming commit changes, and `git show upstream/master:<path>` to inspect the current upstream version. Try to resolve the conflicts after you understand the intent of both sides.
   b. Run `cargo check -p clippy_lints` to verify the resolution compiles.
   c. Run `cargo uibless -- <test_name>` (e.g., `cargo uibless -- manual_filter`) to update `.stderr` and `.fixed` test files with the correct line numbers and suggestions, and to verify the lint's behaviour is correct. Alternatively, to run tests without updating snapshot files, use `cargo test -- <test_name>`.
   d. **Only after tests pass**, run `git add <resolved_files>` and then `git rebase --continue`.
5. Note that if the branch implements a new lint, enhances an existing lint, or fixes a false negative, it is fine if the dogfood test fails, as long as there exists a subsequent commit to apply the relevant fix to Clippy itself.
6. After the rebase completes successfully, run `cargo test -- <test_names>` to do a final verification of the relevant tests, including the dogfood test.
