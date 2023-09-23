# How to approach software design/refactoring
## Documentation
### Requirement documentation
+ Requirement documentation is very important.
+ Comprehensive requirement documentation at the beginning of a project/sprint is probably inefficient.
+ Comprehensive requirement documentation at the end sprint is a must.
### Architecture/API documentation
+ Architecture design documentation that show relationship between various module/app/service is important.
+ API (including module-app level) documentation of each module/app/service is important.
+ Purpose: for collaboration across team, conflict resolution.
### Module Design document
Not as important, especially detailed design (flowchart,...)
Become more important if the module become bigger, more complex.
### Database schema documentation
+ Relational database: Comments in Django model class may be sufficient.
+ NoSQL: //todo
## Single source of truth
Above documentation should be at a single source.
## Good architects is a must
But I don't know how to select them. The only way may be to base on their previous projects. 
## How to Approach Design (during development)
+ It's difficult to have a good comprehensive design before implementation. Requirements may change. Research, trials may need to be done.
+ Focus on design during development may negatively affect speed of development.
+ It's difficult to manage both speed of development and code quality. 
+ We should focus on high-level architecture (cross module/app/service), instead of detail design. We may need to have review of this.
+ The rest should probably be left to refactoring later. 
## How to Approach Refactoring (after development)
+ Find the modules that should be refactored first (based on the amount of bugs, performance issues, planned decks, etc.).
+ Find an engineer with good design/refactoring knowledge (prerequisite). It's a great bonus if he/she already possesses knowledge of the system/technologies.
+ Place the refactoring engineer inside a Production team who is currently handling the modules.
+ With support from members of the Production team, the refactoring engineer will try to understand the modules' source code. Then, he/she will try to find refactoring ideas and the team will review those ideas that are high-risked/requiring lots of efforts. Or maybe even a better approach is that the team themselves find the refactoring ideas and the refactoring engineer reviews them.
+ Then, we plan the refactoring ideas together with new features/bug fixes (to reduce risks and efforts). This should probably involve other stakeholders.
+ Then, either the refactoring engineer will carry out the refactoring and the Production team will review the refactored code or vice versa, or they can do it together.
+ The refactoring should be done step by step. 

It is less risky this way. And after initial refactoring, the source code will become easier to understand; bigger refactoring can be done more easily then. Even a single-line of code is worth it. A disadvantage of this approach may be that a bigger refactoring later may render the previous small refactoring ''meaningless".

+ Then, we move to other modules/teams.

### Select and support refactoring engineer
For one to do well at this job, I think the followings are necessary.
+ He/she must have good design/refactoring knowledge.
+ He/she must have a good understanding of the technologies involved and the modules to be refactored.
+ He/she should have good communication skills to convince various stakeholders.
and also,
+ He/she must have the trust of the various stakeholders, especially the developers whose code is being refactored.
+ The support from management.