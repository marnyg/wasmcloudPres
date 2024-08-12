#slide

### explanation
[[From infra or devops perspective]]
[[From deveoper perspective]]
### examples
[[Comparisons to things you already know]]
Concrete Code examples 

###  Why care
- [ ] refactor into own slides 
[[separation of business logic from runtime logic]]
* components can *Only*  know about the interface of their providers, not their implimentaiton
	*  ie kv-store could be a redis or nats or consul. but the code can not know
	*  [[Example providers]]
	*  [[example components]]
* no networking/databases/secret-provider etc in component code
* components can be MUCH smaller than Docker container often are
* components can be swapped out with other programing languages at a later time
[[better networking]]
- If your team struggles with microservice communication, emphasize the networking simplifications.
* service discovery by default
* no ip or dns
[[easyer scaling]]
- If maintaining and scaling your current infrastructure is challenging, focus on the built-in scaling benefits.
* load balancing automatically
* components must be stateless and single threaded
* Location-independent scaling
[[modern features by default]]
- If improving security and observability are priorities, highlight the OPA and OpenTelemetry integrations.
[[better local dev(maybe)]]
* no networking crap
	* bridge network, multiple levels of netorking viritualization(win->wsl->docker)
* no OS virtualization 
	* no virtual filesytem, no virtual network stack, volume mounts, etc
	* just one binary per component
* might be posibilites for future build tools improvment(personal speculation)

### Why Not care
* its verry imature
* few providers available
* not good Highly parallel workloads with intensive inter-process communication due to  single-threaded nature, where scaling is done with new instances. This would make communication the bottleneck
   For example, complex scientific simulations or large-scale data processing pipelines that require frequent synchronization between parallel branches might face performance bottlenecks.
* missing stuff like
	* ceritficate managment
	* automated rollouts/rollback and no argocd
	* generaly sparse ecosystem

	