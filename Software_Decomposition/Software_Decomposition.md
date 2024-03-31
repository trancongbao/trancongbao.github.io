# Software Decomposition

> A well-defined segmentation of the project effort ensures system modularity. Each task forms a separate, distinct program module. At implementation time each module and its inputs and outputs are well-defined, there is no confusion in the intended interface with other system modules. At checkout time the integrity of the module is tested independently; there are few scheduling problems in synchronizing the completion of several tasks before checkout can begin. Finally, the system is maintained in modular fashion; system errors and deficiencies can be traced to specific system modules, thus limiting the scope of detailed error searching.

[1. What is software decomposition?](./1_What_Is_Software_Decomposition.md)

[2. What are the potential benefits of decomposition?](./2_What_Are_Potential_Benefits_Of_Decomposition.md)

[3. What are the potential costs of decomposition?](./3_What_Are_The_Potential_Costs_Of_Decomposition.md)

## Criteria for good decomposition

Good decomposition means the net benefit is positive (opportunity cost).

### Cohesion
#### Distance between parts

Logic: block -> function -> class -> package -> service
Data: piece of primitive data -> struct/table/class -> package -> service
Peristent data storage: row -> table -> database -> database server

<img src="./images/Decomposition - Cohesion - Types.png" width="600">

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
