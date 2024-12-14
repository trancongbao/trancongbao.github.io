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

## Process and network decomposition

Apart from logical decomposition, application can be decomposed into multiple processes, and these multiple processes can live in different machines.

### An application can be seperated into multiple processes

<img src="./images/Decomposition%20-%20IPC.png" width="600">

### An application's processes can be separated into multiple distributed services

<img src="./images/Decomposition%20-%20Virtualization.webp" width="600">
<img src="./images/Decomposition%20-%20Containers.png" width="600">

### An application's distributed services can be separated into different machines

<img src="./images/Decomposition%20-%20Distributed%20System.png" width="600">
<img src="./images/Decomposition%20-%20Client-Server.webp" width="600">

### Different databases can lives in different database servers
Microservice architecture advocates for breaking one big monolith database into multiple databases in in different servers: each service has its own database (server).