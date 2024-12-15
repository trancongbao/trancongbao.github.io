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

### Factors that influence coupling
Four major aspects of computer systems can increase or decrease intermodular coupling. In order of estimated magnitude of their effect on coupling, these are
- Type of connection between modules. So-called minimally connected systems have the lowest coupling, and normally connected systems have
lower coupling than those with pathological connections.
- Complexity of the interface. This is approximately equal to the number of different items being passed (not the amount of data) - the more
items, the higher the coupling.
- Type of information flow along the connection. Data-coupled systems have lower coupling than control-coupled systems, which have lower
coupling than hybrid-coupled systems.
- Binding time of the connection. Connections bound to fixed referents at execution time result in lower coupling than binding that takes place at loading time, which results in lower coupling than binding that takes place at linkage-edit time, which in turn results in lower coupling than binding that takes place at compilation (or assembly) time - all of which result in still lower coupling than binding that takes place at coding time.

Each of these is important and is discussed separately below.
#### Type of connection between modules
Recall that a connection in a program is a reference by one element to the name, address, or identifier of another element. An intermodular connection occurs when the referenced element is in a different module from the referencing element. Any such referenced element defines an interface, a portion of the module boundary across which data or control flow. The interface may be regarded as residing at the referenced element~ you may think of it as a socket into which the plug, represented by the connection from the referencing module, is inserted. Every interface in a module represents one more thing which is/must be known, understood, and properly connected by other modules in the system.

Clearly, we want to minimize systems/module complexity in part by minimizing the number (and variety) of interfaces per module. We already know that each module must have at least one interface to be uniquely defined and to be tied into a system.
But is a single identity interface sufficient to implement real functioning systems? The key question here is: What purpose do interfaces serve? In programs, they can only serve a limited variety of functional purposes. Only control and data can be passed among modules in a programming system. An interface can serve to transmit data into a module (as input parameters), or out of the module (as output results). It can be a name by which control is received or transmitted. Only these four generic capabilities are required. Any scheme which provides interfaces for all four must, by definition, be sufficient to realize all programmable systems.

By a judicious choice of conventions, we will be able to have a single interface per module serve all four purposes. First, we associate the identity interface of the module with its entry or activation interface~ that is, a single unique entry interface serves not only to receive control, but to identify the module. We also can transmit data to the module without adding interfaces by making the entry/identity interface capable of accepting data as well as control. This requires that elements of data be passed dynamically as arguments (parameters) as part of the activation sequence, which gives control to a module; any static reference to data would introduce new interfaces.

With respect to any two modules, say A and B, we have determined that the following familiar structure is sufficient to get control and data from A into B:

Unfortunately, we cannot use the same approach to get control from B to A, as that would define a system with more than the minimal number of interconnections between modules. We need the identity interface of B to serve as a path for control to be received by A, as transmitted by B; this is a "return'' of control to A. We can accomplish this by having the control transfer from A to B be a conditioned transfer. B will thus be able to return implicitly to A (or any other activating module) without the introduction of additional interfaces.

This also suggests a mechanism for transmitting data from B back to A without adding extra interfaces: We may associate a value with the particular activation of B, and use this contextually in A (e.g., by making B a logical function, as we did in the SCAN example in Chapter 5). Alternatively, we can transmit to B parameters that define locations for return of results to A.

If all connections of a system are restricted to fully parameterized (with respect to inputs and outputs) conditioned transfers of control to the single, unique activation/entryI origin/identity interface of any module, then the system is termed minimally connected. A minimally connected structure has the lowest number of interconnections and interfaces needed to define bidirectional control and information transfer between communicating modules.

It is important to realize that minimally connected structures are minimal in a fundamental sense, and yet are sufficient for the realization of all actual program functions. Minimally connected modules require the least knowledge of discrete, internal features of the module. In addition, such systems have simple, Bnormal" behavior since the entire data context of a module and its precise return are established and guaranteed by the activating module. The pattern of control transfers into and out of modules must define a symmetric, fully nested set, and all transfers must strictly follow the hierarchical lines so established.

