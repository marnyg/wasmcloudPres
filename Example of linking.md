Example static linking (in Rust):
```rust
#[link(wasm_import_module = "wasmcloud:httpserver")]
extern "C" {
    fn handle_http(req: *const HttpRequest) -> *mut HttpResponse;
}
```

Example dynamic linking (in wadm.yaml):
```yaml
apiVersion: core.oam.dev/v1beta1
kind: Application
metadata:
  name: my-app
spec:
  components:
    - name: my-component
      type: wasmcloud-component
      properties:
        image: myregistry.com/my-component:v1
      traits:
        - type: link
          properties:
            target: http-component
            namespace: wasi
            package: http
            interfaces: [incoming-handler]
            source_config:
              - name: default-http
                properties:
                  ADDRESS: 127.0.0.1:8080
```
