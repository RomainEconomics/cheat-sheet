

# Cargo


## Examples

### Main Cargo Commands

```bash
cargo new my_project
cargo build
cargo run
cargo test
```

### Build and Run Release

```bash
cargo build --release
./target/release/my_project
```

### Running multiple binaries

```bash
cargo run --bin my_binary
```

### Running a specific test

```bash
cargo test test_name
```

### Running a specific test module

```bash
cargo test module_name
```

### Cargo Watch

```bash
cargo install cargo-watch
cargo watch -x run  # Run the project
cargo watch -x test # Run tests
```