Other control relationships can be admitted which, while not satisfying the requirements for minimal connectedness, still preserve the normal behavior of minimally
connected systems. We shall call a system normally connected if it is minimally connected, except for one or more instances of the following:
- There is more than one entry point to a single module, provided that each such entry is minimal with respect to data transfers.
- Control returns to other than the next sequential statement in the activating module, provided that alternate returns are defined by the activating module as part of its activation process.
- Control is transferred to a normal entry point by something other than a conditioned transfer of control.

Use of multiple entry points to a module guarantees that there will be more than the minimum number of interconnections for the system. On the other hand, if each entry point still functions as a minimal (fully parameterized, conditioned transfer) connection as far as other modules are concerned, the behavior of the system should be every bit as normal as if minimally connected. We note, however, that the presence of multiple entry points suggests that the module is carrying out multiple functions. Furthermore, there is an excellent chance that the programi:ner will partially overlap the code for each of the functions~ this means that the functions within the multiple-entrypoint module will be content-coupled (a concept discussed in Section 6.1.3). However, this can be regarded as an issue separate from that of using multiple-entry-point modules to build normally connected systems.

In a simittar vein, alternate returns are frequently useful and are within the spirit of normally connected systems. Frequently, a subordinate module wishes to return binary or three-valued results to its superordinate - binary results representing the outcome of decisions in the subordinate. Minimal connectedness would require returning the outcome of such decisions as a datum (e.g., a parameter) to be retested in the superordinate. However, control characteristics would still be simple and predictable if the superordinate module specifies one or more alternate return locations - one of which must be taken by the subordinate upon completion of its processing. Depending on the programming language, the designer can usually provide for alternate returns by specifying a 4 'relative return" (i.e., a return to calling address + 1, to calling address + 2, and so on), or an "alternate return parameter" (where the address of a return location in the superordinate is passed to the subordinate).

If a system is not minimally connected or normally connected, then some of its modules must have pathological connections. That is, at least some of the modules must make unconditioned transfers of control to labels within the boundaries of other modules, or they must make explicit references to data elements outside their own module boundaries. All such situations increase the coupling of the system by increasing the amount that we must know about the 'outside world' in order to understand how any one module works. All other things being equal~ then, coupling is minimized in a minimally connected system~ it is likely to be slightly higher with a normally connected system and much higher with pathological connections. The subject of pathological" connections is so important that all of Chapter 13 is devoted to it.

#### Complexity of the interface
The second dimension of coupling is complexity. The more complex a single connection is, the higher the coupling. This dimension is necessary to account for the effect of a normal subroutine call with 134 parameters specified as opposed to a call involving the specification of only two parameters.

By "complexity" we mean complexity in human terms, as discussed in Chapter 5. There are various ways to approximate the complexity of an interface, though none is perfect. One simple method, for example, is to count the number of characters in the statement (s) involved in the connection between two modules. Obviously, this is a very rough approximation, since making any consistent substitution of identifiers throughout the program could increase or decrease the character count in the appropriate statements without actually affecting their complexity.

A better approximation can be achieved by counting the number of discrete symbols or "language tokens" involved in the interface - that is, names, vocabulary words, variables, punctuation, and so on. In simple ·terms, then, we would expect that a subroutine-calling interface with 134 arguments in the parameter list would involve more coupling than an interface with only two parameters

#### Information flow
Another important aspect of coupling has to do with the type of information that is transmitted between superordinate and subordinate~ the kinds of information we distinguish are data, control, and a special hybrid of data and control. Information that constitutes data is that which is operated upon, manipulated, or changed by a piece of program. Control information (even when represented by a "data variable") is that which governs how the operations upon or manipulations of other information (the data) will take place.

It can be shown that the communication of data alone is necessary for functioning systems of modules. Control communication represents a dispensable addition found in most, but not necessarily all, computer programs. Coupling is, therefore, minimized (all other things being equal, of course) when only input data and output data flow across the interface between two modules. A connection establishes input-output coupling, or data-coupling, if it provides output data from one module that serves as input data to the other. Not all connections which appear to move data are necessarily of this type: The data might be a flag used to control certain aspects of the execution of the other module, or it might be a "branch-address" to be used if certain conditions arise. These are elements of control disguised as data.

