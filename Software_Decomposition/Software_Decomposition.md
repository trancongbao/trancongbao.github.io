# Software Decomposition

> A well-defined segmentation of the project effort ensures system modularity. Each task forms a separate, distinct program module. At implementation time each module and its inputs and outputs are well-defined, there is no confusion in the intended interface with other system modules. At checkout time the integrity of the module is tested independently; there are few scheduling problems in synchronizing the completion of several tasks before checkout can begin. Finally, the system is maintained in modular fashion; system errors and deficiencies can be traced to specific system modules, thus limiting the scope of detailed error searching.

[What_Is_Software_Decomposition](./What_Is_Software_Decomposition.md)

## What is software decomposition

> Decomposition in computer science, also known as factoring, is breaking a complex problem or system into parts that are easier to conceive, understand, program, and maintain. (Wikipedia)

> Structured analysis breaks down a software system from the system context level to system functions and data entities as described by Tom DeMarco. (Wikipedia)

> Object-oriented decomposition, on the other hand, breaks a large system down into progressively smaller classes or objects that are responsible for some part of the problem domain. (Wikipedia)

### Architecture & the 4+1 architecture view model

There are numerous definitions of software architecture. For example, see https://en.wikiquote.org/wiki/Software_architecture to read some of them. My favorite definition comes from Len Bass and colleagues at the Software Engineering Institute (www.sei.cmu.edu), who played a key role in establishing software architecture as a discipline. They define software architecture as follows:

> The software architecture of a computing system is the set of structures needed to reason about the system, which comprise software elements, relations among them, and properties of both. (Documenting Software Architectures by Bass et al.)

That’s obviously a quite abstract definition. But its essence is that an application’s architecture is its **decomposition** into parts (the **elements**) and the relationships (the **relations**) between those parts.

Decomposition is important for a couple of reasons:

- It facilitates the division of labor and knowledge. It enables multiple people (or multiple teams) with possibly specialized knowledge to work productively together on an application.
- It defines how the software elements interact.

It’s the decomposition into parts and the relationships between those parts that determine the application’s -ilities.

> In terms of logic, there is a spectrum from code -> block -> function -> package -> service. In terms of data, there is a spectrum from one piece of primitive data -> array/map/struct -> complex composite -> package -> service. In terms of persistent data storage, the is a spectrum from row -> table -> database -> database server.  
> In terms of design quality, there is a spectrum from code quality -> design quality -> architecture quality.

The design quality of an application can basically be determined from the design quality of each top-level parts and the degree of coupling between these top-level parts. The top-level

- The quality of decomposition is determined by two factors: cohesion and coupling.
- The quality of each parts the degree of coupling in the system is one of the primary indicators of the quality of the decomposition. The other indicators include cohesion, and obviously the quality of the different parts (e.g. if you choose MongoDB as your no-sql databases, ).

#### The 4+1 view model of software architecture

More concretely, an application’s architecture can be viewed from multiple perspectives, in the same way that a building’s architecture can be viewed from structural, plumbing, electrical, and other perspectives. Phillip Krutchen wrote a classic paper describing the 4+1 view model of software architecture, “Architectural Blueprints—The ‘4+1’ View Model of Software Architecture” (www.cs.ubc.ca/~gregor/teaching/papers/4+1view-architecture.pdf).
The 4+1 model defines four different views of a software architecture. Each describes a particular aspect of the architecture and consists of a particular set of software elements and relationships between them.
<img src="./images/Decomposition - Architecture.png" width="600">

The purpose of each view is as follows:

- **Logical view**— The software elements that are created by developers. In object-oriented languages, these elements are classes and packages. The relations between them are the relationships between classes and packages, including inheritance, associations, and depends-on.
- **Implementation view**— The output of the build system. This view consists of modules, which represent packaged code, and components, which are executable or deployable units consisting of one or more modules. In Java, a module is a JAR file, and a component is typically a WAR file or an executable JAR file. The relations between them include dependency relationships between modules and composition relationships between components and modules.
- **Process view**— The components at runtime. Each element is a process, and the relations between processes represent interprocess communication.
- **Deployment view**— How the processes are mapped to machines. The elements in this view consist of (physical or virtual) machines and the processes. The relations between machines represent networking. This view also describes the relationship between processes and machines.

