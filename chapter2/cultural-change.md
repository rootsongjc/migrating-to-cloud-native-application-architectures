# Cultural Change

A great deal of the changes necessary for enterprise IT shops to adopt cloud-native architectures will not be technical at all. They will be cultural and organizational changes that revolve around eliminating structures, processes, and activities that create waste. In this section we’ll examine the necessary cultural shifts.

## From Silos to DevOps

Enterprise IT has typically been organized into many of the follow‐ing silos:

- Software development
- Quality assurance
- Database administration
- System administration
- IT operations
- Release management
- Project management

These silos were created in order to allow those that understand a given specialty to manage and direct those that perform the work of that specialty. These silos often have different management hierarchies, toolsets, communication styles, vocabularies, and incentive structures. These differences inspire very different paradigms of the purpose of enterprise IT and how that purpose should be accomplished.

An often cited example of these conflicting paradigms is the view of change possessed by the development and operations organizations.Development’s mission is usually viewed as delivering additional value to the organization through the development of software features. These features, by their very nature, introduce change into theIT ecosystem. So development’s mission can be described as “delivering change,” and is very often incentivized around how much change it delivers.

Conversely, IT operations’ mission can be described as that of “pre‐venting change.” How? IT operations is usually tasked with main‐taining the desired levels of availability, resiliency, performance, anddurability of IT systems. Therefore they are very often incentivized to maintain key perfomance indicators (KPIs) such as mean time between failures (MTBF) and mean time to recovery (MTTR). One of the primary risk factors associated with any of these measures is the introduction of any type of change into the system. So, rather than find ways to safely introduce development’s desired changes into the IT ecosystem, the knee-jerk reaction is often to put processes in place that make change painful, and thereby reduce the rate of change.

 These differing paradigms obviously lead to many additional suboptimal collaborations. Collaboration, communication, and simple handoff of work product becomes tedious and painful at best, and absolutely chaotic (even dangerous) at worst. Enterprise IT often tries to “fix” the situation by creating heavyweight processes driven by ticket-based systems and committee meetings. And the enterprise IT value stream slows to a crawl under the weight of all of the nonvalue-adding waste.

Environments like these are diametrically opposed to the cloud-native idea of speed. Specialized silos and process are often motivated by the desire to create a safe environment. However they usually offer very little additional safety, and in some cases, make things worse!

At its heart, DevOps represents the idea of tearing down these silo sand building shared toolsets, vocabularies, and communication structures in service of a culture focused on a single goal: delivering value rapidly and safely. Incentive structures are then created that rein force and award behaviors that lead the organization in the direction of that goal. Bureaucracy and process are replaced by trust and accountability.

In this new world, development and IT operations report to the same immediate leadership and collaborate to find practices that support both the continuous delivery of value and the desired levels of availability, resiliency, performance, and durability. Today these context-sensitive practices increasingly include the adoption of cloud-native application architectures that provide the technological support needed to accomplish the organization’s new shared goals.

## From Punctuated Equilibrium to Continuous Delivery

Enterprises have often adopted agile processes such as Scrum, but only as local optimizations within development teams.

As an industry we’ve actually become fairly successful in transition‐ing individual development teams to a more agile way of working.We can begin projects with an inception, write user stories, and carry out all the routines of agile development such as iteration planning meetings, daily standups, retrospectives, and customer showcase demos. The adventurous among us might even venture into engineering practices like pair programming and test-driven development. Continuous integration, which used to be a fairly radical concept, has now become a standard part of the enterprise soft‐ware lexicon. In fact, I’ve been a part of several enterprise softwareteams that have established highly optimized “story to demo” cycles,with the result of each development iteration being enthusiasticallyaccepted during a customer demo.

But then these teams would receive that dreaded question:When can we see these features in our production environment?

   This question is the most difficult for us to answer, as it forces us toconsider forces that are beyond our control:

-    How long will it take for us to navigate the independent quality assurance process?

-    When will we be able to join a production release train?

-    Can we get IT operations to provision a production environment for us in time?

It’s at this point that we realize we’re embedded in what Dave Westhas called the water scrum fall. Our team has moved on to embrace agile principles, but our organization has not. So, rather than eachiteration resulting in a production deployment (this was the original intent behind the Agile Manifesto value of working so ware), the code is actually batched up to participate in a more traditional downstream release cycle.

