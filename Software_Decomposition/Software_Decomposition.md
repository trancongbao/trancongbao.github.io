# Software Decomposition

> A well-defined segmentation of the project effort ensures system modularity. Each task forms a separate, distinct program module. At implementation time each module and its inputs and outputs are well-defined, there is no confusion in the intended interface with other system modules. At checkout time the integrity of the module is tested independently; there are few scheduling problems in synchronizing the completion of several tasks before checkout can begin. Finally, the system is maintained in modular fashion; system errors and deficiencies can be traced to specific system modules, thus limiting the scope of detailed error searching.

[1. What is software decomposition?](./1_What_Is_Software_Decomposition.md)

[2. What are the potential benefits of decomposition?](./2_What_Are_Potential_Benefits_Of_Decomposition.md)

[3. What are the potential costs of decomposition?](./3_What_Are_The_Potential_Costs_Of_Decomposition.md)

## Criteria for good decomposition

Good decomposition means the net benefit is positive (opportunity cost).

### Coupling

<img src="./images/Decomposition%20-%20Coupling%20&%20Cohesion.png" width="600">

- Code coupling (high): one module uses the code of another module, for instance a branch. This violates information hiding – a basic software design concept.
- Global data coupling: several modules have access to the same global data. But it can lead to uncontrolled error propagation and unforeseen side effects when changes are made.
- External coupling
  External coupling occurs when two modules share an externally imposed data format, communication protocol, or device interface. This is basically related to the communication to external tools and devices.
- Control coupling: one module controlling the flow of another, by passing it information on what to do (e.g., passing a what-to-do flag).
- Data-structured coupling: stamp coupling occurs when modules share a composite data structure and use only parts of it, possibly different parts (e.g., passing a whole record to a function that needs only one field of it).
  In this situation, a modification in a field that a module does not need may lead to changing the way the module reads the record.
- Data coupling: modules share data through, for example, parameters. Each datum is an elementary piece, and these are the only data shared (e.g., passing an integer to a function that computes a square root).

#### Object-oriented programming

- Subclass coupling: Describes the relationship between a child and its parent. The child is connected to its parent, but the parent is not connected to the child.
- Temporal coupling: It is when two actions are bundled together into one module just because they happen to occur at the same time.
  In recent work various other coupling concepts have been investigated and used as indicators for different modularization principles used in practice.

#### Monolithic coupling

##### Versioning coupling

One problem with so many developers committing to the same code base is that the build is frequently in an unreleasable state. Trying to solve this problem by using feature branches can result in lengthy, painful merges. Consequently, once a team completes its sprint, a long period of testing and code stabilization follows.

##### IDE coupling

Big code base can slow down the IDE, making developers less productive.

##### Build coupling

##### Startup coupling

Edit-build-run-test loop takes a long time, which badly impact productivity.

##### Resource coupling

A bug in one module—for example, a memory leak—crashes all instances of the application, one by one.
Different application modules have conflicting resource requirements. The restaurant data, for example, is stored in a large, in-memory database, which is ideally deployed on servers with lots of memory. In contrast, the image processing module is CPU intensive and best deployed on servers with lots of CPU. If these modules are part of the same application, FTGO must compromise on the server configuration.

##### Technology stack coupling

The monolithic architecture makes it difficult to adopt new frameworks and languages. It would be extremely expensive and risky to rewrite the entire monolithic application so that it would use a new and presumably better technology. Consequently, developers are stuck with the technology choices they made at the start of the project. Quite often, they must maintain an application written using an increasingly obsolete technology stack.

##### Database schema coupling

### Cohesion
#### Distance between parts

Logic: block -> function -> class -> package -> service
Data: piece of primitive data -> struct/table/class -> package -> service
Peristent data storage: row -> table -> database -> database server

### Intuitiveness

## Decomposition techniques

### Functional decomposition

Functional decomposition is a software design technique in which a complex system is broken down into smaller, more manageable parts, or modules, based on their functionality or behavior. Each module represents a specific function or task within the system, and is designed to operate independently of other modules.

Functional decomposition is commonly used in object-oriented programming and structured programming paradigms. In object-oriented programming, each module is implemented as a class that encapsulates a specific set of functionality. In structured programming, each module is implemented as a function or procedure that performs a specific task.

### Business capability decomposition

Decompose by business capability is a decomposition technique that involves breaking down a software system based on the business capabilities or functions it provides. In other words, the system is divided into smaller components based on the specific business capabilities they support, such as sales, customer service, inventory management, or accounting.

## Related terms

- Divide and Conquer
- Separation of Concerns
- Modular Programming
- Granularity

### Modular programming

> A modularized application may or may not be modular.

> **Modular programming** is a software design technique that emphasizes separating the functionality of a program into independent, interchangeable **modules**, such that each contains everything necessary to execute only one aspect of the desired functionality.  
> A module **interface** expresses the elements that are provided and required by the module. The elements defined in the interface are detectable by other modules. The **implementation** contains the working code that corresponds to the elements declared in the interface. (Wikipedia)

### Information hiding

- Prevent use by mistake (not common)
- Better automatic generation of interfaces documentation
- Better IDE suggestions

## Reference

[Decomposition (computer science) - Wikipedia](<https://en.wikipedia.org/wiki/Decomposition_(computer_science)>)  
[Modular programming - Wikipedia](https://en.wikipedia.org/wiki/Modular_programming)  
[Coupling (computer science) - Wikipedia](<https://en.wikipedia.org/wiki/Coupling_(computer_programming)>)  
[Cohesion (computer science) - Wikipedia](<https://en.wikipedia.org/wiki/Cohesion_(computer_science)>)  
[Information hiding - Wikipedia](https://en.wikipedia.org/wiki/Information_hiding)  
[Expression_problem - Wikipedia](https://en.wikipedia.org/wiki/Expression_problem)  
[How to organize your code (Blog)](https://kislayverma.com/programming/how-to-organize-your-code)  
[Decomposition in Software Testing](https://trailheadtechnology.com/decomposition-in-software-testing/)  
[Monorepo vs Multi-Repo](https://kinsta.com/blog/monorepo-vs-multi-repo/)
