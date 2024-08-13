
You can think of these as the same thing:
* A API is just a library called over the network
### Similarities:
- Encapsulate application code
- Aim for modularity and reusability
### Differences:
- Dependencies: Containers include OS-level dependencies, wasmCloud components are pure WebAssembly, traditional libraries depend on language runtime
- State Management: wasmCloud components are inherently stateless, containers can be stateful
- Size and Startup: wasmCloud components are typically smaller and start faster than containers
- Capability Boundaries: wasmCloud components have stricter, capability-based boundaries