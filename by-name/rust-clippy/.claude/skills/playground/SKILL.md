---
name: playground
description: Instructions to play with Rust Clippy in a local environment.
allowed-tools:
  - Bash(cargo dev lint *)
  - Bash(rustc +nightly -Z unpretty=mir *)
  - Bash(rustc +nightly -Z unpretty=hir *)
---

- An isolated crate is created to test the Clippy lints in `~/repository/rust-playground`.
- Write the test code in `src/lib.rs` or `src/main.rs`.
- Run `cargo dev lint ~/repository/rust-playground/` to see the output of Clippy.
- Run `rustc +nightly -Z unpretty=mir ~/repository/rust-playground/src/main.rs  --edition 2024` to see the test code in MIR format.
- Run `rustc +nightly -Z unpretty=hir ~/repository/rust-playground/src/main.rs  --edition 2024` to see the test code in HIR format.
- When working on an issue, you can use the playground to reproduce the issue and test the fix. Then you can add the test code to the tests in the Clippy repository.
- After you have finished testing, you can use `git reset --hard` to reset the repository to the last commit and remove all changes made during testing.
