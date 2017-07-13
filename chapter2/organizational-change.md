# Organizational Change

In this section we’ll examine the necessary changes to how organizations create teams when adopting cloud-native application architectures. The theory behind this reorganization is the famous observa‐tion known as Conway’s Law. Our solution is to create a team com‐bining staff with many disciplines around each long-term product,instead of segregating staff that have a single discipline in each ownteam, such as testing.

## Business Capability Teams

Any organization that designs a system (defined broadly) will produce a design whose structure is a copy of the organization’s communication structure.

—Melvyn Conway

We’ve already discussed in “From Silos to DevOps” on page 15 the practice of organizing IT into specialized silos. Quite naturally, having created these silos, we have also placed individuals into team saligned with these silos. But what happens when we need to build anew piece of software?

A very common practice is to commission a project team. The team is assigned a project manager, and the project manager then collaborates with various silos to obtain “resources” for each specialty needed to staff the project. Part of what we learn from Conway’sLaw, quoted above, is that these teams will then very naturally produce in their system design the very silos from which they hail. And so we end up with siloed architectures having modules aligned with the silos themselves:

- Data access tier
- Services tier
- Web MVC tier
- Messaging tier
- Etc.

Each of these tiers spans multiple identifiable business capabilities, making it very difficult to innovate and deploy features related to one business capability independently from the others.

Companies seeking to move to cloud-native architectures like microservices segregated by business capability have often employed what Thoughtworks has called the Inverse Conway Maneuver.Rather than building an architecture that matches their org chart, they determine the architecture they want and restructure their organization to match that architecture. If you do that, according toConway, the architecture that you desire will eventually emerge.

   So, as part of the shift to a DevOps culture, teams are organized ascross-functional, business capability teams that develop productsrather than projects. Products are long-lived efforts that continueuntil they no longer provide value to the business. (You’re donewhen your code is no longer in production!) All of the roles neces‐sary to build, test, deliver, and operate the service delivering a busi‐ness capability are present on a team, which doesn’t hand off code toother parts of the organization. These teams are often organized as“two-pizza teams”, meaning that the team is too big if it cannot befed with two pizzas.

   What remains then is to determine what teams to create. If we fol‐low the Inverse Conway Maneuver, we’ll start with the domainmodel for the organization, and seek to identify business capabilitiesthat can be encapsulated within bounded contexts (which we’ll coverin “Decomposing Data” on page 24). Once we identify these capabil‐ities, we create business capability teams to own them throughouttheir useful lifecycle. Business capability teams own the entiredevelopment-to-operations lifecycle for their applications.

## The Platform Operations Team

The business capability teams need to rely on the self-service agile infrastructure described earlier in “Self-Service Agile Infrastructure”on page 11. In fact, we can express a special business capability defined as “the ability to develop, deploy, and operate business capabilities.” This capability is owned by the platform operations team.

The platform operations team operates the self-service agile infra‐structure platform leveraged by the business capability teams. This team typically includes the traditional system, network, and storage administrator roles. If the company is operating the cloud platform on premises, this team also either owns or collaborates closely with teams managing the data centers themselves, and understands the hardware capabilities necessary to provide an infrastructure plat‐form.

IT operations has traditionally interacted with its customers via avariety of ticket-based systems. Because the platform operation steam operates a self-service platform, it must interact differently.Just as the business capability teams collaborate with one another around defined API contracts, the platform operations team presents an API contract for the platform. Rather than queuing up requests for application environments and data services to be provisioned, business capability teams are able to take the leaner approach of building automated release pipelines that provision environments and services on-demand.

   ​