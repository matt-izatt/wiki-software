# Data Oriented

### Overview

In data-oriented code, the structure of data and the patterns by which it is processed drive program design. By optimizing how data is laid out in memory and accessed, DOP reduces cache misses, branch mispredictions, and synchronization overhead. Logic often consists of tight loops or pipeline stages that operate on contiguous chunks of homogeneous data.

#### Key Characteristics

* **Structure of Arrays (SoA) vs. Array of Structures (AoS)**\
  Prefers SoA layouts (e.g., separate arrays per field) to improve spatial locality and enable vectorization.
* **Batch Processing & Streaming**\
  Transforms data in large, sequential passes (e.g., SIMD/vector operations, data pipelines).
* **Data Transformation Pipelines**\
  Chains of pure “stages” that each read input buffers and write to outputs, facilitating parallelism.
* **Minimized Pointer Chasing**\
  Avoids scattered references and indirection to reduce cache misses.
* **Explicit Data Ownership & Lifetimes**\
  Manages buffers and memory arenas to control allocation patterns and avoid fragmentation.
* **Separation of Data and Behavior**\
  Code modules act as functions over raw data buffers rather than methods on objects.

***

### Comparison with Other Paradigms

| Aspect              | Data-Oriented                                | Object-Oriented            | Functional                      |
| ------------------- | -------------------------------------------- | -------------------------- | ------------------------------- |
| Primary Unit        | Data layout & transformations                | Objects (state + behavior) | Pure functions                  |
| Coupling            | Loosely coupled via data contracts           | Coupled by method calls    | Coupled by function composition |
| Memory Access Focus | Cache-friendly, sequential                   | Often pointer-based        | Varies                          |
| Parallelism         | Data parallelism implicit in pipelines       | Explicit threads/locks     | Implicit via purity             |
| Typical Use Cases   | High-performance systems, games, simulations | Business apps, GUIs        | Data processing, analytics      |

***

### History

Data-oriented techniques emerged in high-performance computing and game engine development in the 1990s and 2000s, when CPU–memory gaps grew and SIMD instructions became prevalent. Early scientific codes manually laid out arrays for vector units; game programmers later popularized ECS (Entity–Component–System) architectures, a form of DOP that decouples entities (IDs), components (data arrays), and systems (processing pipelines).

***

### Advantages

* **Performance**\
  Maximizes cache utilization, prefetching, and vectorization for speed.
* **Predictable Latency**\
  Batched, streaming access patterns reduce jitter from unpredictable memory stalls.
* **Scalability**\
  Data-parallel stages map naturally to multi-core and GPU architectures.
* **Simplicity of Transformation**\
  Pure data pipes simplify reasoning about I/O and concurrency.

### Disadvantages

* **Design Overhead**\
  Requires upfront analysis of data access patterns and careful memory design.
* **Reduced Encapsulation**\
  Mixing data buffers and logic can scatter intent across modules.
* **Maintainability**\
  Highly optimized memory layouts may be harder to read and evolve.
* **Not Universally Applicable**\
  Less beneficial for I/O-bound or low-scale applications.

***

### Examples

#### C (SoA vs. AoS)

```c
// Array of Structures (AoS)
typedef struct { float x, y, z; } Vec3;
Vec3 particles[N];

// Structure of Arrays (SoA)
typedef struct { float x[N], y[N], z[N]; } Vec3SoA;
Vec3SoA particles;
```

#### C++ (Entity–Component–System)

```cpp
struct Position { float x, y, z; };
struct Velocity { float vx, vy, vz; };

std::vector<Position> positions;
std::vector<Velocity> velocities;

void updatePositions(float dt) {
    // Batch process all entities’ positions
    for (size_t i = 0; i < positions.size(); ++i) {
        positions[i].x += velocities[i].vx * dt;
        positions[i].y += velocities[i].vy * dt;
        positions[i].z += velocities[i].vz * dt;
    }
}
```

#### Rust (Data Pipelines)

```rust
fn scale_and_shift(data: &mut [f32], scale: f32, shift: f32) {
    data.iter_mut().for_each(|x| *x = *x * scale + shift);
}

fn main() {
    let mut buffer = vec![0.0; 1_000_000];
    scale_and_shift(&mut buffer, 2.0, 1.0);
}
```
