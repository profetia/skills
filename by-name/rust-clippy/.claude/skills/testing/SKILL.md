---
name: testing
description: Conventions and instructions for running tests and writing test cases in Rust Clippy.
allowed-tools:
  - Bash(cargo test *)
  - Bash(cargo uitest *)
  - Bash(cargo bless *)
  - Bash(cargo uibless *)
---

# File Organization

The tests for Clippy are organized in the `tests` directory with the following structure:

- `tests/ui`: Contains UI tests that check the output of Clippy lints. Each `.rs` file in this directory corresponds to a specific lint with the same name as the lint. The expected output is stored in a `.stderr` file with the same name as the test file, as well as a `.fixed` file if the lint has a fix suggestion.
- `tests/ui-cargo`: Contains UI tests that also require a `Cargo.toml` file to configure the test crate. Everything else is the same as `tests/ui`.
- `tests/ui-toml`: Contains UI tests that require a `clippy.toml` file to configure the lints. Everything else is the same as `tests/ui`.
- `ui-internal`: Contains UI tests for internal lints that are not exposed to the public. Everything else is the same as `tests/ui`.
- Everything else in the `tests` directory are testing utilities or additional test cases that are not directly related to a specific lint.

# Testing Instructions

- Use `cargo test` to run all tests. This will run all tests in the `tests` directory, including UI tests and other test cases.
- Use `cargo uitest` to run only the UI tests. This will run all tests in the `tests/ui`, `tests/ui-cargo`, and `tests/ui-toml` directories. Use the "TESTNAME" environment variable to run a specific lint, e.g. `TESTNAME=lint_name cargo uitest`.
- Use `cargo test --test dogfood` to run the dogfood test, which checks that Clippy can lint itself without any errors.
- Use `cargo bless` to update the expected output of the UI tests. This will overwrite the `.stderr` and `.fixed` files with the current output of Clippy. Use this command when you have made changes to a lint and want to update the expected output.
- Use `cargo uibless` to update the expected output of the UI tests. Similarly you can use the `TESTNAME` environment variable to update a specific lint, e.g. `TESTNAME=lint_name cargo uibless`.

# Writing Tests

- Use `@no-rustfix` in the comment at the top of the test file to indicate that the lint does not have a fix suggestion. This will prevent Clippy from generating a `.fixed` file for the test. 
- Use `@check-pass` in the comment at the top of the test file to indicate that the test should pass without any warnings or errors. This is useful for testing that a lint does not trigger on certain code patterns.
- When a lint sometimes give fix suggestions and sometimes does not, put the ones with fix suggestions in a separate test file named with the suffix `_fixable.rs` or put the ones without fix suggestions in a separate test file named with the suffix `_unfixable.rs`.
- Use `#![expect(clippy::lint_name)]` in the comment at the top of the test file if other lints are expected to trigger in the test. 
- Use `//~^ lint_name` in the comment after the test code to indicate that the lint is expected to trigger on that line. The number of `\``s indicates the number of lines the lint is expected to trigger on. For example, `//~^ lint_name` indicates that the lint is expected to trigger on the line right above the comment, while `//~^^ lint_name` indicates that the lint is expected to trigger on the two lines above the comment. Use `//~| lint_name` to indicate that the lint is expected to trigger on multiple lines, but not necessarily consecutively. Use `//~^ ERROR: message` to indicate that the lint is expected to trigger with a specific error message.
- When the test code comes from an issue, use `fn issue1234()` or `mod issue1234{}` to indicate that the test is related to issue #1234.
