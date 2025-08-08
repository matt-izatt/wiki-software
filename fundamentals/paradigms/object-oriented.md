# Object Oriented

### Overview

In OOP, programs are structured as sets of classes (blueprints) and objects (instances). Each class defines:

* **Attributes** (fields or properties) representing the object’s data
* **Methods** (member functions) encapsulating operations on that data

Objects communicate by **sending messages** (calling each other’s methods). Key principles of OOP—**encapsulation**, **inheritance**, **polymorphism**, and **abstraction**—support building flexible, extensible software.

***

### Core Principles

1. **Encapsulation**\
   Bundles state and behavior within objects, exposing only a defined interface and hiding internal implementation details.
2. **Inheritance**\
   Enables a new class (subclass) to acquire the attributes and methods of an existing class (superclass), promoting code reuse and hierarchical organization.
3. **Polymorphism**\
   Allows objects of different classes to be treated uniformly based on a shared interface or superclass. Two main forms:
   * **Subtype polymorphism** (inheritance/interface-based)
   * **Ad hoc polymorphism** (method overloading or operators)
4. **Abstraction**\
   Provides simplified models of complex reality by defining abstract classes or interfaces that specify _what_ an object can do, without detailing _how_ it does it.

***

### History

* **Simula 67 (1967)**\
  Introduced classes, objects, and inheritance to support simulation modeling.
* **Smalltalk (1970s)**\
  Pioneered a pure OOP environment with “everything is an object,” dynamic typing, and a graphical IDE.
* **C++ (1983)**\
  Brought OOP to systems programming via a superset of C, adding classes, multiple inheritance, and strong typing.
* **Java (1995)**\
  Simplified OOP with a single-inheritance model, interfaces, and built-in memory management, popularizing OOP in enterprise and web applications.

***

### Comparison with Other Paradigms

| Aspect            | Object-Oriented                       | Procedural              | Functional                   |
| ----------------- | ------------------------------------- | ----------------------- | ---------------------------- |
| Abstraction Unit  | Objects (state + behavior)            | Procedures / functions  | Pure functions / expressions |
| State Management  | Encapsulated within objects           | Mutable globals/locals  | Immutable                    |
| Code Reuse        | Inheritance & composition             | Procedure calls         | Higher-order functions       |
| Coupling          | Loose through well-defined interfaces | Tighter, direct calls   | Varies; often loose          |
| Typical Use Cases | GUIs, simulations, large systems      | Scripts, low-level code | Data pipelines, concurrency  |

***

### Advantages

* **Modularity**\
  Objects serve as natural code modules with clear boundaries.
* **Reusability**\
  Inheritance and composition allow building new functionality atop existing classes.
* **Maintainability**\
  Encapsulation localizes changes; polymorphism eases extension without modification.
* **Modeling Real-World Domains**\
  Objects map intuitively to real-world entities and relationships.

### Disadvantages

* **Complexity Overhead**\
  Designing class hierarchies can become intricate, leading to over-engineering.
* **Performance Costs**\
  Dynamic dispatch, object creation, and indirection may incur runtime overhead.
* **Tight Coupling Risk**\
  Deep inheritance chains can create fragile dependencies.
* **Learning Curve**\
  Mastery of design patterns and SOLID principles takes time.

***

### Examples

#### Java

```java
public class Animal {
    protected String name;
    public Animal(String name) { this.name = name; }
    public void speak() { System.out.println("..."); }
}

public class Dog extends Animal {
    public Dog(String name) { super(name); }
    @Override
    public void speak() { System.out.println(name + " says: Woof!"); }
}

public class Main {
    public static void main(String[] args) {
        Animal a = new Dog("Buddy");
        a.speak(); // Buddy says: Woof!
    }
}
```

#### Python

```python
class Shape:
    def area(self):
        raise NotImplementedError

class Rectangle(Shape):
    def __init__(self, w, h):
        self.w, self.h = w, h
    def area(self):
        return self.w * self.h

shapes = [Rectangle(3,4)]
print(shapes[0].area())  # 12
```
