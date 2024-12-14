# What are the potential benefits of decomposition?

<img src="./images/Decomposition - Car.png" width="600">

Decomposition addresses the challenge of understanding and managing complexity. It involves breaking down a complex problem or system into smaller, more manageable parts. Good decomposition allows us to solve each independently. In this way, the overall problem is solved or system is constructed by solving or designing each part and then combining them together.

## Comprehensibility

By dividing a complex problem into smaller parts, you can reduce the cognitive load, focus on one aspect at a time, and avoid getting lost in irrelevant details or assumptions. Breaking down complex problems also helps you to communicate more effectively with others, as you can explain your problem and your solution in a clear and logical way, and invite feedback and collaboration.

## Easier Changes

It should be possible to make drastic changes to one module without a need to change others: faster and less risky.

## Easier Coordination/Communication

Separate groups would work on each module with little need for communication.

## Reusability

A function can be re-used at many places.

## Test Isolation

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

## Reference

- [Decomposition (computer science) - Wikipedia](<https://en.wikipedia.org/wiki/Decomposition_(computer_science)>)
- [Modular programming - Wikipedia](https://en.wikipedia.org/wiki/Modular_programming)