In addition to these four views, there are the **scenarios**—the +1 in the 4+1 model—that animate views. Each scenario describes how the various architectural components within a particular view collaborate in order to handle a request. A scenario in the logical view, for example, shows how the classes collaborate. Similarly, a scenario in the process view shows how the processes collaborate.

### Logical decomposition

A program can be thought of, logically, as containing data (states) and logic.

##### Logic can be decomposed into blocks

```C
// C Blocks
// Static variables representing account balances
static double balance1 = 200.0;
static double balance2 = 300.0;

void bankSimulation(double withdrawalAmount, double depositAmount) {
    // Withdrawal operation from balance1
    {
        if (balance1 >= withdrawalAmount) {
            balance1 -= withdrawalAmount;
            printf("Withdrawn $%.2f from Account 1\n", withdrawalAmount);
        } else {
            printf("Insufficient funds for withdrawal from Account 1.\n");
        }
    }

    // Deposit operation into balance2
    {
        balance2 += depositAmount;
        printf("Deposited $%.2f into Account 2\n", depositAmount);
    }
}
```

```kotlin
// Kotlin Scope Functions
val hexNumberRegex = run {
    val digits = "0-9"
    val hexDigits = "A-Fa-f"
    val sign = "+-"

    Regex("[$sign]?[$digits$hexDigits]+")
}

for (match in hexNumberRegex.findAll("+123 -FFFF !%*& 88 XYZ")) {
    println(match.value)
}
```

```go
// Golang Blocks
v := "outer"
fmt.Println(v)
{
    v := "inner"
    fmt.Println(v)
    {
        fmt.Println(v)
    }
}
{
    fmt.Println(v)
}
fmt.Println(v)
```

#### Logic can be decomposed into functions

```C
#include <stdio.h>

// Function to calculate sum of an array of numbers
int calculateSum(int numbers[], int n) {
    int sum = 0;
    for (int i = 0; i < n; i++) {
        sum += numbers[i];
    }
    return sum;
}

// Function to find maximum of an array of numbers
int findMax(int numbers[], int n) {
    int max = numbers[0];
    for (int i = 1; i < n; i++) {
        if (numbers[i] > max) {
            max = numbers[i];
        }
    }
    return max;
}

// Function to find minimum of an array of numbers
int findMin(int numbers[], int n) {
    int min = numbers[0];
    for (int i = 1; i < n; i++) {
        if (numbers[i] < min) {
            min = numbers[i];
        }
    }
    return min;
}

int main() {
    int n;
    printf("Enter the number of elements: ");
    scanf("%d", &n);

    int numbers[n];
    printf("Enter %d numbers:\n", n);
    for (int i = 0; i < n; i++) {
        scanf("%d", &numbers[i]);
    }

    // Calculate sum
    int sum = calculateSum(numbers, n);

    // Find maximum
    int max = findMax(numbers, n);

    // Find minimum
    int min = findMin(numbers, n);

    // Display results
    printf("Sum: %d\n", sum);
    printf("Average: %.2lf\n", average);
    printf("Maximum: %d\n", max);
    printf("Minimum: %d\n", min);

    return 0;
}
```

#### Data can be decomposed into data structures: array, map, struct, table, composite

```C
// C array
const int CITY = 5;
const int WEEK = 7;
int temperature[CITY][WEEK];
```

```kotlin
// Kotlin map (associative array)
val scores = mapOf(
    "Alice" to 95,
    "Bob" to 87,
    "Charlie" to 91
)
```

```java
// Java Stack
Stack<Integer> stack = new Stack<>();
// Java Queue
Queue<Integer> queue = new LinkedList<>();
```

```C
// C struct
struct Student {
    char name[50];
    int age;
    char grade;
};
```

```kotlin
// Kotlin array of maps
val arrayOfMaps: Array<Map<String, Any>> = arrayOf(
    mapOf("name" to "Alice", "age" to 25, "grade" to 'A'),
    mapOf("name" to "Bob", "age" to 30, "grade" to 'B'),
    mapOf("name" to "Charlie", "age" to 28, "grade" to 'C')
)
```

