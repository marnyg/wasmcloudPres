#TODO

## Consuming seecrets
Components access secrets using the [`wasmcloud:secrets`](https://github.com/wasmCloud/wasmCloud/blob/main/crates/runtime/wit/deps/secret/secrets.wit) WIT interface. Support is built into the wasmCloud host to fetch secrets from a secrets backend and provide them to components at runtime.

Ensure you have the `wasmcloud:secrets` interface in your component's WIT world:

### wit

```wit
package wasmcloud:example;

world component {
  import wasmcloud:secrets/store@0.1.0-draft;
  import wasmcloud:secrets/reveal@0.1.0-draft;
}
```

### rust component

```rust
fn is_allowed(provided_password: String) -> bool {
    // Resource secret, not actually loaded
    let password = wasmcloud::secrets::store::get("api_password").expect("failed to get password");

    // Revealed secret
    match wasmcloud::secrets::reveal::reveal(&password) {
        wasmcloud::secrets::store::SecretValue::String(s) => s == provided_password,
        wasmcloud::secrets::store::SecretValue::Bytes(b) => String::from_utf8_lossy(&b) == provided_password,
    }
}
```


## injecting secret

```yaml 
apiVersion: core.oam.dev/v1beta1
kind: Application
metadata:
  name: App with secrets
  annotations:
    version: v0.0.1
    description: 'HTTP hello world demo in Rust'
spec:
  components:
    - name: http-component
      type: component
      properties:
        image: ghcr.io/wasmcloud/components/http-hello-world-rust:0.1.0
        secrets:
          - name: test
            properties:
              backend: vault
              key: 'path/to/key'
      traits:
        # Govern the spread/scheduling of the component
        - type: spreadscaler
          properties:
            replicas: 1
        - type: link
          properties:
            target: httpclient
            namespace: wasi
            package: http
            interfaces: [outgoing-handler]
        - type: link
          properties:
            namespace: wasmcloud
            package: postgres
            interfaces: [managed-query]
            target:
              name: sql-postgres
              secrets:
                - name: db-password
                  properties:
                    backend: vault
                    key: secrets/myapp/db-password
                    version: 1
              config:
                - name: foo
                  properties:
                    value: whatever

    # Add a capability provider that enables HTTP access
    - name: httpserver
      type: capability
      properties:
        image: ghcr.io/wasmcloud/http-server:0.20.0
      traits:
        # Link the httpserver to the component, and configure the HTTP server
        # to listen on port 8080 for incoming requests
        - type: link
          properties:
            namespace: wasi
            package: http
            interfaces: [incoming-handler]
            target:
              name: http-component
              secrets: ...
            source:
              config:
                - name: default-http
                  properties:
                    address: 127.0.0.1:8080
              secrets:

    - name: httpclient
      type: capability
      properties:
        image: ghcr.io/wasmcloud/http-client:0.9.0

    - name: sqldb-postgres
      type: capability
      properties:
        image: ghcr.io/wasmcloud/provider-sqldb-postgres:0.1.0

...

```