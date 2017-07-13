## Why Cloud-Native Application Architectures?

First we’ll examine the common motivations behind moving tocloud-native application architectures.

## Speed

It’s become clear that speed wins in the marketplace. Businesses that are able to innovate, experiment, and deliver software-based solutions quickly are outcompeting those that follow more traditional delivery models.

In the enterprise, the time it takes to provision new application environments and deploy new versions of software is typically measured in days, weeks, or months. This lack of speed severely limits the risk that can be taken on by any one release, because the cost of making and fixing a mistake is also measured on that same timescale.Internet companies are often cited for their practice of deploying hundreds of times per day. Why are frequent deployments important? If you can deploy hundreds of times per day, you can recover from mistakes almost instantly. If you can recover from mistakes almost instantly, you can take on more risk. If you can take on more risk, you can try wild experiments—the results might turn into your next competitive advantage.

The elasticity and self-service nature of cloud-based infrastructure naturally lends itself to this way of working. Provisioning a new application environment by making a call to a cloud service API is faster than a form-based manual process by several orders of magnitude. Deploying code to that new environment via another API call adds more speed. Adding self-service and hooks to teams’ continuous integration/build server environments adds even more speed. Eventually we can measure the answer to Lean guru Mary Poppendick’s question, “How long would it take your organization to deploy a change that involves just one single line of code?” in minutes or seconds.

Imagine what your team...what your business...could do if you were able to move that fast!

## Safety

It’s not enough to go extremely fast. If you get in your car and push the pedal to the floor, eventually you’re going to have a rather expensive (or deadly!) accident. Transportation modes such as aircraft and express bullet trains are built for speed and safety. Cloud-native application architectures balance the need to move rapidly with the needs of stability, availability, and durability. It’s possible and essential to have both.

As we’ve already mentioned, cloud-native application architectures enable us to rapidly recover from mistakes. We’re not talking about mistake prevention, which has been the focus of many expensive hours of process engineering in the enterprise. Big design up front, exhaustive documentation, architectural review boards, and lengthy regression testing cycles all fly in the face of the speed that we’re seeking. Of course, all of these practices were created with good intentions. Unfortunately, none of them have provided consistently measurable improvements in the number of defects that make it into production.

So how do we go fast and safe?

**Visibility**

Our architectures must provide us with the tools necessary to see failure when it happens. We need the ability to measure everything, establish a profile for “what’s normal,” detect devia‐ tions from the norm (including absolute values and rate of change), and identify the components contributing to those deviations. Feature-rich metrics, monitoring, alerting, and data visualization frameworks and tools are at the heart of all cloudnative application architectures.

**Fault isolation**

In order to limit the risk associated with failure, we need to limit the scope of components or features that could be affected by a failure. If no one could purchase products from Ama‐ zon.com every time the recommendations engine went down, that would be disastrous. Monolithic application architectures often possess this type of failure mode. Cloud-native application architectures often employ microservices (“Microservices” on page 10). By composing systems from microservices, we can limit the scope of a failure in any one microservice to just that microservice, but only if combined with fault tolerance.

**Fault tolerance**

It’s not enough to decompose a system into independently deployable components; we must also prevent a failure in one of those components from causing a cascading failure across its possibly many transitive dependencies. Mike Nygard described several fault tolerance patterns in his book Release It! (Pragmatic Programmers), the most popular being the circuit breaker. A software circuit breaker works very similarly to an electrical circuit breaker: it prevents cascading failure by opening the circuit between the component it protects and the remainder of the failing system. It also can provide a graceful fallback behavior, such as a default set of product recommendations, while the circuit is open. We’ll discuss this pattern in detail in “FaultTolerance” on page 42.

**Automated recovery**

With visibility, fault isolation, and fault tolerance, we have the tools we need to identify failure, recover from failure, and provide a reasonable level of service to our customers while we’re engaging in the process of identification and recovery. Some failures are easy to identify: they present the same easily detecta‐ ble pattern every time they occur. Take the example of a service health check, which usually has a binary answer: healthy or unhealthy, up or down. Many times we’ll take the same course of action every time we encounter failures like these. In the case of the failed health check, we’ll often simply restart or redeploy the service in question. Cloud-native application architectures don’t wait for manual intervention in these situations. Instead, they employ automated detection and recovery. In other words, they let a computer wear the pager instead of a human.ScaleAs demand increases, we must scale our capacity to service that demand. In the past we handled more demand by scaling vertically: we bought larger servers. We eventually accomplished our goals, but slowly and at great expense. This led to capacity planning based on peak usage forecasting. We asked “what’s the most computing power this service will ever need?” and then purchased enough hardware to meet that number. Many times we’d get this wrong, and we’d still blow our available capacity during events like Black Friday. But more often we’d be saddled with tens or hundreds of servers with mostly idle CPU’s, which resulted in poor utilization metrics.

