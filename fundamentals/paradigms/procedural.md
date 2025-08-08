# Procedural

### Overview

In procedural programs, the primary unit of abstraction is the procedure. Programs are composed by defining procedures that manipulate program state—typically via variables and data structures—and by calling these procedures in a controlled sequence. Control flow constructs (loops, conditionals) and explicit state changes remain central, but responsibilities are factored into discrete, named routines.

#### Key Characteristics

* **Modular Organization**\
  Code is divided into procedures, each encapsulating a coherent piece of functionality.
* **Procedure Calls**\
  Execution jumps to a procedure and returns when it completes, enabling code reuse and abstraction.
* **Local and Global State**\
  Procedures may operate on global variables or on parameters and local variables passed in.
* **Structured Control Flow**\
  Emphasizes constructs like `if`, `for`/`while`, and avoids unstructured jumps (e.g., `goto`).
* **Top-Down Design**\
  Programs are often planned by decomposing high-level tasks into smaller subtasks, each implemented as a procedure.

***

### History

Procedural programming emerged in the late 1950s and early 1960s alongside the first high-level languages. FORTRAN (1957) introduced subroutines for numerical computation. ALGOL (1958) formalized block structure and scope rules, influencing Pascal (1970) and C (1972). Languages such as BASIC and COBOL also adopted procedural constructs. The structured programming movement (1960s–1970s), championed by Dijkstra and others, refined best practices for procedure design and control flow, cementing the procedural style as the dominant paradigm for decades.

***

### Relationship to Other Paradigms

| Paradigm        | Focus                                        | Abstraction Unit            |
| --------------- | -------------------------------------------- | --------------------------- |
| Procedural      | How to perform tasks via routines            | Procedures / Functions      |
| Imperative      | Step-by-step state changes                   | Statements / Commands       |
| Object-Oriented | Encapsulation of state & behavior in objects | Classes / Objects           |
| Functional      | Evaluation of pure functions                 | Functions (no side effects) |

Procedural programming is a specialized form of imperative programming, distinguished by its emphasis on named routines rather than only ad-hoc sequences of statements. While object-oriented programming (OOP) builds on procedural roots by bundling data with methods, procedural code typically operates on externally defined data structures.

***

### Advantages

* **Clarity and Maintainability**\
  Well-named procedures make high-level program structure explicit.
* **Reusability**\
  Common routines can be invoked from multiple places, reducing duplication.
* **Ease of Understanding**\
  A top-down design maps naturally to human problem-solving: decompose, implement, test.
* **Wide Language Support**\
  Nearly all general-purpose languages provide procedural features.

### Disadvantages

* **Global State Risks**\
  Excessive use of global variables can lead to tight coupling and hard-to-trace bugs.
* **Limited Abstraction**\
  Compared to OOP, procedural code may lack clear data–behavior encapsulation.
* **Scalability Challenges**\
  Very large procedural codebases can become unwieldy without rigorous organization and naming conventions.

***

### Examples

#### C (Procedural)

```c
#include <stdio.h>

int gcd(int a, int b) {
    while (b != 0) {
        int r = a % b;
        a = b;
        b = r;
    }
    return a;
}

int main() {
    int x = 42, y = 56;
    printf("GCD of %d and %d is %d\n", x, y, gcd(x, y));
    return 0;
}
```

#### Python (Procedural Style)

```python
def flatten(matrix):
    result = []
    for row in matrix:
        for val in row:
            result.append(val)
    return result

data = [[1, 2], [3, 4], [5, 6]]
print(flatten(data))  # Outputs: [1, 2, 3, 4, 5, 6]
```
