# Class Diagram

### 1. What Is a Class Diagram?

A UML Class Diagram depicts the static structure of a system by showing its classes, attributes, operations (methods), and the relationships among objects.

***

### 2. Key Components & Legend

| Symbol / Element       | Notation / Appearance                                                    | Description                                                         |
| ---------------------- | ------------------------------------------------------------------------ | ------------------------------------------------------------------- |
| **Class**              | Rectangle divided into three compartments:• Name• Attributes• Operations | Represents a blueprint for objects.                                 |
| **Attribute**          | `+ attributeName: Type- attributeName: Type`                             | A property of a class; `+` public, `-` private, `#` protected.      |
| **Operation (Method)** | `+ methodName(params): ReturnType`                                       | A function or behavior of the class.                                |
| **Association**        | Solid line                                                               | A relationship where one class uses or knows about another.         |
| **Multiplicity**       | Labels near ends of an association (e.g., `1`, `0..*`)                   | Indicates how many instances participate in the relationship.       |
| **Aggregation**        | Hollow diamond at container end                                          | A “whole-part” relationship where the part can exist independently. |
| **Composition**        | Filled diamond at container end                                          | Stronger “whole-part” where the part’s life depends on the whole.   |
| **Inheritance**        | Solid line with hollow arrowhead                                         | Generalization between superclass and subclass.                     |
| **Dependency**         | Dashed line with open arrowhead                                          | A “uses” relationship; a change in one may affect the other.        |

***

### 3. Steps to Create a Class Diagram

1. **Identify Classes**: List the main entities in your system.
2. **Define Attributes & Operations**: For each class, determine its properties and behaviors.
3. **Draw Class Boxes**: Divide each box into Name, Attributes, and Operations sections.
4. **Establish Relationships**:
   * **Associations** for basic links.
   * **Aggregations/Compositions** for whole-part.
   * **Inheritance** for “is-a” hierarchies.
   * **Dependencies** when one class depends on another temporarily.
5. **Label Multiplicities**: Clarify how many instances participate at each end.
6. **Refine Visibility**: Use `+`, `-`, `#` to denote public, private, and protected.
7. **Review & Iterate**: Check completeness and remove any unused or redundant classes.

***

### 4. Example: Simple School System

**Scenario:** Modeling `Person`, `Teacher`, and `Student` classes.

```
classDiagram
    class Person {
        +String name
        +int age
        +void greet()
    }
    class Student {
        +String studentId
        +void enroll(courseName)
    }
    class Teacher {
        +String employeeId
        +void teach(courseName)
    }
    Person <|-- Student
    Person <|-- Teacher
    class Course {
        +String courseName
        +int credits
        +void addStudent(student)
    }
    Student "0..*" -- "1..*" Course : enrolls in
    Teacher "1" -- "0..*" Course : teaches
```

**Explanation of Structure:**

1. **Person** is a general superclass with common attributes and methods.
2. **Student** and **Teacher** inherit from **Person** (`<|--`).
3. **Course** is associated with **Student** and **Teacher**, with multiplicities showing how many can enroll or teach.

***

#### Tips

* Keep classes focused: each should have a single responsibility.
* Avoid overcrowding: split large classes into smaller, cohesive ones.
* Use diagrams to validate design with stakeholders before coding.
* Employ notes (`note left of`, `note right of` in PlantUML) for clarifications.