```kotlin
// Kotlin maps of arrays
val map: Map<Array<Int>, Array<String>> = mapOf(
    arrayOf(1, 2, 3) to arrayOf("apple", "banana", "orange"),
    arrayOf(4, 5) to arrayOf("grape", "kiwi")
)
```

```kotlin
// Kotlin more complex data structure
data class Student(val name: String, val age: Int)
val students = arrayOf(
    mapOf(
        Student("Alice", 20) to mapOf("Math" to 85, "Physics" to 90)
    ),
    mapOf(
        Student("Bob", 22) to mapOf("History" to 75, "English" to 80)
    ),
    mapOf(
        Student("Charlie", 21) to mapOf("Biology" to 95, "Chemistry" to 88)
    )
)
```

```
import ballerina/io;

type Employee record {|
    readonly int id;
    string firstName;
    string lastName;
    int salary;
|};

public function main() {
    table<Employee> key(id) employees = table [
            {id: 1, firstName: "John", lastName: "Smith", salary: 100},
            {id: 2, firstName: "Jane", lastName: "Smith", salary: 150},
            {id: 4, firstName: "Fred", lastName: "Bloggs", salary: 200},
            {id: 7, firstName: "Bobby", lastName: "Clark", salary: 300},
            {id: 9, firstName: "Cassie", lastName: "Smith", salary: 250}
        ];

    int[] salaries = from var emp in employees
                     select emp.salary;
    io:println(salaries);

    table<Employee> highPaidEmployees = from Employee emp in employees
                             where emp.salary > 180
                             order by emp.firstName
                             select emp;

    foreach Employee emp in highPaidEmployees {
        io:println(emp.firstName, " ", emp.lastName);
    }
}
```

#### Data and logic can be decomposed into object (OOP)

```java
// Java class
public class Student {
    private String name;
    private int age;
    private char grade;

    // Constructor
    public Student(String name, int age, char grade) {
        this.name = name;
        this.age = age;
        this.grade = grade;
    }

    // Getters and Setters
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public char getGrade() {
        return grade;
    }

    public void setGrade(char grade) {
        this.grade = grade;
    }

    // Method to check if student is eligible for promotion
    public boolean isEligibleForPromotion() {
        return grade >= 'C'; // Assuming grade 'C' or above is eligible
    }

    // Method to print a message based on the student's grade
    public void printGradeMessage() {
        switch (grade) {
            case 'A':
                System.out.println("Excellent performance!");
                break;
            case 'B':
                System.out.println("Good performance!");
                break;
            case 'C':
                System.out.println("Satisfactory performance.");
                break;
            default:
                System.out.println("Needs improvement.");
                break;
        }
    }

    // Override toString() method
    @Override
    public String toString() {
        return "Student{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", grade=" + grade +
                '}';
    }
}
```

#### Data and logic can be decomposed into packages

<img src="./images/Decomposition%20-%20Packages%20-%20C.jpg" width="600">

<img src="./images/Decomposition%20-%20Packages%20-%20JS.jpg" width="600">

<img src="./images/Decomposition%20-%20Packages%20-%20Java.png" width="400">

#### Packages can be decomposed into modules

<img src="./images/Decomposition%20-%20Modules%20-%20Go.png" width="600">

#### Persistent data can be divided into sql tables/no-sql documents

<img src="./images/Decomposition%20-%20Databases.webp" width="600">

#### Sql tables/no-sql documents can be separated into different databases

<img src="./images/Decomposition%20-%20Databases.png" width="600">

#### Differences between decomposing data+logic into C modules vs. Java objects

Even though data+logic can be decomposed into different parts using either modules in C or objects in Java, there is a critical difference: relationship between the parts. Java provides built-in constructs to manage the following relationships between objects. C does not provides built-in constructs to manage the relationships between modules, except dependency in the form of `#inlcude`.

| Relationship | C   | Java |
| ------------ | --- | ---- |
| Dependency   | yes | yes  |
| Association  | no  | yes  |
| Aggregation  | no  | yes  |
| Composition  | no  | yes  |
| Inheritance  | no  | yes  |

