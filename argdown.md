```argdown 
===
title: >
  A first example (with arguments from 'The Debaters Handbook')
subTitle: Some Pros and Cons Reconstructed in Detail
author: Gregor Betz
date: 24/10/2018
model:
    removeTagsFromText: true
vizJs:
    engine: dot
dot:
    graphVizSettings:
        rankdir: RL #RL,LR,TB,BT
        concentrate: true
        ranksep: 0.8
        nodesep: 0.5
===
[OTHER]: asdf 
	_ build tools and uinit itegration testing, can be done wihtout docker/testcontainers
	_ what you need i for a propper cluster
		_ service discovery (dns, message bus, kv-store)
			_ dns is just a distributeed kv store, which is why service dsicovery goes away
		_ auto bin packing (runtime and allocation)
		_ Load balancing
		_ Automated tolouts and rollbacks
		_ Horizontal scaling
		_ cert manager (ssl, statefull program)
		_ persistant state managment (volumes)
		_ High avalability

[Why use wasmcloud]: pros/cons of wasmcloud
    + <Local development> 
    + <build in observability>: opentelemery comes for free
    + <built in permission engin>: openpolocy
    + <built in service discovery>: 
    + <Netowrking>
    + <Buisniss logic seperation>
    - <Maturity>: Verre not mature #con
	+ <No in process parralelizing>: each commponent is single threaded
	+ <Componens use reactive programing>: do not run when nothing to do
	

 <Netowrking>: Much easyer networking (handled by Nats) 
	+ <No dns/ ip adreessse>: Much easyer networking (h`andled by Nats) 

<Buisniss logic seperation>: cxomponents are stateless, and state is accessed via providers 
	+ <Much less vendor lock in>:
	+ <better seperation of concern>:
	+ <built in providers>:
		+ postgress
		+ seecret managmetn
		+ logging
	+ <no networking in buinsiss logic>: 
	+ <swapping component is much easyer>: therer is much better decuppeling based on interfaces (functions and types), so changing a algorythom from python to rust is trivial
		

<Local development>
	+ <no virtualization problems>
		+ Not run docker via wsl in windows
		+ 
	+ <no host dependant networking>
		+ no issue with bridg networkings on windowns
		+ no messing with ip addresses #
    + <better runtime/no docker>
		+ you can run curl on wasmtime
		+ you can run your integration tests on wasmtime
		+ you can run your unit tests on wasmtime
		+ you can run your unit via other languages on wasmtime
		+ you can run zip on wasmtime
		+ you can run dotnet build on wasmtime
	
/***
 comments
***/


```argdown
<Local development>
	+ <no virtualization problems>
		+ Not run docker via wsl in windows
		+ 
	+ <no host dependant networking>
		+ no issue with bridg networkings on windowns
		+ no messing with ip addresses #
    + <better runtime/no docker>
		<+ asdfa
	
```
