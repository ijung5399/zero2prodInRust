
# HttpServer
- Transport layer
- Connection
  - Max concurrent connection#
  - TLS
  - etc

# App
After connection, App comes in.
- routing
- middleware
- req handling

# About `macro`
- the main purpose of `Rust macro` is `code generation`.
- Rust macros operate at the `token` level.
- How do we debug or inspect what is happening with a particular macro? 

>[INFO] You inspect the tokens it outputs!
=> `cargo expand` all macros in your code without passing the output to the compiler, allowing you to step through it and understand waht is going on.

```
cargo install cargo-expand
cargo expand
```

- `cargo-expand` relies on the `nightly` compiler to expand our macros.

```
rustup toolchain install nightly --allow-downgrade
```
- now, `cargo expand` will find and use `nightly` automatically.