Innovative companies dealt with this problem through two pioneer‐ ing moves:

- Rather than continuing to buy larger servers, they horizontallyscaled application instances across large numbers of cheapercommodity machines. These machines were easier to acquire(or assemble) and deploy quickly.
- Poor utilization of existing large servers was improved by virtualizing several smaller servers in the same footprint and deploying multiple isolated workloads to them.

As public cloud infrastructure like Amazon Web Services became available, these two moves converged. The virtualization effort was delegated to the cloud provider, and the consumer focused on horizontal scale of its applications across large numbers of cloud server instances. Recently another shift has happened with the move from virtual servers to containers as the unit of application deployment. We’ll discuss containers in “Containerization” on page 26.

This shift to the cloud opened the door for more innovation, as companies no longer required large amounts of startup capital to deploy their software. Ongoing maintenance also required a lower capital investment, and provisioning via API not only improved the speed of initial deployment, but also maximized the speed with which we could respond to changes in demand.

Unfortunately all of these benefits come with a cost. Applications must be architected differently for horizontal rather than vertical scale. The elasticity of the cloud demands ephemerality. Not only must we be able to create new application instances quickly; we must also be able to dispose of them quickly and safely. This need is a question of state management: how does the disposable interact with the persistent? Traditional methods such as clustered sessions and shared filesystems employed in mostly vertical architectures do not scale very well.

Another hallmark of cloud-native application architectures is the externalization of state to in-memory data grids, caches, and persistent object stores, while keeping the application instance itself essentially stateless. Stateless applications can be quickly created and destroyed, as well as attached to and detached from external state managers, enhancing our ability to respond to changes in demand. Of course this also requires the external state managers themselves to be scalable. Most cloud infrastructure providers have recognized this necessity and provide a healthy menu of such services.

## Mobile Applications and Client Diversity

In January 2014, mobile devices accounted for 55% of Internet usage in the United States. Gone are the days of implementing applications targeted at users working on computer terminals tethered to desks. Instead we must assume that our users are walking around with multicore supercomputers in their pockets. This has serious impli‐ cations for our application architectures, as exponentially more users can interact with our systems anytime and anywhere.

Take the example of viewing a checking account balance. This task used to be accomplished by calling the bank’s call center, taking a trip to an ATM location, or asking a teller at one of the bank’s branch locations. These customer interaction models placed signifi‐ cant limits on the demand that could be placed on the bank’s under‐ lying software systems at any one time.

The move to online banking services caused an uptick in demand, but still didn’t fundamentally change the interaction model. You still had to physically be at a computer terminal to interact with the system, which still limited the demand significantly. Only when we all began, as my colleague Andrew Clay Shafer often says, “walking around with supercomputers in our pockets,” did we start to inflict pain on these systems. Now thousands of customers can interact with the bank’s systems anytime and anywhere. One bank executive has said that on payday, customers will check their balances several times every few minutes. Legacy banking systems simply weren’t architected to meet this kind of demand, while cloud-native application architectures are.

The huge diversity in mobile platforms has also placed demands on application architectures. At any time customers may want to inter‐ act with our systems from devices produced by multiple different vendors, running multiple different operating platforms, running multiple versions of the same operating platform, and from devices of different form factors (e.g., phones vs. tablets). Not only does this place various constraints on the mobile application developers, but also on the developers of backend services.

Mobile applications often have to interact with multiple legacy systems as well as multiple microservices in a cloud-native application architecture. These services cannot be designed to support the unique needs of each of the diverse mobile platforms used by our customers. Forcing the burden of integration of these diverse serv‐ ices on the mobile developer increases latency and network trips, leading to slow response times and high battery usage, ultimately leading to users deleting your app. Cloud-native application architectures also support the notion of mobile-first development through design patterns such as the API Gateway, which transfers the burden of service aggregation back to the server-side. We’ll discuss the API Gateway pattern in “API Gateways/Edge Services” on page 47.