# Why limiting/reducing software complexity is so hard
It boils down to:
+ It's hard to know what is a good design. There is no simple set of rules. Therefore, it's hard to measure quality of various designs relative to one another.
+ It's hard to measure benefits, with regard to the bottomlines, of a design.
+ It's hard to measure cost (estimation).
Since it's hard to measure, it's hard to manage. Specically, it's hard to incentivize people to aim for good design.
## It's hard to know what is a good design
The first and most important reason is that software design and architecture is a very difficult and complicated subject. Computer science is a huge and difficult field.
An web developer may need to study the following, at least to a certain extent.
+ Operating system
+ Programming languages
+ Data structure and algorithms
+ Software design, architecture
+ The Internet, HTTP, SHH
+ Front end stack: HTML, CSS, JS, frameworks
+ Backend stack: databases (SQL, NoSQL), ORM, framework, security
+ Hosting, virtualization, docker, cloud, devops

There are many architectural patterns to choose from with different infrastructure implications. 

Below that, there's design of various services/modules. There have been many competing programming paradigms (procedural, functional, object-oriented, to name the most common ones). These paradigms have sometimes widely different claims. Many may consider OOP to be the silver bullet for software design, but some consider it to be one of the worst things that ever happened to the software industry. (Personally, I belong more to the latter camp.)

Then, there're problems of specification of the requirement itself, persistency/database design, performance, concurrency, distributed system/microservices, infrastructure. All of them are huge subjects in their own rights.

In addition, an engineer needs to have a good grasp of the requirements and the current source code and have good creativity to be able to devise good designs. These are not small tasks.
### There're probably no hard and fast rule
Even when the study of software design mature in the future, I think there would be no simple set of rules that can be applied to get a good software design.

Instead, an engineer will need apply his/her judgment on a case-by-case basis. He/she will need evaluate cost/benefit of different designs based on time-tested fundamental concepts of software design (e.g. states, cohesion, coupling, abstraction/indirection, et cetera).

Therefore, it's very difficult to derive a simple list of guidelines/best practices. It may even be counter-productive to do so.
### It's hard to measure code complexity
Currently available methods in measuring code complexity are highly inadequate.
### Software engineering education does not focus enough on software design
I have an impression that, currently, the software engineering education is not focusing enough on software design. 

I believe one of significant reasons is the popularity of object-oriented paradigm in both academia and industry. So it makes sense for educational establishment to focus on object-oriented programming. There's not much motivation for them do dig any deeper.
## It's very hard to for various stakeholders to work together effectively
There are various stakeholders influencing the design quality of a complex application.
+ Requirement team
+ UX/UI designers
+ Infrastructure designers
+ Software architects
+ Software development teams (including team leaders, developers)
+ Product owners, project manager
+ Upper management
For these various stakeholders to work together effectively, it's important for them to agree on the costs/benefits of various designs. But due to the reasons discussed above, this is extremely difficult. This have several serious consequences.
### It's very hard to incentivize people
Firstly, it's very hard to incentivize people to limit/reduce code complexity. 

For  a product company, it may be obvious for upper management that, if possible, they should aim for less complexity because they will have to deal with it sooner or later. There're even research on effect of code complexity to the bottomline, so management can be convinced. However, how much effort should be spent is not so obvious. And because it's hard to measure, it's hard to manage. All the more reason for management to let go of code quality management.

From a outsourcing company's perspective, however, it may not make sense for them to focus on design. It's hard for a customer to compare quote quality of different vendors, so they won't be able to reward adequately. Rather, they will probably focus on some acceptance tests, time and cost. Also, The customer is also unclear about how much effort that should be spent (same as above). The vendor, in turn will focus on short term gains, just passing acceptance tests and get the money, not on design or code cleanliness.

Perversely, there is even motivation for them to do the opposite. It probably makes business sense for vendors to make customer dependent on them. So, if they make the source code complex, if the customers choose other vendors, those vendors will have a hard time working with the source code and may not do a good job. Conversely, if the original vendor spends more resources to make the code more understandale, later vendors will finish the job with less resources than the previous case. The customer may then think this is due to the later vendors' better capability. This is especially true when duration of the contract/project is short.

The same logic applies to team/people down the hierarchy. From a team leader's perspective, for example, if he/she sacrifice other performance indices to make the design of team's modules better, upper management may not reward that adequately. If that modules are later transferred to other teams. Then this other team will reap the benefits of good code quality. 

