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

#### Subclass coupling (OOP)

Describes the relationship between a child and its parent. The child is connected to its parent, but the parent is not connected to the child.

#### Communication protocol coupling

The client must use communication protocol the server provide, be it REST or grpc.

#### Authentication coupling

The client need to authenticate with server according to mechamsim the server uses.

#### Monolithic, monorepo coupling

- _Versioning coupling_. One problem with so many developers committing to the same code base is that the build is frequently in an unreleasable state. Trying to solve this problem by using feature branches can result in lengthy, painful merges. Consequently, once a team completes its sprint, a long period of testing and code stabilization follows.
- _Dependency management coupling_. Different modules use the same dependency file (e.g. `package.json`).
- _IDE coupling_. Big code base can slow down the IDE, making developers less productive.
- _Build coupling_
- _Deployment coupling_
- _Startup coupling_. Edit-build-run-test loop takes a long time, which badly impact productivity.
- _Resource coupling_. A bug in one module—for example, a memory leak—crashes all instances of the application, one by one. Different application modules have conflicting resource requirements. The restaurant data, for example, is stored in a large, in-memory database, which is ideally deployed on servers with lots of memory. In contrast, the image processing module is CPU intensive and best deployed on servers with lots of CPU. If these modules are part of the same application, FTGO must compromise on the server configuration.
- _Technology coupling_. The monolithic architecture makes it difficult to adopt new frameworks and languages. It would be extremely expensive and risky to rewrite the entire monolithic application so that it would use a new and presumably better technology. Consequently, developers are stuck with the technology choices they made at the start of the project. Quite often, they must maintain an application written using an increasingly obsolete technology stack.

### Synchronous vs. asynchronous

There is an important dimention when we talk about coupling: (a)synchronity.

One service needs to another service to be available.

### Code coupling (high)

One module uses the code of another module, for instance a branch.

## Couplings reduce the benefit from decomposition

- Cognitive load is not reduced as much, as we need to take into account dependent modules.
- Changes in one part are more likely to necessitate changes in other parts.
- Members/teams must communicate more closely if their modules.
- More difficult to isolate test.

Moreover, the problem couplings introduce can become more severe when we have decomposition. Also, the higher the decomposition level, the worse the problem couplings will introduce.

- We now have indirection. For example, instead of seeing the code inline, we have to call a function and passing in the arguments. To understand what the function does, we need to rely on the function name which can be difficult to understand, misleading even: naming is not easy. So, sometimes, we need to read the documentation, which can also be difficult to understand or even misleading. So, sometimes, to be sure, we have to get to the function to read it. The function definition may locate in a different part of the module, or in a different module, different file, even a different repository.
- When the app is decomposed into distributed services, instead of a method call, we need to use a network calls.

Sometimes, decompose introduces other types of coupling.

- protocol

Sometimes, the net benefit can be negative: we're better off reducing the decompotiion granularity.

## Indirection

### Distributed systems are complex

Another issue with using the microservice architecture is that developers must deal with the additional complexity of creating a distributed system. Services must use an interprocess communication mechanism. This is more complex than a simple method call. Moreover, a service must be designed to handle partial failure and deal with the remote service either being unavailable or exhibiting high latency.

Implementing use cases that span multiple services requires the use of unfamiliar techniques. Each service has its own database, which makes it a challenge to implement transactions and queries that span services. As described in chapter 4, a microservices-based application must use what are known as sagas to maintain data consistency across services. Chapter 7 explains that a microservices-based application can’t retrieve data from multiple services using simple queries. Instead, it must implement queries using either API composition or CQRS views.

IDEs and other development tools are focused on building monolithic applications and don’t provide explicit support for developing distributed applications. Writing automated tests that involve multiple services is challenging. These are all issues that are specific to the microservice architecture. Consequently, your organization’s developers must have sophisticated software development and delivery skills in order to successfully use microservices.

The microservice architecture also introduces significant operational complexity. Many more moving parts—multiple instances of different types of service—must be managed in production. To successfully deploy microservices, you need a high level of automation. You must use technologies such as the following:

- Automated deployment tooling, like Netflix Spinnaker
- An off-the-shelf PaaS, like Pivotal Cloud Foundry or Red Hat OpenShift
- A Docker orchestration platform, like Docker Swarm or Kubernetes

## Abstraction

## Costs of Multi-Repo

## Higher barriers of entry

When new staff members start working for a company, they need to download the code and install the required tools to begin working on their tasks. Suppose the project is scattered across many repositories, each having its installation instructions and tooling required. In that case, the initial setup will be complex, and more often than not, the documentation will not be complete, requiring these new team members to reach out to colleagues for help.

A monorepo simplifies matters. Since there is a single location containing all code and documentation, you can streamline the initial setup.

## Painful application-wide refactorings

When creating an application-wide refactoring of the code, multiple libraries will be affected. If you’re hosting them via multiple repositories, managing all the different pull requests to keep them synchronized with each other can prove to be a challenge.

A monorepo makes it easy to perform all modifications to all code for all libraries and submit it under a single pull request.

## Libraries must constantly be re-synced

When a new version of a library containing breaking changes is released, libraries depending on this library will need to be adapted to start using the latest version. If the release cycle of the library is faster than that of its dependent libraries, they could quickly become out of sync with each other.

Teams will need to constantly catch up to use the latest releases from other teams. Given that different teams have different priorities, this may sometimes prove arduous to achieve.

Consequently, a team not able to catch up may end up sticking to the outdated version of the depended-upon library. This outcome will have implications on the application (in terms of security, speed, and other considerations), and the gap in development across libraries may only get wider.

## May fragment teams

When different teams don’t need to interact, they may work in their own silos. In the long term, this could result in teams producing their subcultures within the company, such as employing different methodologies of programming or management or utilizing different sets of development tools.

If some team member eventually needs to work in a different team, they may suffer a bit of culture shock and learn a new way of doing their job.
