# Process and network decomposition

Apart from logical decomposition, application can be decomposed into multiple processes, and these multiple processes can live in different machines.

## An application can be seperated into multiple processes

<img src="./images/Decomposition%20-%20IPC.png" width="600">

## An application's processes can be separated into multiple distributed services

<img src="./images/Decomposition%20-%20Virtualization.webp" width="600">
<img src="./images/Decomposition%20-%20Containers.png" width="600">

## An application's distributed services can be separated into different machines

<img src="./images/Decomposition%20-%20Distributed%20System.png" width="600">
<img src="./images/Decomposition%20-%20Client-Server.webp" width="600">

## Different databases can lives in different database servers
Microservice architecture advocates for breaking one big monolith database into multiple databases in in different servers: each service has its own database (server).

## Architecture & the 4+1 architecture view model

There are numerous definitions of software architecture. For example, see https://en.wikiquote.org/wiki/Software_architecture to read some of them. My favorite definition comes from Len Bass and colleagues at the Software Engineering Institute (www.sei.cmu.edu), who played a key role in establishing software architecture as a discipline. They define software architecture as follows:

> The software architecture of a computing system is the set of structures needed to reason about the system, which comprise software elements, relations among them, and properties of both. (Documenting Software Architectures by Bass et al.)

That’s obviously a quite abstract definition. But its essence is that an application’s architecture is its **decomposition** into parts (the **elements**) and the relationships (the **relations**) between those parts.

Decomposition is important for a couple of reasons:

- It facilitates the division of labor and knowledge. It enables multiple people (or multiple teams) with possibly specialized knowledge to work productively together on an application.
- It defines how the software elements interact.

It’s the decomposition into parts and the relationships between those parts that determine the application’s -ilities.

### The 4+1 view model of software architecture

More concretely, an application’s architecture can be viewed from multiple perspectives, in the same way that a building’s architecture can be viewed from structural, plumbing, electrical, and other perspectives. Phillip Krutchen wrote a classic paper describing the 4+1 view model of software architecture, “Architectural Blueprints—The ‘4+1’ View Model of Software Architecture” (www.cs.ubc.ca/~gregor/teaching/papers/4+1view-architecture.pdf).
The 4+1 model defines four different views of a software architecture. Each describes a particular aspect of the architecture and consists of a particular set of software elements and relationships between them.
<img src="./images/Decomposition - Architecture.png" width="600">

The purpose of each view is as follows:

- **Logical view**— The software elements that are created by developers. In object-oriented languages, these elements are classes and packages. The relations between them are the relationships between classes and packages, including inheritance, associations, and depends-on.
- **Implementation view**— The output of the build system. This view consists of modules, which represent packaged code, and components, which are executable or deployable units consisting of one or more modules. In Java, a module is a JAR file, and a component is typically a WAR file or an executable JAR file. The relations between them include dependency relationships between modules and composition relationships between components and modules.
- **Process view**— The components at runtime. Each element is a process, and the relations between processes represent interprocess communication.
- **Deployment view**— How the processes are mapped to machines. The elements in this view consist of (physical or virtual) machines and the processes. The relations between machines represent networking. This view also describes the relationship between processes and machines.

In addition to these four views, there are the **scenarios**—the +1 in the 4+1 model—that animate views. Each scenario describes how the various architectural components within a particular view collaborate in order to handle a request. A scenario in the logical view, for example, shows how the classes collaborate. Similarly, a scenario in the process view shows how the processes collaborate.

## Benefits of multiprocess/distributed services

### Parallelism

Multiprocess architecture allows the application to do more than one thing at a time, if you have multicore/multi-CPU system. Even if you have only a single CPU/core, it allows the OS scheduler to ensure that everything that needs to do work gets its fair share of processing time.

Another advantage of separate processes is that they can provide a security barrier. If a program needs to do some work with different permissions (e.g., as root, or even just as a different user), it can spawn a new process running as that other user to do just that bit of work. That way, it's much, much harder for a bug in one part of the code to affect the part running with different permissions. Apache is usually configured to work this way, for example. Only root can bind to low-number ports (like port 80 which is usually used by web servers), so you have to start it as root, and it binds to the port. But it doesn't need root permissions to process each web request, so it spawns a new process with lower permissions to do that work. This provides a huge security benefit since if there's a bug in a script that processes the request that allows an attacker to run arbitrary commands, it's at least running with very little privileges, so it can't access critical system files (at least not without exploiting a second bug to escalate its privileges).

A final difference is that using separate processes is the first step toward allowing you to offload the work onto a completely separate computer (client/server style). So if you're using a program flexible enough that it allows you to spread its work across several computers in a network, it'll probably use processes instead of threads.

