#slide

### Core infra concepts
- Host Runtime: Manages components and providers
	- Wasmtime
	- Manages "Job" allocation
	- Open policy agent
	- Open telemetry
	- [[Host Machine diagram]]
- Lattice: Distributed application network
	- Uses Nats
	- Self-forming, self-healing mesh network that provides a unified, flat topology across environments using NATS
	- [[Lattice Diagram]]
- **Providers** are executable host plugins that implement longer-lived processes, typically providing reusable [capabilities](https://wasmcloud.com/docs/concepts/capabilities) (such as key-value storage).