# Software Decomposition (Modular Programming)

> A well-defined segmentation of the project effort ensures system modularity. Each task forms a separate, distinct program module. At implementation time each module and its inputs and outputs are well-defined, there is no confusion in the intended interface with other system modules. At checkout time the integrity of the module is tested independently; there are few scheduling problems in synchronizing the completion of several tasks before checkout can begin. Finally, the system is maintained in modular fashion; system errors and deficiencies can be traced to specific system modules, thus limiting the scope of detailed error searching.

## What is Software Decompistion
> Decomposition in computer science, also known as factoring, is breaking a complex problem or system into parts that are easier to conceive, understand, program, and maintain. (Wikipedia)

> Structured analysis breaks down a software system from the system context level to system functions and data entities as described by Tom DeMarco. (Wikipedia)

> Object-oriented decomposition, on the other hand, breaks a large system down into progressively smaller classes or objects that are responsible for some part of the problem domain. (Wikipedia)  

Expanded definition: data structure, procedures, blocks.

## What is Modular Programming
> Modular programming is a software design technique that emphasizes separating the functionality of a program into independent, interchangeable modules, such that each contains everything necessary to execute only one aspect of the desired functionality.  
A module interface expresses the elements that are provided and required by the module. The elements defined in the interface are detectable by other modules. The implementation contains the working code that corresponds to the elements declared in the interface. Modular programming is closely related to structured programming and object-oriented programming, all having the same goal of facilitating construction of large software programs and systems by decomposition into smaller pieces, and all originating around the 1960s. While the historical usage of these terms has been inconsistent, "modular programming" now refers to the high-level decomposition of the code of an entire program into pieces: structured programming to the low-level code use of structured control flow, and object-oriented programming to the data use of objects. (Wikipedia)

## Expected Benefits of Modular Programming
The benefits expected of modular programming are:
+ comprehensibility: it should be possible to study the system one module at a time. The whole system can therefore be better designed because it is better understood.
+ product flexibility: it should be possible to make drastic changes to one module without a need to change others
+ managerial: development time should be shortened because separate groups would work on each module with little need for communication

### Information Hiding
+ Prevent use by mistake (not common)
+ Better automatic generation of interfaces documentation 
+ Better IDE suggestions
## Criteria
### Coupling 
A module here refers to a subroutine of any kind, i.e. a set of one or more statements having a name and preferably its own set of variable names.
+ Code coupling (high): one module uses the code of another module, for instance a branch. This violates information hiding – a basic software design concept.
+ Global data coupling: several modules have access to the same global data. But it can lead to uncontrolled error propagation and unforeseen side-effects when changes are made.
+ External coupling
External coupling occurs when two modules share an externally imposed data format, communication protocol, or device interface. This is basically related to the communication to external tools and devices.
+ Control coupling: one module controlling the flow of another, by passing it information on what to do (e.g., passing a what-to-do flag).
+ Data-structured coupling: stamp coupling occurs when modules share a composite data structure and use only parts of it, possibly different parts (e.g., passing a whole record to a function that needs only one field of it).
In this situation, a modification in a field that a module does not need may lead to changing the way the module reads the record.
+ Data coupling: modules share data through, for example, parameters. Each datum is an elementary piece, and these are the only data shared (e.g., passing an integer to a function that computes a square root).
#### Object-oriented programming
+ Subclass coupling: Describes the relationship between a child and its parent. The child is connected to its parent, but the parent is not connected to the child.
+ Temporal coupling: It is when two actions are bundled together into one module just because they happen to occur at the same time.
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
### Intuitiveness

## Reference
[Decomposition (computer science) - Wikipedia](https://en.wikipedia.org/wiki/Decomposition_(computer_science))  
[Modular programming - Wikipedia](https://en.wikipedia.org/wiki/Modular_programming)  
[Coupling (computer science) - Wikipedia](https://en.wikipedia.org/wiki/Coupling_(computer_programming))  
[Cohesion (computer science) - Wikipedia](https://en.wikipedia.org/wiki/Cohesion_(computer_science))  
[Information hiding - Wikipedia](https://en.wikipedia.org/wiki/Information_hiding)  
[Expression_problem - Wikipedia](https://en.wikipedia.org/wiki/Expression_problem)