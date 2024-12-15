# What are the potential costs of decomposition

## Coupling

The different parts of an application cannot work alone. They need to connect with each other somehow in order to solve the problems. For example, one part of the application uses the result from another part. This "connection" is called **coupling**. This basically makes working with one part dependent on the other parts.

Couplings exist, whether the application is decomposed or not, or how granular the decomposition is. The business requirements necessitate a certain of coupling.

When it come to decomposition, the more coupling we have, the less benefit we can get from the decomposition.

<img src="./images/Decomposition - Coupling & Cohesion.png" width="600">
<img src="./images/Decomposition - Coupling.png" width="600">

Two modules are totally independent if each can function completely without the presence of the other. This definition implies that there are no interconnections between the modules - direct or indirect, explicit or implicit, obvious or obscure. This establishes a zero point on the scale of "dependence" (the inverse of independence).

In general, the more interconnections between modules, the less independent they are likely to be. Of course, this is only an approximation; and before we can judge whether more is worse, we must ask whether the various connections between modules are identical, similar, or different. If two modules require six distinct, completely unique connections in order to function together, then they are more highly interconnected than if six connections of the same form would suffice. Similarly, six connections must generally lead to more dependence than three comparable ones. The key question is: How much of one module must be known in order to understand another module? The more that we must know of module B in order to understand module A, the more closely connected A is to B. The fact that we must know something about anothermodule is a priori evidence of some degree of interconnection even if the form of the interconnection is not known.

Unfortunately, the phrase "knowledge required to understand a module" is not very objective: we need an operational method of approximating the degree of interconnection. As we have already suggested, a simple accounting of the number and variety of interconnections between modules is insufficie_nt to fully characterize the influence of the interconnections on the system's modularity. At the very least, we must be able to account for the fact that a long, involved calling sequence that 'interfaces with many internal control variables makes two modules less independent of each other than two equivalent modules with only a few basic input-output parameters passed in the call.

The measure that we are seeking is known as coupling; it is a measure of the strength of interconnection. Thus, "highly coupled" modules are joined by strong interconnections, 'loosely coupled" modules are joined by weak interconnections; "uncoupled" or "decoupled" modules have no interconnections and are, thus, independent. Obviously, what we are striving for is loosely coupled systems - that is, systems in which one can study (or debug, or maintain) any one module without having to know very much about any other modules in the system.

Coupling as an abstract concept - the degree of interdependence between modules -- may be operationalized as the probability that in coding, debugging, or modifying one module, a programmer will have to take into account something about another module. If two modules are highly coupled, then there is a high probability that a programmer trying to modify one of them will have to make a change to the other. Clearly, total systems cost will be strongly influenced by the degree of coupling between modules.

To see how coupling can be an important factor in total systems complexity, consider a system that processes records from a "customer master file"; we would expect such a file to have information about a customer's name, street address, city, state, ZIP code, telephone number, and the various financial or business data with which the system is primarily concerned. Now, suppose that one programmer is assigned the task of writing a module to edit the "telephone number" field within the record - that is to check the ten-digit field to ensure that it does, in fact, consist of all numeric digits, and that the field is nonzero. To "simplify the interfaces" (as several of our students have phrased it), the designer might decide to pass the entire customer record to the TELEPHONE~EDIT module, rather than just the field it requires.

Now for the consequences of such a design: Suppose that Charlie, the programmer who designs and implements the TELEPHONE-EDIT module, is very aggressive and eager to do a good job. It occurs to him that he can do a better job of editing the telephone number by cross-checking the "state" field within the customer record with the "area code" portion of the telephone number. Without telling anyone else in the programming team about this brilliant move (after all, he is writing a black-box module, so why should he have to tell anyone what the module does internally?), he sets up an area code/state code table internally in his module, and uses that to cross-check the telephone number in each customer record.

The first thing that goes wrong is that the TELEPHONE-EDIT module begins rejecting telephone numbers because they don't correlate with the state code - and later analysis shows that the state code was incorrect, not the telephone number! As a result, Charlie inserts a little extra coding to make sure, as best he can, that the state code is reasonable before he attempts to cross-check it with the telephone area code. Meanwhile, the word spreads through the rest of the programming team. Apparently, Charlie has some weird code in his TELEPHONE-EDIT module that does something with the state code."

The coupling aspect of the problem becomes obvious when the user of the system suddenly announces that he wishes to change the state code in the customer record from the standard two-character abbreviation (e.g., NY, TX, and so on) to a full character string representation (e.g., NEW YORK, TEXAS, and so forth). Everyone on the programming team immediately panics: Which parts of the system will be affected?
The point is obvious: In order to comprehend an aspect of the system that, on the surface, has nothing to do with telephone numbers, we must be familiar with Charlie's TELEPHONE-EDIT module. Why? Because, ultimately, Charlie's module was coupled with other modules in the system.

### Coupling Types

#### Data coupling

This is probably the most severe coupling. Modules share data through, for example, parameters or global data.

Sometimes, modules share a composite data structure and use only parts of it, possibly different parts (e.g., passing a whole record to a function that needs only one field of it). In this situation, a modification in a field that a module does not need may lead to changing the way the module reads the record. There's even a term for this: **Stamp coupling**.

#### Control coupling

One part is executed depending on other parts.

#### Subclass coupling (OOP)

Describes the relationship between a child and its parent. The child is connected to its parent, but the parent is not connected to the child.

## Couplings reduce the benefit from decomposition

There more couplings, the less benefit we can get from decomposition. Sometimes, the net benefit can be negative: we're better off reducing the decompotiion granularity. There more couplings, the less benefit we can get from decomposition.

- Cognitive load is not reduced as much, as we need to take into account dependent modules.
- Changes in one part are more likely to necessitate changes in other parts.
- Members/teams must communicate more closely if their modules.
- More difficult to isolate test.

## Coupling with decomposition introduce indirection

We now have indirection. For example, instead of seeing the code inline, we have to call a function and passing in the arguments. To understand what the function does, we need to rely on the function name which can be difficult to understand, misleading even: naming is not easy. So, sometimes, we need to read the documentation, which can also be difficult to understand or even misleading. So, sometimes, to be sure, we have to get to the function to read it. The function definition may locate in a different part of the module, or in a different module, different file, even a different repository.

In event-drivent architecture, asynchronous messaging communication, the communication is not direct and asynchronous.

## Decomposition introduces bad or premature abstraction

This can be both a benefit and a liability.
The abstract can be bad (OOP), premature.

## Reference

- [Coupling (computer science) - Wikipedia](<https://en.wikipedia.org/wiki/Coupling_(computer_programming)>)
- [What Are Abstractions in Software Engineering with Examples](https://thevaluable.dev/abstraction-type-software-example/)
- [Global Variables and States: Why So Much Hate?](https://thevaluable.dev/global-variable-explained/)
- [A Detailed Explanation of The KISS Principle in Software](https://thevaluable.dev/kiss-principle-explained/)
- [The DRY Principle: Benefits and Costs with Examples](https://thevaluable.dev/dry-principle-cost-benefit-example/)
