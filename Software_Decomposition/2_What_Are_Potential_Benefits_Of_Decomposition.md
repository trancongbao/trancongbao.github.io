# What are the potential benefits of decomposition?

<img src="./images/Decomposition%20-%20Car.png" width="600">

Decomposition addresses the challenge of understanding and managing complexity. It involves breaking down a complex problem or system into smaller, more manageable parts. Good decomposition allows us to solve each independently. In this way, the overall problem is solved or system is constructed by solving or designing each part and then combining them together.

## Comprehensibility

By dividing a complex problem into smaller parts, you can reduce the cognitive load, focus on one aspect at a time, and avoid getting lost in irrelevant details or assumptions. Breaking down complex problems also helps you to communicate more effectively with others, as you can explain your problem and your solution in a clear and logical way, and invite feedback and collaboration.

## Easier Changes

It should be possible to make drastic changes to one module without a need to change others: faster and less risky.

## Coordination/Communication

Separate groups would work on each module with little need for communication.

## Reusability

A function can be re-used at many places.

## Test isolation

## Benefits of multi-repo

### Versioning decoupling

One problem with so many developers committing to the same code base is that the build is frequently in an unreleasable state. Trying to solve this problem by using feature branches can result in lengthy, painful merges. Consequently, once a team completes its sprint, a long period of testing and code stabilization follows.

### Independent library versioning

When tagging a repository, its whole codebase is assigned the “new” tag. Since only the code for a specific library is on the repository, the library can be tagged and versioned independently of all other libraries hosted elsewhere.
Having an independent version for every library helps define the dependency tree for the application, allowing us to configure what version of each library to use.

### Independent service releases

Since the repository only contains the code for some service and nothing else, it can have its own deployment cycle, independently of any progress made on the applications accessing it.

The service can use a fast release cycle such as continuous delivery (where new code is deployed after it passes all the tests). Some libraries accessing the service may use a slower release cycle, such as those that only produce a new release once a week.

### Helps define access control across the organization

Only the team members involved with developing a library need to be added to the corresponding repository and download its code. As a result, there’s an implicit access control strategy for each layer in the application. Those involved with the library will be granted editing rights, and everyone else may get no access to the repository. Or they may be given reading but not editing rights.

### Allows teams to work autonomously

Team members can design the library’s architecture and implement its code working in isolation from all other teams. They can make decisions based on what the library does in the general context without being affected by the specific requirements from some external team or application.

### Less load on IDE when only one repo needs to be worked on

Less load on IDE when only one repo needs to be worked on.

## Benefits of multi-process (multi)

### Parallelism

Multiprocess architecture allows the application to do more than one thing at a time, if you have multicore/multi-CPU system. Even if you have only a single CPU/core, it allows the OS scheduler to ensure that everything that needs to do work gets its fair share of processing time.

Another advantage of separate processes is that they can provide a security barrier. If a program needs to do some work with different permissions (e.g., as root, or even just as a different user), it can spawn a new process running as that other user to do just that bit of work. That way, it's much, much harder for a bug in one part of the code to affect the part running with different permissions. Apache is usually configured to work this way, for example. Only root can bind to low-number ports (like port 80 which is usually used by web servers), so you have to start it as root, and it binds to the port. But it doesn't need root permissions to process each web request, so it spawns a new process with lower permissions to do that work. This provides a huge security benefit since if there's a bug in a script that processes the request that allows an attacker to run arbitrary commands, it's at least running with very little privileges, so it can't access critical system files (at least not without exploiting a second bug to escalate its privileges).

A final difference is that using separate processes is the first step toward allowing you to offload the work onto a completely separate computer (client/server style). So if you're using a program flexible enough that it allows you to spread its work across several computers in a network, it'll probably use processes instead of threads.

## Faster build and startup

Edit-build-run-test loop takes less time, which improves productivity.

## Benefits of decomposing into distributed services

Part of the application can reside in different machines, different rooms, different buildings, different parts of the world.