This operating style has direct consequences. Rather than each iteration resulting in value delivered to the customer and valuable feed‐back pouring back into the development team, we continue a “punctuated equilibrium” style of delivery. Punctuated equilibrium actually short-circuits two of the key benefits of agile delivery:

- Customers will likely go several weeks without seeing new value in the software. They perceive that this new agile way of work‐ing is just “business as usual,” and do not develop the promisedincreased trust relationship with the development team.Because they don’t see a reliable delivery cadence, they revert totheir old practices of piling as many requirements as possibleinto releases. Why? Because they have little confidence that any software delivery will happen soon, they want as much value as possible to be included when it finally does occur.
- Teams may go several weeks without real feedback. Demos are great, but any seasoned developer knows that the best feedback comes only after real users engage with production software.That feedback provides valuable course corrections that enable teams to “build the right thing.” By delaying this feedback, the likelihood that the wrong thing gets built only increases, along with the associated costly rework.

Gaining the benefits of cloud-native application architectures requires a shift to continuous delivery. Rather than punctuated equilibrium driven by a water scrum fall organization, we embrace the principles of value from end to end. A useful model for envisioning such a lifecycle is the idea of “Concept to Cash” described by Maryand Tom Poppendieck in their book Implementing Lean So wareDevelopment (Addison-Wesley). This approach considers all of theactivities necessary to carry a business idea from its conception tothe point where it generates profit, and constructs a value streamaligning people and process toward the optimal achievement of thatgoal.

We technically support this way of working with the engineering practices of continuous delivery, where every iteration (in fact, every source code commit!) is proven to be deployable in an automatedfashion. We construct deployment pipelines which automate every test which would prevent a production deployment should that test fail. The only remaining decision to make is a business decision:does it make good business sense to deploy the available new fea‐tures now? We already know they work as advertised, so do we wantto give them to our customers? And because the deployment pipe‐line is fully automated, the business is able to act on that decision with the click of a button.

## Centralized Governance to Decentralized Autonomy

   One portion of the waterscrumfall culture merits a special mention,as I have seen it become a real sticking point in cloud-native adop‐tion.

   Enterprises normally adopt centralized governance structuresaround application architecture and data management, with com‐mittees responsible for maintaining guidelines and standards, aswell as approving individual designs and changes. Centralized gov‐ernance is intended to help with a few issues:

-    It can prevent widespread inconsistencies in technology stacks, decreasing the overall maintenance burden for the organization.

-    It can prevent widespread inconsistencies in architectural choices, allowing for a common view of application development across the organization.

-    Cross-cutting concerns like regulatory compliance can be handled in a consistent way for the entire organization.

-    Ownership of data can be determined by those who have abroad view of all organizational concerns.

These structures are created with the belief that they will result in higher quality, lower costs, or both. However, these structures rarelyresult in the quality improvements or cost savings desired, and fur‐ther prevent the speed of delivery sought from cloud-native applica‐tion architectures. Just as monolithic application architectures can create bottlenecks which limit the speed of technical innovation, monolithic governance structures can do the same. Architectural committees often only assemble periodically, and long waiting queues of work often ensue. Even small data model changes—changes that could be implemented in minutes or hours, and that would be readily approved by the committee—lay wasting in a never-growing stack of to-do items.

Adoption of cloud-native application architectures is almost always coupled with a move to decentralized governance. The teams build‐ing cloud-native applications (“Business Capability Teams” on page21) own all facets of the capability they’re charged with delivering.They own and govern the data, the technology stack, the application architecture, the design of individual components, and the API con‐tract delivered to the remainder of the organization. If a decision needs to be made, it’s made and executed upon autonomously by the team.

The decentralization and autonomy of individual teams is balanced by minimal, lightweight structures that are imposed on the integration patterns used between independently developed and deployed services (e.g., they prefer HTTP REST JSON APIs rather than many different styles of RPC). These structures often emerge through grass roots adoption of solutions to cross-cutting problems like fault tolerance. Teams are encouraged to devise solutions to these problems locally, and then self-organize with other teams to establish common patterns and frameworks. As a preferred solution for the  entire organization emerges, ownership of that solution is very often transfered to a cloud frameworks/tools team, which may or may not be embedded in the platform operations team (“The Platform Operations Team” on page 22). This cloud frameworks/tools team will  often pioneer solutions as well while the organization is reforming around a shared understanding of the architecture.
