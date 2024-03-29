# Software Decomposition

> A well-defined segmentation of the project effort ensures system modularity. Each task forms a separate, distinct program module. At implementation time each module and its inputs and outputs are well-defined, there is no confusion in the intended interface with other system modules. At checkout time the integrity of the module is tested independently; there are few scheduling problems in synchronizing the completion of several tasks before checkout can begin. Finally, the system is maintained in modular fashion; system errors and deficiencies can be traced to specific system modules, thus limiting the scope of detailed error searching.

## What is software decomposition

> Decomposition in computer science, also known as factoring, is breaking a complex problem or system into parts that are easier to conceive, understand, program, and maintain. (Wikipedia)

> Structured analysis breaks down a software system from the system context level to system functions and data entities as described by Tom DeMarco. (Wikipedia)

> Object-oriented decomposition, on the other hand, breaks a large system down into progressively smaller classes or objects that are responsible for some part of the problem domain. (Wikipedia)

A program can be thought of as containing data (states) and logic.

### Logic can be decomposed into blocks

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

### Logic can be decomposed into functions

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

### Data can be decomposed into data structures: array, map, struct, table, composite

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

### Data and logic can be decomposed into object (OOP)

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

### Data and logic can be decomposed into packages

<img src="Software_Decomposition/Decomposition - Packages - C.jpg" width="600">

<img src="Software_Decomposition/Decomposition - Packages - JS.jpg" width="600">

<img src="Software_Decomposition/Decomposition - Packages - Java.png" width="400">

### Packages can be decomposed into modules

<img src="Software_Decomposition/Decomposition - Modules - Go.png" width="600">

### Other (non-code) types of separation

<img src="Software_Decomposition/Decomposition - Architecture.png" width="600">

#### An application can be seperated into multiple processes

<img src="Software_Decomposition/Decomposition - IPC.png" width="400">

#### An application's processes can be separated into multiple distributed services

<img src="Software_Decomposition/Decomposition - Virtualization.png" width="600">
<img src="Software_Decomposition/Decomposition - Containers.png" width="600">

#### An application's distributed services can be separated into different machines

<img src="Software_Decomposition/Decomposition - Distributed System.png" width="600">
<img src="Software_Decomposition/Decomposition - Client-Server.webp" width="600">

#### Peristent data can be separated into different databases

<img src="Software_Decomposition/Decomposition - Databases.png" width="600">

#### Code can be seprated into multiple IDE projects

Big code base can slow down the IDE, making developers less productive.

#### Code can be separated into multiple repositories

## What are the potential benefits of decomposition?

<img src="Software_Decomposition/Decomposition - Car.png" width="600">

Decomposition addresses the challenge of understanding and managing complexity. It involves breaking down a complex problem or system into smaller, more manageable parts. Good decomposition allows us to solve each independently. In this way, the overall problem is solved or system is constructed by solving or designing each part and then combining them together. Decomposition is the design equivalent of distributed computation in many ways.

By dividing a complex problem into smaller parts, you can reduce the cognitive load, focus on one aspect at a time, and avoid getting lost in irrelevant details or assumptions. Breaking down complex problems also helps you to communicate more effectively with others, as you can explain your problem and your solution in a clear and logical way, and invite feedback and collaboration.

### Comprehensibility

It should be possible to study the system one module at a time. The whole system can therefore be better designed because it is better understood.

### Easier Changes

It should be possible to make drastic changes to one module without a need to change others: faster and less risky.

### Coordination/Communication

Separate groups would work on each module with little need for communication.

### Reusability

A function can be re-used at many places.

### Test isolation

### Multi-repo benefits
One problem with so many developers committing to the same code base is that the build is frequently in an unreleasable state. Trying to solve this problem by using feature branches can result in lengthy, painful merges. Consequently, once a team completes its sprint, a long period of testing and code stabilization follows.

#### Versioning decoupling

One problem with so many developers committing to the same code base is that the build is frequently in an unreleasable state. Trying to solve this problem by using feature branches can result in lengthy, painful merges. Consequently, once a team completes its sprint, a long period of testing and code stabilization follows.

### Multi-process benefits

Parallelism -- it allows the application to do more than one thing at a time, if you have multicore/multi-CPU system. Even if you have only a single CPU/core, it allows the OS scheduler to ensure that everything that needs to do work gets its fair share of processing time.
Another advantage of separate processes is that they can provide a security barrier. If a program needs to do some work with different permissions (e.g., as root, or even just as a different user), it can spawn a new process running as that other user to do just that bit of work. That way, it's much, much harder for a bug in one part of the code to affect the part running with different permissions. Apache is usually configured to work this way, for example. Only root can bind to low-number ports (like port 80 which is usually used by web servers), so you have to start it as root, and it binds to the port. But it doesn't need root permissions to process each web request, so it spawns a new process with lower permissions to do that work. This provides a huge security benefit since if there's a bug in a script that processes the request that allows an attacker to run arbitrary commands, it's at least running with very little privileges so it can't access critical system files (at least not without exploiting a second bug to escalate its privileges).

A final difference is that using separate processes is the first step toward allowing you to offload the work onto a completely separate computer (client/server style). So if you're using a program flexible enough that it allows you to spread its work across several computers in a network, it'll probably use processes instead of threads.

### Distributed system benefits

Part of the application can resides in different machines, different rooms, different buildings, different parts of the world.

## What are the potential costs of decomposition
<img src="Software_Decomposition/Decomposition - Coupling.png" width="600">

Indirection
Abstraction
Coupling

## Criteria for good decomposition

Good decomposition means the net benefit is positive (oppurtunity cost).

### Coupling
<img src="Software_Decomposition/Decomposition - Coupling & Cohesion.png" width="600">
A module here refers to a subroutine of any kind, i.e. a set of one or more statements having a name and preferably its own set of variable names.

- Code coupling (high): one module uses the code of another module, for instance a branch. This violates information hiding – a basic software design concept.
- Global data coupling: several modules have access to the same global data. But it can lead to uncontrolled error propagation and unforeseen side-effects when changes are made.
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

### Intuitiveness

## Decomposition techniques

### Functional decomposition

Functional decomposition is a software design technique in which a complex system is broken down into smaller, more manageable parts, or modules, based on their functionality or behavior. Each module represents a specific function or task within the system, and is designed to operate independently of other modules.

Functional decomposition is commonly used in object-oriented programming and structured programming paradigms. In object-oriented programming, each module is implemented as a class that encapsulates a specific set of functionality. In structured programming, each module is implemented as a function or procedure that performs a specific task.

### Business capability Decomposition

Decompose by business capability is a decomposition technique that involves breaking down a software system based on the business capabilities or functions it provides. In other words, the system is divided into smaller components based on the specific business capabilities they support, such as sales, customer service, inventory management, or accounting.

## Related terms

- Divide and Conquer
- Separation of Concerns
- Modular Programming
- Grannularity

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
