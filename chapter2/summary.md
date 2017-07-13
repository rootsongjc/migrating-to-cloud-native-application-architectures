# Summary

In this chapter we’ve examined a few of the changes that most enter‐prises will need to make in order to adopt cloud-native applicationarchitectures. Culturally the overall theme is one of decentralizationand autonomy:

**DevOps**

Decentralization of skill sets into cross-functional teams.

**Continuous delivery**

Decentralization of the release schedule and process.

**Autonomy**

Decentralization of decision making.

We codify this decentralization into two primary team structures:

**Business capability teams**

Cross-functional teams that make their own decisions aboutdesign, process, and release schedule.

**Platform operations teams**

Teams that provide the cross-functional teams with the plat‐form they need to operate.

And technically, we also decentralize control:

**Monoliths to microservices**

Control of individual business capabilities is distributed to individual autonomous services.

**Bounded contexts**

Control of internally consistent subsets of the business domain model is distributed to microservices.

**Containerization**

Control of application packaging is distributed to business capability teams.

**Choreography**

Control of service integration is distributed to the service end‐points.

All of these changes create autonomous units that are able to safelymove at the desired rate of innovation.

In the final chapter, we’ll delve into technical specifics of migrating to cloud-native application architectures through a set of cookbook-style recipes.