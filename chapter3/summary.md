# Summary

In this chapter we walked through two sets of recipes that can helpus move toward a cloud-native application architecture:

**Decomposition**

We break down monolithic applications by:

1. Building all new features as microservices.
2. Integrating new microservices with the monolith via anti-corruption layers.
3. Strangling the monolith by identifying bounded contextsand extracting services.

**Distributed systems**

We compose distributed systems by:

1. Versioning, distributing, and refreshing configuration via a configuration server and management bus.
2. Dynamically discovering remote dependencies.
3. Decentralizing load balancing decisions.
4. Preventing cascading failures through circuit breakers and bulkheads.
5. Integrating on the behalf of specific clients via API Gate‐ways.

Many additional helpful patterns exist, including those for automated testing and the construction of continuous delivery pipelines.For more information, the reader is invited to read “Testing Strategies in a Microservice Architecture” by Toby Clemson and Continuous Delivery: Reliable So ware Releases through Build, Test, andDeployment Automation by Jez Humble and David Farley (Addison-Wesley).