### Faster build and startup

And each service typically starts a lot faster than a large monolith does, which also makes developers more productive and speeds up deployments.

### Geographical

Part of the application can reside in different machines, different rooms, different buildings, different parts of the world.

### Independent deployment
Each service can be deployed independently of other services. If the developers responsible for a service need to deploy a change that’s local to that service, they don’t need to coordinate with other developers. They can deploy their changes. As a result, it’s much easier to deploy changes frequently into production.
You can structure the engineering organization as a collection of small (for example, two-pizza) teams. Each team is solely responsible for the development and deployment of one or more related services. Each team can develop, deploy, and scale their services independently of all the other teams. As a result, the development velocity is much higher.

<img src="./images/Decomposition - Microservice - Teams.png" width="600">

The ability to do continuous delivery and deployment has several business benefits:
+ It reduces the time to market, which enables the business to rapidly react to feedback from customers.
+ It enables the business to provide the kind of reliable service today’s customers have come to expect.

### Services are independently scalable
Each service in a microservice architecture can be scaled independently of other services using X-axis cloning and Z-axis partitioning. Moreover, each service can be deployed on hardware that’s best suited to its resource requirements. This is quite different than when using a monolithic architecture, where components with wildly different resource requirements—for example, CPU-intensive vs. memory-intensive—must be deployed together.

### Better fault isolation
The microservice architecture has better fault isolation. For example, a memory leak in one service only affects that service. Other services will continue to handle requests normally. In comparison, one misbehaving component of a monolithic architecture will bring down the entire system.

### Easily experiment with and adopt new technologies
Last but not least, the microservice architecture eliminates any long-term commitment to a technology stack. In principle, when developing a new service, the developers are free to pick whatever language and frameworks are best suited for that service. In many organizations, it makes sense to restrict the choices, but the key point is that you aren’t constrained by past decisions.

Moreover, because the services are small, rewriting them using better languages and technologies becomes practical. If the trial of a new technology fails, you can throw away that work without risking the entire project. This is quite different than when using a monolithic architecture, where your initial technology choices severely constrain your ability to use different languages and frameworks in the future.

### Outsourcing flexibility
It may be necessary for a business to outsource certain functions to third-party partners. Many companies are concerned about protecting intellectual property with a monolithic architecture format. However, a microservices architecture allows businesses to segment areas just for partners that won’t otherwise disclose core services.

## Monolithic, monorepo coupling

- _Versioning coupling_. One problem with so many developers committing to the same code base is that the build is frequently in an unreleasable state. Trying to solve this problem by using feature branches can result in lengthy, painful merges. Consequently, once a team completes its sprint, a long period of testing and code stabilization follows.
- _Dependency management coupling_. Different modules use the same dependency file (e.g. `package.json`).
- _IDE coupling_. Big code base can slow down the IDE, making developers less productive.
- _Build coupling_
- _Deployment coupling_
- _Startup coupling_. Edit-build-run-test loop takes a long time, which badly impact productivity.
- _Resource coupling_. A bug in one module—for example, a memory leak—crashes all instances of the application, one by one. Different application modules have conflicting resource requirements. The restaurant data, for example, is stored in a large, in-memory database, which is ideally deployed on servers with lots of memory. In contrast, the image processing module is CPU intensive and best deployed on servers with lots of CPU. If these modules are part of the same application, FTGO must compromise on the server configuration.
- _Technology coupling_. The monolithic architecture makes it difficult to adopt new frameworks and languages. It would be extremely expensive and risky to rewrite the entire monolithic application so that it would use a new and presumably better technology. Consequently, developers are stuck with the technology choices they made at the start of the project. Quite often, they must maintain an application written using an increasingly obsolete technology stack.

## Coupling in distributed system
Distributed system still have to content with data and control coupling. 

### Communication protocol coupling

The client must use communication protocol the server provide, be it REST or grpc.

#### Authentication coupling

The client need to authenticate with server according to mechamsim the server uses.

#### Availability coupling (synchronous vs. asynchronous communicaton)

Services can use synchronous request/response-based communication mechanisms, such as HTTPbased REST or gRPC. Alternatively, they can use asynchronous, message-based communication mechanisms such as AMQP or STOMP.

- _Synchronous_. The client expects a timely response from the service and might
  even block while it waits.
- _Asynchronous_. The client doesn’t block, and the response, if any, isn’t necessarily sent immediately.

Event-driven architectures have loose coupling within space, time and synchronization, providing a scalable infrastructure for information exchange and distributed workflows. However, event-architectures are tightly coupled, via event subscriptions and patterns, to the semantics of the underlying event schema and values.