# Decomposition Recipes

After discussing the decomposition of data, services, and teams with customers, I’m often asked, “Great! How do we get there from here?” Good question. How do we tear apart existing monoliths and move them to the cloud?

As it turns out, I’ve seen companies succeed with a fairly repeatable pattern of incremental migration which I now recommend to all of my customers. Publicly reference able examples of this pattern can be found at SoundCloud and Karma.

In this section we’ll walk step-by-step through a series of recipes that provide a process for decomposing monolithic services and moving them to the cloud.

## New Features as Microservices

Surprisingly, the first step is not to start chipping away at the monolith itself. We’ll begin with the assumption that you still have a back‐log of features to be built within the monolith. In fact, if you don’thave any net new functionality to build, it’s arguable that youshouldn’t even be considering this decomposition. (Given that our primary motivation is speed, how do you leave something unchanged really fast?)

...the team decided that the best approach to deal with the architec‐ture changes would not be to split the Mothership immediately, butrather to not add anything new to it. All of our new features werebuilt as microservices...

—Phil Calcado, SoundCloud

So it’s time to stop adding new code to the monolith. All new fea‐tures will be built as microservices. Get good at this first, as buildingnew services from scratch is far easier than surgically extractingthem from a big ball of mud.

Inevitably, however, these new microservices will need to talk backto the monolith in order to get anything done. How do we attackthat problem?

## The Anti-Corruption Layer

Because so much of our logic was still in the Rails monolith, pretty much all of our microservices had to talk to it somehow.

—Phil Calcado, SoundCloud

Domain-Driven Design (DDD), by Eric Evans (Addison-Wesley),discusses the idea of an anti-corruption layer. Its purpose is to allow the integration of two systems without allowing the domain model of one system to corrupt the domain model of the other. As you build new functionality into microservices, you don’t want these new services to become tightly coupled with the monolith by giving them deep knowledge of the monolith’s internals. The anti-corruption layer is a way of creating API contracts that make the monolith look like other microservices.

Evans divides the implementation of anti-corruption layers intothree submodules, the first two representing classic design patterns

(from Gamma et al., Design Patterns: Elements of Reusable Object-Oriented So ware [Addison Wesley]):

**Facade**

The purpose of the facade module here is to simplify the pro‐cess of integrating with the monolith’s interface. It’s very likelythat the monolith was not designed with this type of integrationin mind, so the facade’s purpose is to solve this problem. Importantly, it does not change the monolith’s model, being careful not to couple translation and integration concerns.

**Adapter**

The adapter is where we define “services” that provide things our new features need. It knows how to take a request from our system, using a protocol that it understands, and make that request to the monolith’s facade(s).

**Translator**

The translator’s responsibility is to convert requests and responses between the domain model of the monolith and the domain model of the new microservice.

These three loosely coupled components solve three problems:

1. System integration
2. Protocol translation
3. Model translation

What remains is the location of the communication link. In DDD,Evans discusses two alternatives. The first, facade to system, is primarily useful when you can’t access or alter the legacy system. Our focus here is on monoliths we do control, so we’ll lean toward Evans’ second suggestion, adapter to facade. Using this alternative, we build the facade into the monolith, allowing communications to occur between the adapter and the facade, as presumably it’s easier to create this link between two things written explicitly for this purpose.

Finally, it’s important to note that anti-corruption layers can facili‐tate two-way communication. Just as our new microservices mayneed to communicate with the monolith to accomplish work, theinverse may be true as well, particularly as we move on to our nextphase.

## Strangling the Monolith

After the architecture changes were made, our teams were free to build their new features and enhancements in a much more flexible environment. An important question remained, though: how do we extract the features from the monolithic Rails application calledMothership?

—Phil Calcado, SoundCloud

I borrow the idea of “strangling the monolith” from Martin Fowler’s article entitled “StranglerApplication”. In this article, Fowler explains the idea of gradually creating “a new system around the edges of the old, letting it grow slowly over several years until the old system is strangled.” We’re effectively going to do the same thing here. Through a combination of extracted microservices and additional anti-corruption layers, we’ll build a new cloud-native system around the edges of the existing monolith.

Two criteria help us choose which components to extract:

1. SoundCloud nails the first criterion: identify bounded contexts within the monolith. If you’ll recall our earlier discussions of bounded contexts, they require a domain model that is internally consistent. It’s extremely likely that our monolith’s domain model is not internally consistent. Now it’s time to start identifying submodels that can be. These are our candidates for extraction.
2. Our second criterion deals with priority: which of our candidates do we extract first? We can answer this by reviewing our first reason for moving to cloud-native architecture: speed of innovation. What candidate microservices will benefit most from speed of innovation? We obviously want to choose those that are changing the most given our current business needs.Look at the monolith’s backlog. Identify the areas of the monolith’s code that will need to change in order to deliver the changed requirements, and then extract the appropriate bounded contexts before making the desired changes.

## Potential End States

How do we know when we are finished? There are basically two end states:

1. The monolith has been completely strangled to death. All bounded contexts have been extracted into microservices. The final step is to identify opportunities to eliminate anti-corruption layers that are no longer necessary.
2. The monolith has been strangled to a point where the cost of additional service extraction exceeds the return on the necessary development efforts. Some portions of the monolith maybe fairly stable—we haven’t changed them in years and they’re doing their jobs. There may not be much value in moving these portions around, and the cost of maintaining the necessary anti-corruption layers to integrate with them may be low enough that we can take it on long-term.