# Technical Change

Now we can turn to some implementation issues in moving to a DevOps platform in the cloud.

## Decomposing Monoliths

Traditional n-tier, monolithic enterprise applications rarely operate well when deployed to cloud infrastructure, as they often make unsupportable assumptions about their deployment environment that cloud infrastructures simply cannot provide. A few examples include:

- Access to mounted, shared filesystems

- Peer-to-peer application server clustering

- Shared libraries

- Configuration files sitting in well-known locations

Most of these assumptions are coupled with the fact that monoliths are typically deployed to long-lived infrastructure. Unfortunately, they are not very compatible with the idea of elastic and ephemeral infrastructure.

But let’s assume that we could build a monolith that does not make any of these assumptions. We still have trouble:

-   Monoliths couple change cycles together such that independent business capabilities cannot be deployed as required, preventing speed of innovation.

-   Services embedded in monoliths cannot be scaled independently of other services, so load is far more difficult to account for efficiently.

-   Developers new to the organization must acclimate to a new team, often learn a new business domain, and become familiar with an extremely large codebase all at once. This only adds to the typical 3–6 month ramp up time before achieving real productivity.

-   Attempting to scale the development organization by adding more people further crowds the sandbox, adding expensive coordination and communication overhead.

-   Technical stacks are committed to for the long term. Introducing new technology is considered too risky, as it can adversely affect the entire monolith.

The observant reader will notice that this list is the inverse of the list from “Microservices” on page 10. The decomposition of the organization into business capability teams also requires that we decompose applications into microservices. Only then can we harness the maximum benefit from our move to cloud infrastructure.

## Decomposing Data

It’s not enough to decompose monolithic applications into microservices. Data models must also be decoupled. If business capability teams are supposedly autonomous but are forced to collaborate via a single data store, the monolithic barrier to innovation is simply relocated.

In fact, it’s arguable that product architecture must start with the data. The principles found in Domain-Driven Design (DDD), by EricEvans (Addison-Wesley), argue that our success is largely governed by the quality of our domain model (and the ubiquitous language that underpins it). For a domain model to be effective, it must also be internally consistent—we should not find terms or concepts withinconsistent definitions within the same model.

It is incredibly difficult and costly (and arguably impossible) to create a federated domain model that does not suffer from such inconsistencies. Evans refers to internally consistent subsets of the overall domain model of the business as bounded contexts.

When working with an airline customer recently, we were discus‐sing the concepts most central to their business. Naturally the topicof “airline reservation” came up. The group could count seventeen different logical definitions of reservation within its business, with little to no hope of reconciling them into one. Instead, all of the nuance of each definition was carefully baked into a single concept, which became a huge bottleneck for the organization.

Bounded contexts allow you to keep inconsistent definitions of a single concept across the organization, as long as they are defined consistently within the contexts themselves.

  So we begin by identifying the segments of the domain model that can be made internally consistent. We draw fixed boundaries around these segments, which become our bounded contexts. We’re then able to align business capability teams with these contexts, and those teams build microservices providing those capabilities.

  This definition of microservice provides a useful rubric for definingwhat your twelve-factor apps ought to be. Twelve-factor is primarily a technical specification, whereas microservices are primarily a business specification. We define our bounded contexts, assign them a set of business capabilities, commission capability teams to own those business capabilities, and have them build twelve-factor applications. The fact that these applications are independently deployable provides business capability teams with a useful set of technical tools for operation.

  We couple bounded contexts with the database per service pattern,where each microservice encapsulates, governs, and protects its own domain model and persistent store. In the database per service pat‐tern, only one application service is allowed to gain access to a logical data store, which could exist as a single schema within a multi‐tenant cluster or a dedicated physical database. Any external access to the concepts is made through a well-defined business contract implemented as an API (often REST but potentially any protocol).

This decomposition allows for the application of polyglot persis‐tence, or choosing different data stores based on data shape andread/write access patterns. However, data must often be recomposedvia event-driven techniques in order to ask cross-context questions.Techniques such as command query responsibility segregation(CQRS) and event sourcing, beyond the scope of this report, areoften helpful when synchronizing similar concepts across contexts.

## Containerization

Container images, such as those prepared via the LXC, Docker, orRocket projects, are rapidly becoming the unit of deployment for cloud-native application architectures. Such container images are then instantiated by various scheduling solutions such as Kubernetes, Marathon, or Lattice. Public cloud providers such as Amazon and Google also provide first-class solutions for container scheduling and deployment. Containers leverage modern Linux kernel primitives such as control groups (cgroups) and namespaces to pro‐vide similar resource allocation and isolation features as those provided by virtual machines with much less overhead and muchgreater portability. Application developers will need to become comfortable packaging applications as container images to take full advantage of the features of modern cloud infrastructure.

## From Orchestration to Choreography

Not only must service delivery, data modeling, and governance be decentralized, but also service integration. Enterprise integration ofservices has traditionally been accomplished via the enterprise ser‐vice bus (ESB). The ESB becomes the owner of all routing, transformation, policy, security, and other decisions governing the interaction between services. We call this orchestration, analogous to theconductor who determines the course of the music performed by anorchestra during its performance. ESBs and orchestration make forvery simple and pleasing architecture diagrams, but their simplicityis deceiving. Often hiding within the ESB is a tangled web of com‐plexity. Managing this complexity becomes a full-time occupation,and working with it becomes a continual bottleneck for the applica‐tion development team. Just as we saw with a federated data model,a federated integration solution like the ESB becomes a monolithichazard to speed.

Cloud-native architectures, such as microservices, tend to prefer choreography, akin to dancers in a ballet. Rather than placing the smarts in the integration mechanism, they are placed in the end‐points, akin to the dumb pipes and smart filters of the Unix architecture. When circumstances on stage differ from the original plan, there’s no conductor present to tell the dancers what to do. Instead, they simply adapt. In the same way, services adapt to changing circumstances in their environment via patterns such as client-side load balancing (“Routing and Load Balancing” on page 39) and circuit breakers (“Fault-Tolerance” on page 42).

While the architecture diagrams tend to look like a tangled web, their complexity is no greater than a traditional SOA. Choreography simply acknowledges and exposes the essential complexity of the system. Once again this shift is in support of the autonomy required to enable the speed sought from cloud-native architectures. Teams are able to adapt to their changing circumstances without the difficult overhead of coordinating with other teams, and avoid the over‐head of coordinating changes with a centrally-managed ESB.