# What are the potential costs of decomposition

## Coupling

The different parts of an application cannot work alone. They need to connect with each other somehow in order to solve the problems. For example, one part of the application uses the result from another part. This "connection" is called **coupling**. This basically makes working with one part dependent on the other parts.

Couplings exist, whether the application is decomposed or not, or how granular the decomposition is. The business requirements necessitate a certain of coupling.

When it come to decomposition, the more coupling we have, the less benefit we can get from the decomposition.

<img src="./images/Decomposition - Coupling & Cohesion.png" width="600">
<img src="./images/Decomposition - Coupling.png" width="600">

### Coupling Types

#### Data coupling

This is probably the most severe coupling. Modules share data through, for example, parameters or global data.

Sometimes, modules share a composite data structure and use only parts of it, possibly different parts (e.g., passing a whole record to a function that needs only one field of it). In this situation, a modification in a field that a module does not need may lead to changing the way the module reads the record. There's even a term for this: **Stamp coupling**.

#### Control coupling

One part is executed depending on other parts.

#### Subclass coupling (OOP)

Describes the relationship between a child and its parent. The child is connected to its parent, but the parent is not connected to the child.

## Couplings reduce the benefit from decomposition

There more couplings, the less benefit we can get from decomposition.

- Cognitive load is not reduced as much, as we need to take into account dependent modules.
- Changes in one part are more likely to necessitate changes in other parts.
- Members/teams must communicate more closely if their modules.
- More difficult to isolate test.

## Coupling with decomposition introduce indirection

We now have indirection. For example, instead of seeing the code inline, we have to call a function and passing in the arguments. To understand what the function does, we need to rely on the function name which can be difficult to understand, misleading even: naming is not easy. So, sometimes, we need to read the documentation, which can also be difficult to understand or even misleading. So, sometimes, to be sure, we have to get to the function to read it. The function definition may locate in a different part of the module, or in a different module, different file, even a different repository.

In event-drivent architecture, asynchronous messaging communication, the communication is not direct and asynchronous.

## Decoupling make problems from coupling more severe

The problem couplings introduce can become more severe when we have decomposition. Also, the higher the decomposition level, the worse the problem couplings will introduce.

- When the app is decomposed into distributed services, instead of a method call, we need to use a network calls. Network failure (or configuration error) is a reality. The probability of having one part of your software unreachable is infinitely bigger now.
- Transaction management become much more difficult in distributed enironment.
- Another issue with using the microservice architecture is that developers must deal with the additional complexity of creating a distributed system. Services must use an interprocess communication mechanism. This is more complex than a simple method call. Moreover, a service must be designed to handle partial failure and deal with the remote service either being unavailable or exhibiting high latency.
- Implementing use cases that span multiple services requires the use of unfamiliar techniques. Each service has its own database, which makes it a challenge to implement transactions and queries that span services.
- IDEs and other development tools are focused on building monolithic applications and don’t provide explicit support for developing distributed applications. Writing automated tests that involve multiple services is challenging. These are all issues that are specific to the microservice architecture. Consequently, your organization’s developers must have sophisticated software development and delivery skills in order to successfully use microservices.
- The microservice architecture also introduces significant operational complexity. Many more moving parts—multiple instances of different types of service—must be managed in production. To successfully deploy microservices, you need a high level of automation.

Sometimes, the net benefit can be negative: we're better off reducing the decompotiion granularity.

## Decomposition introduces bad or premature abstraction

This can be both a benefit and a liability.
The abstract can be bad (OOP), premature.

## Other considerations

### Fragment technology stacks

One supposed benefit of microservice architecture is that projects can use different tech stakc. However, this could create a hiring and management nightmare. In fact, may microservice architecture opt to use a standard tech stack.

### Fragment teams

One supposed benefit of microservice architecture is that teams can operate indeepently. However, when different teams don’t need to interact, they may work in their own silos. In the long term, this could result in teams producing their subcultures within the company, such as employing different methodologies of programming or management or utilizing different sets of development tools.

If some team member eventually needs to work in a different team, they may suffer a bit of culture shock and learn a new way of doing their job.

### Granularity

<img src="./images/Granularity of Decomposition.png" width="600">

## Reference

- [Coupling (computer science) - Wikipedia](<https://en.wikipedia.org/wiki/Coupling_(computer_programming)>)
- [What Are Abstractions in Software Engineering with Examples](https://thevaluable.dev/abstraction-type-software-example/)
