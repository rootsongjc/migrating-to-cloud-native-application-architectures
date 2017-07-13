# Defining Cloud-Native Architectures

Now we’ll explore several key characteristics of cloud-native application architectures. We’ll also look at how these characteristics address motivations we’ve already discussed.

## Twelve-Factor Applications

The twelve-factor app is a collection of patterns for cloud-native application architectures, originally developed by engineers at Heroku. The patterns describe an application archetype that optimizes for the “why” of cloud-native application architectures. They focus on speed, safety, and scale by emphasizing declarative configuration, stateless/shared-nothing processes that horizontally scale, and an overall loose coupling to the deployment environment. Cloud application platforms like Cloud Foundry, Heroku, and Amazon ElasticBeanstalk are optimized for deploying twelve-factor apps.

In the context of twelve-factor, application (or app) refers to a single deployable unit. Organizations will often refer to multiple collaborating deployables as an application. In this context, however, we will refer to these multiple collaborating deploy ables as a distributed system.

A twelve-factor app can be described in the following ways:

**Codebase**

Each deployable app is tracked as one codebase tracked in revision control. It may have many deployed instances across multiple environments.

**Dependencies**

An app explicitly declares and isolates dependencies via appropriate tooling (e.g., Maven, Bundler, NPM) rather than depend‐ing on implicitly realized dependencies in its deployment environment.

**Config**

Configuration, or anything that is likely to differ between deployment environments (e.g., development, staging, production) is injected via operating system-level environment variables.

**Backing services**

Backing services, such as databases or message brokers, aretreated as attached resources and consumed identically across all environments.

**Build, release, run**

The stages of building a deployable app artifact, combining that artifact with configuration, and starting one or more processes from that artifact/configuration combination, are strictly separated.

**Processes**

The app executes as one or more stateless processes (e.g., master/workers) that share nothing. Any necessary state is externalized to backing services (cache, object store, etc.).

**Port banding**

The app is self-contained and exports any/all services via port binding (including HTTP).

**Concurrency**

Concurrency is usually accomplished by scaling out app processes horizontally (though processes may also multiplex work via internally managed threads if desired).

**Disposability**

Robustness is maximized via processes that start up quickly and shut down gracefully. These aspects allow for rapid elastic scaling, deployment of changes, and recovery from crashes.

**Dev/prod parity**

Continuous delivery and deployment are enabled by keeping development, staging, and production environments as similar as possible.

**Logs**

Rather than managing logfiles, treat logs as event streams, allowing the execution environment to collect, aggregate, index, and analyze the events via centralized services.

**Admin processes**

Administrative or managements tasks, such as database migrations, are executed as one-off processes in environments identical to the app’s long-running processes.

These characteristics lend themselves well to deploying applications quickly, as they make few to no assumptions about the environments to which they’ll be deployed. This lack of assumptions allows the underlying cloud platform to use a simple and consistent mechanism, easily automated, to provision new environments quickly and to deploy these apps to them. In this way, the twelve-factor application patterns enable us to optimize for speed.

These characteristics also lend themselves well to the idea of ephemerality, or applications that we can “throw away” with very little cost.The application environment itself is 100% disposable, as any application state, be it in-memory or persistent, is extracted to some backing service. This allows the application to be scaled up and down in a very simple and elastic manner that is easily automated.In most cases, the underlying platform simply copies the existing environment the desired number of times and starts the processes.Scaling down is accomplished by halting the running processes and deleting the environments, with no effort expended backing up or otherwise preserving the state of those environments. In this way, the twelve-factor application patterns enable us to optimize for scale.

Finally, the disposability of the applications enables the underlying platform to automatically recover from failure events very quickly.

Furthermore, the treatment of logs as event streams greatly enables visibility into the underlying behavior of the applications at runtime.
The enforced parity between environments and the consistency of
configuration mechanisms and backing service management enable
cloud platforms to provide rich visibility into all aspects of the appli‐
cation’s runtime fabric. In this way, the twelve-factor application pat‐
terns enable us to optimize for safety.

## Microservices

Microservices represent the decomposition of monolithic business systems into independently deployable services that do “one thing well.” That one thing usually represents a business capability, or the smallest, “atomic” unit of service that delivers business value.

Microservice architectures enable speed, safety, and scale in sever always:

