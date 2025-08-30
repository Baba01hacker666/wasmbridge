# multi-wasm-web

Project layout:

multi-wasm-web/
├── go-server/
│   ├── main.go
│   └── static/           # index.html, pkg/ (wasm JS + wasm), wasm_glue.js
├── rust-wasm/
│   ├── Cargo.toml
│   └── src/
│       └── lib.rs
└── README.md

Quick start:

1. Build Rust -> wasm (recommended with wasm-pack):
   - Install wasm-pack: https://rustwasm.github.io/wasm-pack/installer/
   - From project root:
     cd rust-wasm
     wasm-pack build --target web --out-dir ../go-server/static/pkg --out-name package_name

   This will place `package_name.js` and `package_name_bg.wasm` into `go-server/static/pkg`.

   Alternative (manual):
   - rustup target add wasm32-unknown-unknown
   - cargo build --release --target wasm32-unknown-unknown
   - run wasm-bindgen on the produced .wasm file to generate JS glue and wasm.

2. Run the Go static server:
   cd go-server
   go run main.go

3. Open http://localhost:8080

Notes:
- index.html expects the wasm package files at static/pkg/package_name.js and package_name_bg.wasm
- Adjust build/out-name if you use a different package name.
