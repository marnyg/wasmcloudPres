#TODO
## Example Folder structure
``` 
/
├── build
│  ├── A.wasm
│  └── B.wasm
├── componentA
│  ├── src/
│  ├── wit/
│  ├── wadm.yaml
│  └── wasmcloud.toml
└── componentB
   ├── src/
   ├── wit/
   ├── wadm.yaml
   └── wasmcloud.toml
```

## Example WADM.yaml
[[Example of linking]]
## Example wasmcloud.toml
```toml
name = "http-hello-world"
language = "tinygo"
type = "component"
version = "0.1.0"

[component]
wit_world = "hello"
wasm_target = "wasm32-wasi-preview2"
destination = "build/http_hello_world_s.wasm"
```
## Example Code
[[Example components]]