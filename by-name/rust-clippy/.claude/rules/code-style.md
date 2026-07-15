---
paths:
  - "clippy_lints/**/*.rs"
  - "clippy_lints_internal/**/*.rs"
  - "clippy_utils/**/*.rs"
---

- Try not use `unwrap()` or similar methods in the codebase. Instead, use `?` to propagate errors or handle them gracefully.