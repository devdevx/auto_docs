# Rust

## Commands

Install toolchain

````
rustup install stable-x86_64-pc-windows-gnu
rustup install stable-x86_64-pc-windows-msvc

rustup default stable-x86_64-pc-windows-msvc
````

Update toolchain

````
rustup update
````

List toolchains

````
rustup toolchain list
````

Install cargo watch

````
cargo install cargo-watch
````

Install cargo edit

````
cargo install cargo-edit
cargo install cargo-edit --features vendored-openssl
````

Cargo edit commands

````
cargo add x
cargo add x --features f1 f2
cargo rm x
cargo upgrade
cargo upgrade x

cargo set-version 1.0.0
cargo set-version --bump major
cargo set-version --bump minor
cargo set-version --bump patch
````

Create new project

````
cargo new hello_world --bin
cargo new hello_world --lib
````

Watch project

````
cargo watch -x 'run'
cargo watch -x 'run' --why
````

## Libraries to explore

Tokio, Hyper/Reqwest, Ring, and Neon

warp

tokio-tungstenite

https://crates.io/crates/anyhow

https://crates.io/crates/wasm-bindgen

https://crates.io/crates/femme

## Learn

https://github.com/pingcap/talent-plan/tree/master/courses/rust

https://github.com/rust-lang/rustlings

https://docs.microsoft.com/en-us/learn/paths/rust-first-steps/?WT.mc_id=javascript-00000-wachegha

https://betterprogramming.pub/structuring-rust-project-for-testability-18207b5d0243

`uninplemented!()`

https://www.youtube.com/c/RustVideos/videos

https://www.youtube.com/watch?v=gesNaLkUJeA

## Documentation

[The Rust Programming Language](https://doc.rust-lang.org/stable/book/title-page.html)

[The Rustonomicon](https://doc.rust-lang.org/stable/nomicon/intro.html)

## IDEs

### Visual Studio Code