It's similar from individual developer's perspective. No one want to be (seemingly) easily replacable. 

Of course, it goes without saying that I'm not advocating for this; I just want to point out the perversion of incentives here.

Another problem is that instead of finding the design solutions best suited to the problems, sometimes developers tends to over-engineer their solutions, i.e. using design pattern/technologies more complicated than optimal. Majorirty of developers want to improve their skills, and try new design ideas which they do think are good. This is mostly  done subconciously. 

I strongly believe that many developers do have intrinsic motivation to study and aim for good design. Some want to create real values. Many want to be proud of the code. Ego is a thing. Some are simply 'allergic' to bad code. However, systematically, engineers does not have incentives to study software design, especially paradigms that are not trendy. They may have an impression that object-oriented design and its various design patterns are good enough. 
### Common code quality management methods are ineffective
Common code quality management methods are as followed:
+ Various tests: static test, functional test, performance test
+ Design documentation
+ Design reviews
These methods does help to improve code quality greatly, but in my opinion, far from adequate.

Firstly, various tests help to ensure correctness and performance of the software. This in tun incentivize various stakeholders to aim for good design to a certain extent, especially at the beginning of the development phase, as bad design will hamper their effort later on the development phase. However, test effectiveness is quite limited, even in ensuring the software's correctness. 

Test does not measure code quality, except maybe some static test. Static test can help ensure the source code conforming to certain coding conventions. Their effects are very limited.

The requirement for design documentation together with design review are probably effective to a certain extent. 
+ The requirement to document their design may make developers think carefully about their design. But this is limited by the developers' design knowlege, creativity and motivation.
There may be rules preventing developers from modifying the high-level design on a whim. But this assumes the high-level design is good, and that the reviewers are good.
+ It takes time from developers, reviewers to make and review the documentation. The resrouces need to spent on auditing, to make sure that developers/reviewers do what required of them. These resources may be better spent on the design itself. 
When there is not enough time, developers and reviewers will do a sloppy job. They may not aim for better design. Or the documentation does not reflect the design accurately. 
+ I've worked on projects where the source code is a spaghetti mess, but the design documentation does not reflect that. This had been the situation for many years. No one bothers to correct it anymore. To make documentation reflect the source code accurately, the efforts needed is inimaginable.
+ Auditors (if any) do not understand the source code well enough to judge the correctness of documentation.

I have worked in projects where comprehesive documentation are required and projects where not much is done in terms of documentation. Difference in effort spent on documentation is significant but difference in code quality is not obvious.

In one such project, I've seen a misunderstanding of the requirement still passes through various design phases' reviews and straight to code.
### It's hard to manage quantity, delivery and quality at the same time
Agile

### Management tend to follow trends: oop, microservices

### It's hard to reach concencus
These are especially hard if the one giving design advice is not of high authority/reputation/title. Experience does not mean better design thinking. //todo: add link

It's even hard for different developers in a same team to reach consensus. It's even harder for leaders (especially business ones) to select engineers with good design skills, especially when good engineers are costly. 

It's very hard to convince people on the business/management side of things. It may be easy to convince a business person the benefit of code readability in a general sense as there are research on the effect of readability (or lack of it) on the bottom-line. However, it's a whole different story when it get downs to the specifics. It's probably very hard to discuss merits and cost of a specific refactoring idea.

Even good technical leaders cannot manage deep below the chain. There will be impedance across the chain. Only the engineers who directly manage the module will have a good understanding of it.
## Refactoring (after development) is also harder
Refactoring is also hard, sometimes even harder. In addition to the above difficulties, for the case of refactoring:
+ It's even harder to convince other engineers about the ill-designed aspects of their already done code.
+ It is risky and takes further resources, without obvious benefits (i.e things like new features, better performance).
+ Measuring/judging its effectiveness and values is difficult.
## Some personal experience
I've had many refactoring/design ideas during my career that I believed can improve the codebase significantly.
+ Almost none of those are derived out of requests from my leaders/managers.
+ Some of those are refused by others without good counter-arguments.
+ Most of those are left untouched, as there is no time.
+ Some of those, I did out of my own volution, occasionally out of my own time.
+ I often refactored while fixing some bugs or adding some new features.
+ Many times I thought it would save time and effort to refactor the related code. And more often than not, that thought turned out to be the case.
+ Sometimes, after the refactoring, a previously hard-to-understand bug might become clearer or even disappear without any further fixing!
+ I did want to try out my design idea, but in retrospect, those refactoring are worth it.