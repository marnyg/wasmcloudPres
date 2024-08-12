#slide
#TODO
- [ ] add examples of interfaces WIT
- [ ] add examples of linking (both static and dynamic)
### Core Developer concepts
- **Components** are portable, interoperable WebAssembly binaries that implement stateless logic.
- **Providers** are executable host plugins that implement longer-lived processes, typically providing reusable [capabilities](https://wasmcloud.com/docs/concepts/capabilities) (such as key-value storage).
- **Interfaces** are contracts that define the relationships between entities like components and providers, often defining functionalities like HTTP or key-value storage at a high and vendor-agnostic level.

- **Linking** is the connection of a component's requirements (or "imports") to the exposed function (or "export") of another entity.

![[Pasted image 20240812122033.png]]