- As we decouple the business domain into independently deployable bounded contexts of capabilities, we also decouple the associated change cycles. As long as the changes are restricted to a single bounded context, and the service continues to fulfill its existing contracts, those changes can be made and deployed independent of any coordination with the rest of the business. The result is enablement of more frequent and rapid deployments, allowing for a continuous flow of value.
- Development can be accelerated by scaling the development organization itself. It’s very difficult to build software faster by adding more people due to the overhead of communication and coordination. Fred Brooks taught us years ago that adding more people to a late software project makes it later. However, rather than placing all of the developers in a single sandbox, we can create parallel work streams by building more sandboxes through bounded contexts.
- The new developers that we add to each sandbox can ramp up and become productive more rapidly due to the reduced cognitive load of learning the business domain and the existing code, and building relationships within a smaller team.
- Adoption of new technology can be accelerated. Large mono‐lithic application architectures are typically associated withlong-term commitments to technical stacks. These commitments exist to mitigate the risk of adopting new technology bysimply not doing it. Technology adoption mistakes are moreexpensive in a monolithic architecture, as those mistakes canpollute the entire enterprise architecture. If we adopt new technology within the scope of a single monolith, we isolate and minimze the risk in much the same way that we isolate and minimize the risk of runtime failure.
- Microservices offer independent, efficient scaling of services.Monolithic architectures can scale, but require us to scale all components, not simply those that are under heavy load. Microservices can be scaled if and only if their associated load requires it.

## Self-Service Agile Infrastructure

Teams developing cloud-native application architectures are typically responsible for their deployment and ongoing operations. Successful adopters of cloud-native applications have empowered teams with self-service platforms.

Just as we create business capability teams to build microservices foreach bounded context, we also create a capability team responsible for providing a platform on which to deploy and operate these microservices (“The Platform Operations Team” on page 22).

The best of these platforms raise the primary abstraction layer fortheir consumers. With infrastructure as a service (IAAS) we asked the API to create virtual server instances, networks, and storage, and then applied various forms of configuration management and automation to enable our applications and supporting services to run.Platforms are now emerging that allow us to think in terms of applications and backing services.

Application code is simply “pushed” in the form of pre-built artifacts (perhaps those produced as part of a continuous delivery pipe‐line) or raw source code to a Git remote. The platform then builds the application artifact, constructs an application environment, deploys the application, and starts the necessary processes. Teams do not have to think about where their code is running or how it got there, as the platform takes care of these types of concerns transparently.

The same model is supported for backing services. Need a database?How about a message queue or a mail server? Simply ask the plat‐form to provision one that fits your needs. Platforms now support a wide range of SQL/NoSQL data stores, message queues, search engines, caches, and other important backing services. These service instances can then be “bound” to your application, with necessary credentials automatically injected into your application’s environment for it to consume. A great deal of messy and error-prone be spoke automation is thereby eliminated.

These platforms also often provide a wide array of additional operational capabilities:

- Automated and on-demand scaling of application instances

- Application health management

- Dynamic routing and load balancing of requests to and acrossapplication instances

- Aggregation of logs and metrics

This combination of tools ensures that capability teams are able to develop and operate services according to agile principles, again enabling speed, safety, and scale.

## API-Based Collaboration

The sole mode of interaction between services in a cloud-native application architecture is via published and versioned APIs. TheseAPIs are typically HTTP REST-style with JSON serialization, but can use other protocols and serialization formats.

Teams are able to deploy new functionality whenever there is a need, without synchronizing with other teams, provided that they do not break any existing API contracts. The primary interaction model for the self-service infrastructure platform is also an API, just as it is with the business services. Rather than submitting tickets to provision, scale, and maintain application infrastructure, those same requests are submitted to an API that automatically services the requests.

Contract compliance can be verified on both sides of a service-to-service interaction via consumer-driven contracts. Service consumers are not allowed to gain access to private implementation details of their dependencies or directly access their dependencies’ data stores. In fact, only one service is ever allowed to gain direct access to any data store. This forced decoupling directly supports the  cloud-native goal of speed.

## Antifragility

The concept of antifragility was introduced in Nassim Taleb’s book Antifragile (Random House). If fragility is the quality of a system that gets weaker or breaks when subjected to stressors, then what is the opposite of that? Many would respond with the idea of robust‐ness or resilience—things that don’t break or get weaker when subjected to stressors. However, Taleb introduces the opposite of fragility as antifragility, or the quality of a system that gets stronger when subjected to stressors. What systems work that way? Consider the human immune system, which gets stronger when exposed to pathogens and weaker when quarantined. Can we build architectures that way? Adopters of cloud-native architectures have sought to build them. One example is the Netflix Simian Army project, with the famous submodule “Chaos Monkey,” which injects random failures into production components with the goal of identifying and eliminating weaknesses in the architecture. By explicitly seeking out weaknesses in the application architecture, injecting failures, and forcing their remediation, the architecture naturally converges on a greater degree of safety over time.			
  ​