# Functional

### Overview

In functional programs, the primary building blocks are functions that map inputs to outputs without side effects. Rather than specifying sequences of commands, developers compose and transform data through function application. The paradigm draws heavily on the principles of lambda calculus and algebraic data types.

#### Key Characteristics

* **Pure Functions**\
  Functions consistently produce the same output for the same inputs and do not alter external state.
* **Immutability**\
  Data structures cannot be modified after creation; operations return new structures.
* **First-Class and Higher-Order Functions**\
  Functions are values: they can be passed as arguments, returned from other functions, and stored in data structures.
* **Function Composition**\
  Complex operations arise from combining simpler functions, often via operators like `∘`, `|>`, or specialized combinators.
* **Declarative Data Transformation**\
  Uses constructs such as `map`, `filter`, and `reduce` to express transformations over collections.
* **Lazy vs. Strict Evaluation**\
  Some languages defer computation until results are needed (lazy), while others evaluate eagerly (strict).
* **Strong Typing and Type Inference** (in many FP languages)\
  Advanced type systems (e.g., Hindley–Milner) enable compile-time guarantees and concise code.

***

### Styles and Sub-Paradigms

1. **Pure vs. Impure FP**
   * _Pure FP:_ Enforces purity (e.g., Haskell).
   * _Impure FP:_ Allows controlled side effects (e.g., Scala, F#, Clojure).
2. **Strict vs. Lazy Evaluation**
   * _Strict:_ Eagerly evaluates function arguments (e.g., ML, OCaml).
   * _Lazy:_ Delays evaluation until needed (e.g., Haskell).
3. **Statically vs. Dynamically Typed FP**
   * _Statically Typed:_ Compile-time type checking (e.g., Haskell, Elm).
   * _Dynamically Typed:_ Run-time type checking (e.g., Clojure, JavaScript with FP libraries).
4. **Functional Reactive Programming (FRP)**\
   Extends FP to reactive systems, modeling time-varying values as streams (e.g., Rx, Elm).
5. **Category-Theoretic and Algebraic Approaches**\
   Employs abstractions like monads, functors, and applicatives for structuring effects and computations.

***

### Comparison with Other Paradigms

| Aspect                 | Functional                                 | Imperative                | Declarative                  |
| ---------------------- | ------------------------------------------ | ------------------------- | ---------------------------- |
| State & Side Effects   | Avoided or isolated via monads/contexts    | Pervasive                 | Varies; often discouraged    |
| Control Flow           | Function composition & recursion           | Loops, conditionals       | Specification of what        |
| Abstraction Mechanisms | Higher-order functions, types, combinators | Procedures, objects       | Queries, rules               |
| Parallelism            | Implicit via pure code                     | Manual threads/locks      | Runtime-driven in some DSLs  |
| Reasoning & Testing    | Equational reasoning                       | Harder with mutable state | Often easier than imperative |

***

### History

Functional concepts originate from Alonzo Church’s **lambda calculus** (1930s), a formal system for functions and application. Lisp (1958) was the first practical FP language, pioneering recursive functions and symbolic computation. ML (1973) introduced static typing and pattern matching. Haskell (1990) solidified pure, lazy FP with a standardized language report. Since then, FP ideas have influenced mainstream languages (JavaScript, Python, Java, C#) through libraries and functional features.

***

### Advantages

* **Modularity & Composability**\
  Small, pure functions compose predictably to build complex behavior.
* **Ease of Testing & Verification**\
  Purity and immutability simplify unit testing and formal proofs.
* **Concurrency & Parallelism**\
  Lack of shared mutable state reduces race conditions, enabling safe parallel execution.
* **Conciseness**\
  High-level abstractions often yield shorter, expressive code.

### Disadvantages

* **Performance Overheads**\
  Immutable data and recursion may incur runtime or memory costs without optimizations (e.g., tail-call elimination).
* **Steep Learning Curve**\
  Concepts like monads, currying, and type inference can be challenging for newcomers.
* **Debugging FP Code**\
  Indirect control flow and lazy evaluation order can complicate debugging and profiling.

***

### Examples

#### Haskell (Pure, Lazy)

```haskell
-- Compute factorial using recursion and composition
factorial :: Integer -> Integer
factorial n = foldl (*) 1 [1..n]
```
