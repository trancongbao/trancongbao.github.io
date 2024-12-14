# What is software decomposition

> Structured analysis breaks down a software system from the system context level to system functions and data entities as described by Tom DeMarco. (Wikipedia)

> Object-oriented decomposition, on the other hand, breaks a large system down into progressively smaller classes or objects that are responsible for some part of the problem domain. (Wikipedia)

## Architecture & the 4+1 architecture view model

There are numerous definitions of software architecture. For example, see https://en.wikiquote.org/wiki/Software_architecture to read some of them. My favorite definition comes from Len Bass and colleagues at the Software Engineering Institute (www.sei.cmu.edu), who played a key role in establishing software architecture as a discipline. They define software architecture as follows:

> The software architecture of a computing system is the set of structures needed to reason about the system, which comprise software elements, relations among them, and properties of both. (Documenting Software Architectures by Bass et al.)

That’s obviously a quite abstract definition. But its essence is that an application’s architecture is its **decomposition** into parts (the **elements**) and the relationships (the **relations**) between those parts.

Decomposition is important for a couple of reasons:

- It facilitates the division of labor and knowledge. It enables multiple people (or multiple teams) with possibly specialized knowledge to work productively together on an application.
- It defines how the software elements interact.

It’s the decomposition into parts and the relationships between those parts that determine the application’s -ilities.

### The 4+1 view model of software architecture

More concretely, an application’s architecture can be viewed from multiple perspectives, in the same way that a building’s architecture can be viewed from structural, plumbing, electrical, and other perspectives. Phillip Krutchen wrote a classic paper describing the 4+1 view model of software architecture, “Architectural Blueprints—The ‘4+1’ View Model of Software Architecture” (www.cs.ubc.ca/~gregor/teaching/papers/4+1view-architecture.pdf).
The 4+1 model defines four different views of a software architecture. Each describes a particular aspect of the architecture and consists of a particular set of software elements and relationships between them.
<img src="./images/Decomposition - Architecture.png" width="600">

The purpose of each view is as follows:

- **Logical view**— The software elements that are created by developers. In object-oriented languages, these elements are classes and packages. The relations between them are the relationships between classes and packages, including inheritance, associations, and depends-on.
- **Implementation view**— The output of the build system. This view consists of modules, which represent packaged code, and components, which are executable or deployable units consisting of one or more modules. In Java, a module is a JAR file, and a component is typically a WAR file or an executable JAR file. The relations between them include dependency relationships between modules and composition relationships between components and modules.
- **Process view**— The components at runtime. Each element is a process, and the relations between processes represent interprocess communication.
- **Deployment view**— How the processes are mapped to machines. The elements in this view consist of (physical or virtual) machines and the processes. The relations between machines represent networking. This view also describes the relationship between processes and machines.

In addition to these four views, there are the **scenarios**—the +1 in the 4+1 model—that animate views. Each scenario describes how the various architectural components within a particular view collaborate in order to handle a request. A scenario in the logical view, for example, shows how the classes collaborate. Similarly, a scenario in the process view shows how the processes collaborate.

## Logical decomposition

A program can be thought of, logically, as containing data (states) and logic.

> In terms of logic, there is a spectrum from code -> block -> function -> package -> service. In hierarchical data model, there is a spectrum from one piece of primitive data -> array/map/struct -> complex composite -> package -> service. In relational data model, the is a spectrum from row -> table -> database -> database server.

```mermaid
flowchart TD
    subgraph Application[Applicaion]
        subgraph 1 [Service 1]
            subgraph 1.1 [Module 1.1]
                subgraph 1.1.1 [Function]
                    1.1.1.1[Code Block]
                    1.1.1.2[Code Block]
                end
                subgraph 1.1.2 [Function]
                    1.1.2.1[Code Block]
                    1.1.2.2[Code Block]
                end
            end
            subgraph 1.2 [Module 1.2]
                subgraph 1.2.1 [Function]
                    1.2.1.1[Code Block]
                    1.2.1.2[Code Block]
                end
                subgraph 1.2.2 [Function]
                    1.2.2.1[Code Block]
                    1.2.2.2[Code Block]
                end
            end
        end
        subgraph 2 [Service 2]
            subgraph 2.1 [Module 2.1]
                subgraph 2.1.1 [Function]
                    2.1.1.1[Code Block]
                    2.1.1.2[Code Block]
                end
                subgraph 2.1.2 [Function]
                    2.1.2.1[Code Block]
                    2.1.2.2[Code Block]
                end
            end
            subgraph 2.2 [Module 2.2]
                subgraph 2.2.1 [Function]
                    2.2.1.1[Code Block]
                    2.2.1.2[Code Block]
                end
                subgraph 2.2.2 [Function]
                    2.2.2.1[Code Block]
                    2.2.2.2[Code Block]
                end
            end
        end
    end
```

> In terms of design quality, there is a spectrum from code quality -> design quality -> architecture quality.

The design quality of an application can basically be determined from the design quality of each parts and the degree of coupling between these top-level parts.

- The quality of decomposition is determined by two factors: cohesion and coupling.
- The degree of coupling in the system is one of the primary indicators of the quality of the decomposition. The other indicators include cohesion, and obviously the quality of the different parts (e.g. if you choose MongoDB as your no-sql databases).

#### Logic can be decomposed into blocks

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

<img src="./images/Decomposition%20-%20Packages%20-%20C.jpg" width="600">

<img src="./images/Decomposition%20-%20Packages%20-%20JS.jpg" width="600">

<img src="./images/Decomposition%20-%20Packages%20-%20Java.png" width="400">

### Packages can be decomposed into modules

<img src="./images/Decomposition%20-%20Modules%20-%20Go.png" width="600">

### Persistent data can be divided into sql tables/no-sql documents

<img src="./images/Decomposition%20-%20Databases.webp" width="600">

### Sql tables/no-sql documents can be separated into different databases

<img src="./images/Decomposition%20-%20Databases.png" width="600">

### Differences between decomposing data+logic into C modules vs. Java objects

Even though data+logic can be encapsulated using either modules in C or objects in Java, there are two critical differences.

One critical difference is that multiple similar objects in Java can be instatiated from the same class (the blueprint specifying what fields and methods are included). C modules basically function as packages in Java. Java `class` is closer to C `struct`. C `struct` supports Association, Aggregation and Composition. However, C `struct` does not support encapsulation of data and behavior in the Java sense. We can only approximate by adding field of function pointer to a `struct`. Then we can simulate the Dependency and Inheritance relationship.

The other crirical difference is relationship between the parts. Java provides built-in constructs to manage the following relationships between objects. C does not provides built-in constructs to manage the relationships between modules, except dependency in the form of `#inlcude`.

| Relationship | C   | Java |
| ------------ | --- | ---- |
| Dependency   | yes | yes  |
| Association  | no  | yes  |
| Aggregation  | no  | yes  |
| Composition  | no  | yes  |
| Inheritance  | no  | yes  |

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

## Implementation/process/deployment decomposition

### An application can be seperated into multiple processes

<img src="./images/Decomposition%20-%20IPC.png" width="600">

### An application's processes can be separated into multiple distributed services

<img src="./images/Decomposition%20-%20Virtualization.webp" width="600">
<img src="./images/Decomposition%20-%20Containers.png" width="600">

### An application's distributed services can be separated into different machines

<img src="./images/Decomposition%20-%20Distributed%20System.png" width="600">
<img src="./images/Decomposition%20-%20Client-Server.webp" width="600">
