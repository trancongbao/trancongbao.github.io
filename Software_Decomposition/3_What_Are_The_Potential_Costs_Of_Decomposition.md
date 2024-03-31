# What are the potential costs of decomposition

<img src="./images/Decomposition%20-%20Coupling.png" width="600">

## Coupling

The different parts of an application cannot work alone. They still need to connect with each other somehow in order to solve the original problems. This "connection" is called **coupling**.
Even though there will always be some degree of coupling between parts, different designs can introduce different degree of coupling. And higher the degree of coupling is, the worse the design.

## Indirection

## Abstraction

## Coupling

## Costs of Multi-Repo

## Higher barriers of entry

When new staff members start working for a company, they need to download the code and install the required tools to begin working on their tasks. Suppose the project is scattered across many repositories, each having its installation instructions and tooling required. In that case, the initial setup will be complex, and more often than not, the documentation will not be complete, requiring these new team members to reach out to colleagues for help.

A monorepo simplifies matters. Since there is a single location containing all code and documentation, you can streamline the initial setup.

## Painful application-wide refactorings

When creating an application-wide refactoring of the code, multiple libraries will be affected. If you’re hosting them via multiple repositories, managing all the different pull requests to keep them synchronized with each other can prove to be a challenge.

A monorepo makes it easy to perform all modifications to all code for all libraries and submit it under a single pull request.

## Libraries must constantly be re-synced

When a new version of a library containing breaking changes is released, libraries depending on this library will need to be adapted to start using the latest version. If the release cycle of the library is faster than that of its dependent libraries, they could quickly become out of sync with each other.

Teams will need to constantly catch up to use the latest releases from other teams. Given that different teams have different priorities, this may sometimes prove arduous to achieve.

Consequently, a team not able to catch up may end up sticking to the outdated version of the depended-upon library. This outcome will have implications on the application (in terms of security, speed, and other considerations), and the gap in development across libraries may only get wider.

## May fragment teams

When different teams don’t need to interact, they may work in their own silos. In the long term, this could result in teams producing their subcultures within the company, such as employing different methodologies of programming or management or utilizing different sets of development tools.

If some team member eventually needs to work in a different team, they may suffer a bit of culture shock and learn a new way of doing their job.