# cRUSTy: Python-to-Rust Learning Path

This repository provides an iterative set of checkpoints to help a Python programmer learn Rust by building and extending small projects. The curriculum is organized into tiers so you can progress from fundamentals to real-world tooling.

## How to use this repo
1. **Install Rust**: Follow the official installer at <https://www.rust-lang.org/tools/install> (rustup). Verify with `rustc --version`.
2. **Create a workspace**: Run `cargo new --bin hello_rust` (or `cargo new --lib rust_playground`) inside this repository to start coding each checkpoint. Use a new Cargo package for each tier or keep adding modules to one crate—whatever keeps your experiments tidy.
3. **Test continuously**: Use `cargo test` after each checkpoint. Rust’s compiler errors are part of the learning process—read them closely.
4. **Compare with Python**: For each exercise, jot down a short note on how the Rust solution differs from your Python intuition (ownership, types, pattern matching, error handling, etc.).

## Checkpoint roadmap
Each checkpoint is designed to be a small commit-sized milestone. Try to finish one per session.

### Tier 0: Rust basics
- Print "Hello, Rust" and run it with `cargo run`.
- Parse command-line arguments with `std::env::args`.
- Write a function that sums a vector of integers and returns `Result<i32, String>`; handle empty input as an error using `?` and `Option::ok_or`.

### Tier 1: Ownership and borrowing
- Re-implement the classic word-count (`wc`) tool: read stdin, count lines/words/chars. Focus on borrowing slices instead of cloning strings.
- Build a mini REPL that echoes input until `:quit`. Practice mutable vs. immutable bindings and `match` expressions.
- Write unit tests for each helper function (e.g., `count_words`, `count_lines`).

### Tier 2: Data structures and enums
- Implement a simple todo list CLI that stores items in memory using `Vec<TodoItem>`, where `TodoItem` is an enum with states (e.g., `Pending`, `Done`).
- Serialize/deserialize the todo list to JSON using `serde` and `serde_json`; note how derives work.
- Add command parsing with `clap` for commands like `add`, `list`, and `complete`.

### Tier 3: Error handling and traits
- Introduce a custom error type using `thiserror` and convert lower-level errors with `From`.
- Define a trait (`Storage`) with implementations for in-memory and file-backed todo lists. Practice trait objects vs. generics.
- Add integration tests to ensure both storage backends behave the same.

### Tier 4: Concurrency and async
- Build a tiny web server with `axum` that exposes your todo API. Practice `tokio` async patterns, `Arc`, and `Mutex` where needed.
- Stream server-sent events (SSE) to broadcast todo updates. Compare to Python async with `asyncio`.
- Add a `client` binary that consumes the API with `reqwest` and displays results.

### Tier 5: Performance and tooling
- Benchmark critical functions with `cargo bench` and the `criterion` crate; compare allocations via `cargo +nightly bench -- -Z unstable-options --profile-time=5` if available.
- Set up linting with `cargo clippy` and formatting with `cargo fmt` (consider adding a `Makefile` target that runs `fmt`, `clippy`, and `test`).
- Inspect generated assembly with `cargo asm` or `cargo llvm-ir` (optional but great for optimization insight).

### Stretch goals and comparisons
- Recreate a small Python script you use daily in Rust—note ergonomics, speed, and safety differences.
- Package your binary with `cargo install --path .` and share it. Reflect on deployment differences between Python packaging and Rust crates.
- Experiment with `pyo3` to build a Python extension in Rust, bridging both ecosystems.

## Tips for a smooth transition from Python
- **Types first**: Embrace explicit types and lifetimes as communication tools, not obstacles.
- **Borrowing vs. ownership**: Prefer references (`&T`) over owned types (`T`) until you truly need ownership. Avoid `clone()` until you know why you need it.
- **Error handling mindset**: Replace exceptions with `Result` and exhaustive `match`. Use `?` to bubble up errors cleanly.
- **Testing habit**: Rust unit tests live alongside the code in the same module. Use them as guardrails while you experiment.

Happy hacking—commit early and keep comparing your Rust solutions to the Python versions you already know!
