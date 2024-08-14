External first-party providers :

- [http-client](https://github.com/wasmCloud/wasmCloud/tree/main/crates/provider-http-client)
- [http-server](https://github.com/wasmCloud/wasmCloud/tree/main/crates/provider-http-server)
- [keyvalue-redis](https://github.com/wasmCloud/wasmCloud/tree/main/crates/provider-keyvalue-redis)
- [keyvalue-vault](https://github.com/wasmCloud/wasmCloud/tree/main/crates/provider-keyvalue-vault)
- [blobstore-fs](https://github.com/wasmCloud/wasmCloud/tree/main/crates/provider-blobstore-fs)
- [blobstore-s3](https://github.com/wasmCloud/wasmCloud/tree/main/crates/provider-blobstore-s3)
- [messaging-kafka](https://github.com/wasmCloud/wasmCloud/tree/main/crates/provider-messaging-kafka)
- [messaging-nats](https://github.com/wasmCloud/wasmCloud/tree/main/crates/provider-messaging-nats)
- [sqldb-postgres](https://github.com/wasmCloud/wasmCloud/tree/main/crates/provider-sqldb-postgres)

In [Wadm manifests](https://wasmcloud.com/docs/ecosystem/wadm/), you can refer to the [wasmCloud GitHub Packages registry](https://github.com/orgs/wasmCloud/packages?repo_name=wasmCloud) for OCI images of providers—for example: `ghcr.io/wasmcloud/keyvalue-redis:0.27.0`

### Built-in providers

Because built-in providers are part of the wasmCloud host itself, they do not communicate over NATS and run in the same process as the host. Updating a built-in provider requires updating the host. Built-in providers include:

- Logging (using the [`wasi-logging`](https://github.com/WebAssembly/wasi-logging) interface)
- Random (using the [`wasi-random`](https://github.com/WebAssembly/wasi-random) interface)
- Clocks (using the [`wasi-clocks`](https://github.com/WebAssembly/wasi-clocks) interface)