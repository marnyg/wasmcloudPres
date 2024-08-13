## Kubernetes Security Model

- **Network Policies**: Define how pods communicate with each other and other network endpoints.
- **RBAC (Role-Based Access Control)**: Regulate access to Kubernetes API resources.
- **Pod Security Policies**: Control security-sensitive aspects of pod specification.
- **Secrets Management**: Handle sensitive information, though often requires additional tools for encryption at rest.
- **Service Accounts**: Provide identities for processes running in pods.

## wasmCloud Security Model

- **Capability-based Security**: Components only get access to capabilities they explicitly declare and are granted.
- **Component Model**: Components are isolated and can only communicate through well-defined type safe interfaces.
- **Signed Modules**: All components (actors and capability providers) must be cryptographically signed. 
- **Encrypted communication**: Communication between components go via Nats, so if Nats has set up TLS, so will the rest of the cluster
- **Claims-based Identity**: Each module has a unique, cryptographically verifiable identity.
- **Least Privilege by Default**: Components start with zero privileges, gaining only what they need.

## Key Differences

1. **Granularity**: wasmCloud's capability-based model offers finer-grained control than Kubernetes' primarily network-based approach.
2. **Simplicity**: wasmCloud's model is often simpler to reason about and configure compared to Kubernetes' multiple layers of security controls.
3. **Default Stance**: wasmCloud starts from zero trust, while Kubernetes often requires explicit restrictions.
4. **Scope**: Kubernetes focuses on cluster-level security, while wasmCloud's model extends to the application level.
5. **Portability**: wasmCloud's security model remains consistent across different environments, while Kubernetes may require environment-specific configurations.