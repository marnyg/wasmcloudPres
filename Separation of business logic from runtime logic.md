#slide 
* Components can *Only*  know about the interface of their providers, not their implementation
	*  IE: kv-store could be a redis or nats or consul. but the code can not know
	*  [[Example providers]]
	*  [[Example components]]
* No networking/databases/secret-provider etc in component code
* Components can be MUCH smaller than Docker container often are
	* Both in logic they contain, and in runtime cost
* Components can be swapped out with other programing languages at a later time