#slide
# wasmCloud Core Developer Concepts

## Providers
- Executable host plugins implementing longer-lived processes
- Provide reusable capabilities (e.g., key-value storage, messaging)
- Example: Redis capability provider
- Example: Postgres capability provider
## Components
- Portable, interoperable WebAssembly binaries implementing stateless logic
- Sandboxed execution in wasmtime runtime for enhanced security
- Example: A component transforming data from database
## Interfaces
- Contracts defining relationships between components and providers
- Use WebAssembly Interface Type (WIT) syntax
- Vendor-agnostic, high-level definitions of functionalities
- [[Example WIT interface]]
## Linking
- Connects a component's requirements (imports) to another entity's exposed functions (exports)
- Can be done at build time (static) or runtime (dynamic)
- Configured via wadm.yaml (analogous to Kubernetes Deployment)
- [[Example of linking]]

## Key points:
- WIT provides language-agnostic interface definitions
- wasmtime ensures secure, sandboxed execution of components
- Linking allows flexible composition of applications
- wadm.yaml enables declarative application configuration