We should emphasize that input-output coupling bears no relationship to inputoutput devices. Disks, tapes, and other peripheral devices may or may not mediate the connection. What is essential is the purpose the connection serves. 

Input-output coupling is minimal, because no system can function without it. Modules cannot function as a single system performing an overall purpose, unless the outputs of some modules become the inputs of others. Moreover, any system can be constructed in such a way that the only coupling is input-output coupling. The inescapable conclusion is that all communication of control not only is extraneous, but also introduces needless additional coupling

It is easy to see, at a high level, how a system could be constructed with only input-output coupling. Consider, for example, an application involving four "transforms" to be applied to a stream of data consisting of student names, in alphabetical order; associated with each student record is a list of other students (presumably from the same educational institution) that he/she likes best. The first transform involves splitting the stream of data into two separate "substreams" one substream consists of the student's name (and other biographical data), and the other substream consists of the names that the student has nominated as favorites. The second transform involves performing some computations on the first substream of student names. The third transform involves sorting the second substream into alphabetical order - those people who have been named as favorites. The fourth and firial transform is to produce a combined report that lists a student, appropriate biographical information (with the results of the computations performed by the second transform), and a list of all those who named him as a favorite.

The input-output flow, or data flow, structure of this problem is shown in Fig. 6.1. If we have enough equipment lying around, we can program this as four fully independent programs, each of which reads inputs from paper tape and punches output on paper tape. Assuming that the paper tape readers have interlocks to prevent the tape from tearing, we could load these machines in the manner shown in Fig. 6.2, and start all four running. That we have achieved parallel processing is not the central point; what is important is that we have succeeded in constructing a system that is only inputoutput coupled (you should be able to see that we can always do this), and it consists of maximally independent modules - no control information is being passed. Q.E.D.! We will return to this topic, exploring it in terms of more elementary modules, in Chapter 18.

In discussing input-output coupling, we noted that communication of elements of control represented a stronger (and, therefore, less desirable) form of coupling. Since control-coupling is nonessential, any system that includes it must consist of less independent modules (other things being equal, of course!). Control-coupling covers all forms of connection that communicate elements of control. This may involve actual transfer of control (e.g., activation of modules), or it may involve the passing of data that change, regulate, or synchronize the target module (or serve to do the same for the originating module).

Such nsecondary" or indirect control is termed ·coordination. Coordination involves one module in the procedural contents of another; this may not be obvious in the abstract, but it should be clear in an example. For instance, a subroutine that assembles successive elements of data into compound elements for the superordinate may send a flag to the superordinate indicating whether its return is to request an additional data element or to deliver a completed compound item. The superordinate must contain a decision (in this case, binary in nature), which relates to an internal task of the subordinate module that assembles items (namely: Is the item assembled?). This involvement in the internal activities of another module means that coordinating controlcoupling is stronger (and, therefore, less desirable) than "activating" control-coupling.

The function of data and control sometimes may be even more confused than in coordinating control-coupling. When one module modifies the procedural contents of another module, we have hybrid-coupling. Hybrid-coupling is simply intermodular statement modification. To the target (modified) module, the connection functions as control; to the modifying module, it functions as data.

The degree of module interdependence associated with hybrid-coupling is clearly very strong, since the very function of the target module can be changed. Moreover, any modification or recoding of either the source or target module may affect the other
by an extreme, even disastrous, amount. A change in the target module may eliminate or shift the label of the statement being modified, resulting in modification of the wrong statement~ similarly, changes in the source module, which are not based on full
analysis of the possible consequences for the target module, can cause it to malfunction in mysterious ways. Fortunately, using hybrid-coupling is a practice that is declining except among systems programmers and those involved in assembly language programming on minicomputers or microcomputers.

Experience has shown that direct modification of data operands, whether intermodular or intramodular, is less serious than modification of programming statements. This seems to affect hybrid-coupling as well.

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