Also, there is no concept of instantiating multiple C modules of the same type. C modules basically function as packages in Java.  
Java `class` is closer to C `struct`. C `struct` supports Association, Aggregation and Composition. However, C `struct` does not support encapsulation of data and behavior in the Java sense. We can only approximate by adding field of function pointer to a `struct`. Then we can simulate the Dependency and Inheritance relationship.

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Forward declaration of the Person struct
struct Person;

// Function pointer type for printing a Person object
typedef void (*PrintFunc)(const struct Person*);

// Define a structure to represent a Person object
typedef struct Person {
    char name[50];
    int age;
    PrintFunc print;
} Person;

// Function to create a new Person object
Person* createPerson(const char* name, int age) {
    Person* person = (Person*)malloc(sizeof(Person));
    if (person == NULL) {
        fprintf(stderr, "Memory allocation failed\n");
        exit(EXIT_FAILURE);
    }
    strncpy(person->name, name, sizeof(person->name));
    person->age = age;
    person->print = printPerson; // Assigning the print function pointer
    return person;
}

// Function to destroy a Person object
void destroyPerson(Person* person) {
    if (person != NULL) {
        free(person);
    }
}

// Function to print information about a Person object
void printPerson(const Person* person) {
    if (person != NULL) {
        printf("Name: %s\n", person->name);
        printf("Age: %d\n", person->age);
    }
}

