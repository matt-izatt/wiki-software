# Declarative

### Overview

Unlike imperative programming, which focuses on explicit sequences of commands and mutable state, declarative programming emphasizes the _declaration_ of desired results. The underlying system (compiler, interpreter, or runtime) is responsible for deriving an execution strategy that satisfies those declarations.

#### Key Characteristics

* **Expression of Intent**\
  Programs consist of expressions or declarations that specify the relationship between input and output, rather than sequences of steps.
* **Immutability**\
  State changes are minimized or eliminated; data structures are often immutable.
* **Side‐Effect Minimization**\
  Pure declarative functions avoid side effects, enabling equational reasoning and easier testing.
* **Automatic Optimization**\
  With intent specified rather than procedure, runtimes can reorder, parallelize, or optimize computations transparently.
* **Abstraction**\
  Control flow, iteration, and state management are handled by the language or libraries, freeing developers to focus on domain logic.

***

### Categories of Declarative Paradigms

1. **Functional Programming**\
   Emphasizes evaluation of pure functions, higher‐order functions, and expressions.
   * _Examples:_ Haskell, Elm, parts of Scala, F#
2. **Logic Programming**\
   Represents programs as sets of logical clauses and queries; a solver determines which facts and rules satisfy a query.
   * _Examples:_ Prolog, Datalog
3. **Constraint Programming**\
   Specifies constraints (relations) that must hold; a solver finds variable assignments that satisfy all constraints.
   * _Examples:_ MiniZinc, CLP(FD)
4. **Database Query Languages**\
   Describe _what_ data to retrieve rather than _how_ to traverse records.
   * _Examples:_ SQL, SPARQL
5. **Markup & Configuration**\
   Used for describing data structures, UI layouts, or build configurations.
   * _Examples:_ HTML, XML, JSON, YAML, Terraform HCL

***

### Comparison with Imperative Programming

| Aspect        | Declarative                          | Imperative                            |
| ------------- | ------------------------------------ | ------------------------------------- |
| Focus         | _What_ to do (specification)         | _How_ to do it (control flow)         |
| State         | Minimized or implicit                | Explicit, mutable                     |
| Side Effects  | Discouraged or absent                | Common                                |
| Parallelism   | Often implicit (runtime‐driven)      | Must be managed by programmer         |
| Readability   | Tends to be higher for domain logic  | Can be lower due to low‐level details |
| Optimizations | Compiler/runtime may freely optimize | Limited by explicit control flow      |

***

### History

Although early languages like COBOL (1959) and Lisp (1958) exhibited declarative traits, the paradigm was formalized in the 1970s with the development of logic programming (e.g., Prolog in 1972) and the emergence of purely functional languages (e.g., Miranda in 1985, Haskell in 1990). The rise of relational databases in the 1970s popularized declarative query languages (SQL), demonstrating the power of specifying _what_ rather than _how_. Since then, declarative techniques have proliferated into domain‐specific languages, build systems, and configuration management tools.

***

### Advantages

* **Clarity and Maintainability**\
  By focusing on _what_ needs to be achieved, code closely mirrors problem specifications.
* **Correctness Reasoning**\
  Pure, side‐effect‐free functions and logical rules facilitate formal verification and testing.
* **Optimization Potential**\
  Runtimes can safely transform and parallelize computations without altering program semantics.
* **Conciseness**\
  High‐level abstractions often lead to more succinct code.

### Disadvantages

* **Performance Predictability**\
  Abstraction layers may obscure control flow, making performance tuning more difficult.
* **Learning Curve**\
  Developers accustomed to imperative thinking may find declarative constructs non‐intuitive.
* **Tooling and Debugging**\
  Debugging declarative programs—where control flow is implicit—often requires specialized tools or tracing support.

### Example

#### SQL

```sql
SELECT name, COUNT(*) AS order_count
FROM orders
WHERE order_date >= '2025-01-01'
GROUP BY name;
```

This statement declares _what_ data to return; the database engine determines the optimal execution plan (indexes to use, join orders, parallel scans).
