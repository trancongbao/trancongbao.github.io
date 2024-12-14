Distributed-services architecture almost always comes hand-in-hand with multi-databases architecture and multi-repo versioning strategy.

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

## Costs of Multi-Repo

### Higher barriers of entry

When new staff members start working for a company, they need to download the code and install the required tools to begin working on their tasks. Suppose the project is scattered across many repositories, each having its installation instructions and tooling required. In that case, the initial setup will be complex, and more often than not, the documentation will not be complete, requiring these new team members to reach out to colleagues for help.

A monorepo simplifies matters. Since there is a single location containing all code and documentation, you can streamline the initial setup.

### Painful application-wide refactorings

When creating an application-wide refactoring of the code, multiple libraries will be affected. If you’re hosting them via multiple repositories, managing all the different pull requests to keep them synchronized with each other can prove to be a challenge.

A monorepo makes it easy to perform all modifications to all code for all libraries and submit it under a single pull request.

### Libraries must constantly be re-synced

When a new version of a library containing breaking changes is released, libraries depending on this library will need to be adapted to start using the latest version. If the release cycle of the library is faster than that of its dependent libraries, they could quickly become out of sync with each other.

Teams will need to constantly catch up to use the latest releases from other teams. Given that different teams have different priorities, this may sometimes prove arduous to achieve.

Consequently, a team not able to catch up may end up sticking to the outdated version of the depended-upon library. This outcome will have implications on the application (in terms of security, speed, and other considerations), and the gap in development across libraries may only get wider.

## Merge conflict

A good design with less coupling could reduce merge conflict.

## Reference

- [Monorepo vs Multi-Repo](https://kinsta.com/blog/monorepo-vs-multi-repo/)