int main() {
    // Create a new Person object
    Person* person1 = createPerson("John Doe", 30);

    // Call the print function via the function pointer
    person1->print(person1);

    // Destroy the Person object
    destroyPerson(person1);

    return 0;
}
```

### Implementation/process/deployment decomposition

#### An application can be seperated into multiple processes

<img src="./images/Decomposition%20-%20IPC.png" width="600">

#### An application's processes can be separated into multiple distributed services

<img src="./images/Decomposition%20-%20Virtualization.webp" width="600">
<img src="./images/Decomposition%20-%20Containers.png" width="600">

#### An application's distributed services can be separated into different machines

<img src="./images/Decomposition%20-%20Distributed%20System.png" width="600">
<img src="./images/Decomposition%20-%20Client-Server.webp" width="600">

### Other types of separation

#### Code can be separated into multiple repositories

Processes in multiprocess architecture tend to be distributed services. And distributed-services architecture almost always comes hand-in-hand with multi-databases architecture and multi-repo versioning strategy. This is often called microservice architecture.

## What are the potential benefits of decomposition?

<img src="./images/Decomposition%20-%20Car.png" width="600">

Decomposition addresses the challenge of understanding and managing complexity. It involves breaking down a complex problem or system into smaller, more manageable parts. Good decomposition allows us to solve each independently. In this way, the overall problem is solved or system is constructed by solving or designing each part and then combining them together.

### Comprehensibility

By dividing a complex problem into smaller parts, you can reduce the cognitive load, focus on one aspect at a time, and avoid getting lost in irrelevant details or assumptions. Breaking down complex problems also helps you to communicate more effectively with others, as you can explain your problem and your solution in a clear and logical way, and invite feedback and collaboration.

### Easier Changes

It should be possible to make drastic changes to one module without a need to change others: faster and less risky.

### Coordination/Communication

Separate groups would work on each module with little need for communication.

### Reusability

A function can be re-used at many places.

### Test isolation

### Benefits of multi-repo

#### Versioning decoupling

One problem with so many developers committing to the same code base is that the build is frequently in an unreleasable state. Trying to solve this problem by using feature branches can result in lengthy, painful merges. Consequently, once a team completes its sprint, a long period of testing and code stabilization follows.

#### Independent library versioning

When tagging a repository, its whole codebase is assigned the “new” tag. Since only the code for a specific library is on the repository, the library can be tagged and versioned independently of all other libraries hosted elsewhere.
Having an independent version for every library helps define the dependency tree for the application, allowing us to configure what version of each library to use.

#### Independent service releases

Since the repository only contains the code for some service and nothing else, it can have its own deployment cycle, independently of any progress made on the applications accessing it.

The service can use a fast release cycle such as continuous delivery (where new code is deployed after it passes all the tests). Some libraries accessing the service may use a slower release cycle, such as those that only produce a new release once a week.

#### Helps define access control across the organization

Only the team members involved with developing a library need to be added to the corresponding repository and download its code. As a result, there’s an implicit access control strategy for each layer in the application. Those involved with the library will be granted editing rights, and everyone else may get no access to the repository. Or they may be given reading but not editing rights.

#### Allows teams to work autonomously

Team members can design the library’s architecture and implement its code working in isolation from all other teams. They can make decisions based on what the library does in the general context without being affected by the specific requirements from some external team or application.

#### Less load on IDE when only one repo needs to be worked on

Less load on IDE when only one repo needs to be worked on.

### Benefits of multi-process (multi)

#### Parallelism

Multiprocess architecture allows the application to do more than one thing at a time, if you have multicore/multi-CPU system. Even if you have only a single CPU/core, it allows the OS scheduler to ensure that everything that needs to do work gets its fair share of processing time.

Another advantage of separate processes is that they can provide a security barrier. If a program needs to do some work with different permissions (e.g., as root, or even just as a different user), it can spawn a new process running as that other user to do just that bit of work. That way, it's much, much harder for a bug in one part of the code to affect the part running with different permissions. Apache is usually configured to work this way, for example. Only root can bind to low-number ports (like port 80 which is usually used by web servers), so you have to start it as root, and it binds to the port. But it doesn't need root permissions to process each web request, so it spawns a new process with lower permissions to do that work. This provides a huge security benefit since if there's a bug in a script that processes the request that allows an attacker to run arbitrary commands, it's at least running with very little privileges, so it can't access critical system files (at least not without exploiting a second bug to escalate its privileges).

A final difference is that using separate processes is the first step toward allowing you to offload the work onto a completely separate computer (client/server style). So if you're using a program flexible enough that it allows you to spread its work across several computers in a network, it'll probably use processes instead of threads.

### Faster build and startup

Edit-build-run-test loop takes less time, which improves productivity.

### Benefits of decomposing into distributed services

Part of the application can reside in different machines, different rooms, different buildings, different parts of the world.

## What are the potential costs of decomposition

<img src="./images/Decomposition%20-%20Coupling.png" width="600">

### Coupling

The different parts of an application cannot work alone. They still need to connect with each other somehow in order to solve the original problems. This "connection" is called **coupling**.
Even though there will always be some degree of coupling between parts, different designs can introduce different degree of coupling. And higher the degree of coupling is, the worse the design.

### Indirection

### Abstraction

### Coupling

### Costs of Multi-Repo

#### Higher barriers of entry

When new staff members start working for a company, they need to download the code and install the required tools to begin working on their tasks. Suppose the project is scattered across many repositories, each having its installation instructions and tooling required. In that case, the initial setup will be complex, and more often than not, the documentation will not be complete, requiring these new team members to reach out to colleagues for help.

A monorepo simplifies matters. Since there is a single location containing all code and documentation, you can streamline the initial setup.

#### Painful application-wide refactorings

When creating an application-wide refactoring of the code, multiple libraries will be affected. If you’re hosting them via multiple repositories, managing all the different pull requests to keep them synchronized with each other can prove to be a challenge.

A monorepo makes it easy to perform all modifications to all code for all libraries and submit it under a single pull request.

#### Libraries must constantly be re-synced

When a new version of a library containing breaking changes is released, libraries depending on this library will need to be adapted to start using the latest version. If the release cycle of the library is faster than that of its dependent libraries, they could quickly become out of sync with each other.

Teams will need to constantly catch up to use the latest releases from other teams. Given that different teams have different priorities, this may sometimes prove arduous to achieve.

Consequently, a team not able to catch up may end up sticking to the outdated version of the depended-upon library. This outcome will have implications on the application (in terms of security, speed, and other considerations), and the gap in development across libraries may only get wider.

#### May fragment teams

When different teams don’t need to interact, they may work in their own silos. In the long term, this could result in teams producing their subcultures within the company, such as employing different methodologies of programming or management or utilizing different sets of development tools.

If some team member eventually needs to work in a different team, they may suffer a bit of culture shock and learn a new way of doing their job.

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
