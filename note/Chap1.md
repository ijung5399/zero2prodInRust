# Faster Linking
```
cargo install -f cargo-binutils
rustup component add llvm-tools-preview
```
In `~\.cargo\config.toml
```
[target.x86_64-pc-windows-msvc]
rustflags = ["-C", "link-arg=-fuse-ld=lld"]

[target.x86_64-pc-windows-gnu]
rustflags = ["-C", "link-arg=-fuse-ld=lld"]
```

But my computer complaint about this options. This means msvc doesn't know this rustflag. So, I switched it to gnu by:

for checking:
```
rustup show active-toolchain
```


for switching to gnu:
```
rustup install stable-x86_64-pc-windows-gnu
rustup default stable-x86_64-pc-windows-gnu
```


# cargo-watch
```
cargo watch -x check -x test -x run
```

# code coverage
```
cargo install cargo-llvm-cov
cargo llvm-cov
```

# Linting
```
rustup component add clippy
cargo clippy
cargo clippy -- -D warnings
```

# Format
`rustfmt`
```
rustup component add rustfmt
cargo fmt
cargo fmt -- --check
```

# Security Vulnerability
```
cargo install cargo-audit
cargo audit
```
NOTE: I got continuous failure while installing this.
So, reverted my tool-chain to msvc:
```
rustup default stable-x86_64-pc-windows-msvc
```
Now, I got audit working:
```
❯ cargo audit
    Fetching advisory database from `https://github.com/RustSec/advisory-db.git`
      Loaded 792 security advisories (from C:\Users\ilmojung\.cargo\advisory-db)
    Updating crates.io index
    Scanning Cargo.lock for vulnerabilities (1 crate dependencies)
```
Also, `cargo watch` works smoothly:
```
❯ cargo watch -x fmt -x check -x test -x run
[Running 'cargo fmt && cargo check && cargo test && cargo run']
    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.02s
    Finished `test` profile [unoptimized + debuginfo] target(s) in 0.02s
     Running unittests src\main.rs (target\debug\deps\zero2prodInRust-3a28f4833b4b195f.exe)

running 0 tests

test result: ok. 0 passed; 0 failed; 0 ignored; 0 measured; 0 filtered out; finished in 0.00s

    Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.03s
     Running `target\debug\zero2prodInRust.exe`
Hello, Ilmo world!!
[Finished running. Exit status: 0]
```
