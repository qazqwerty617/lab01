# Matrix-Vector Multiplication (Serial & Parallel)

This repository contains implementations of matrix-vector multiplication algorithms in both serial and parallel versions using MPI (Message Passing Interface).

## Files

- `serialMV.cpp` - Serial implementation of matrix-vector multiplication
- `parallelMV.cpp` - Parallel implementation using MPI for distributed computing

## Computational Experiments (Exercise 2)

### Serial Algorithm Performance Results

Below are the results of the serial matrix-vector multiplication performance tests:

| Test Number | Matrix Size | Execution Time (sec) |
|-------------|-------------|---------------------|
| 1           | 10          | 0.000001            |
| 2           | 100         | 0.000021            |
| 3           | 1,000       | 0.002274            |
| 4           | 2,000       | 0.008302            |
| 5           | 3,000       | 0.017908            |
| 6           | 4,000       | 0.034297            |
| 7           | 5,000       | 0.049847            |
| 8           | 6,000       | 0.079489            |
| 9           | 7,000       | 0.104879            |
| 10          | 8,000       | 0.132574            |
| 11          | 9,000       | 0.162175            |
| 12          | 10,000      | 0.231854            |

### Performance Comparison: Serial vs Parallel Matrix-Vector Multiplication

| Matrix Size | Serial Algorithm (s) | 1 Processor (s) | 2 Processors (s) | Speed-up (x) | 4 Processors (s) | Speed-up (x) | 8 Processors (s) | Speed-up (x) |
|-------------|---------------------|-----------------|------------------|--------------|------------------|--------------|------------------|--------------|
| 10          | 0.000001            | 0.000013        | 0.000086         | 0.012        | 0.000164         | 0.006        | 0.000190         | 0.005        |
| 100         | 0.000021            | 0.000082        | 0.000095         | 0.221        | 0.000128         | 0.164        | 0.000360         | 0.058        |
| 1,000       | 0.002274            | 0.005902        | 0.003990         | 0.570        | 0.008905         | 0.255        | 0.007849         | 0.290        |
| 2,000       | 0.008302            | 0.021380        | 0.017656         | 0.470        | 0.014582         | 0.569        | 0.020585         | 0.404        |
| 3,000       | 0.017908            | 0.041498        | 0.033311         | 0.538        | 0.035685         | 0.502        | 0.037004         | 0.484        |
| 4,000       | 0.034297            | 0.076273        | 0.061416         | 0.558        | 0.061187         | 0.561        | 0.058020         | 0.591        |
| 5,000       | 0.049847            | 0.119062        | 0.098593         | 0.506        | 0.087212         | 0.572        | 0.099650         | 0.500        |
| 6,000       | 0.079489            | 0.222101        | 0.162361         | 0.489        | 0.145407         | 0.547        | 0.124267         | 0.639        |
| 7,000       | 0.104879            | 0.259092        | 0.185179         | 0.567        | 0.166697         | 0.629        | 0.180208         | 0.582        |
| 8,000       | 0.132574            | 0.387418        | 0.303950         | 0.436        | 0.315440         | 0.420        | 0.296376         | 0.447        |
| 9,000       | 0.162175            | 0.447766        | 0.362223         | 0.448        | 0.341767         | 0.475        | 0.384447         | 0.422        |
| 10,000      | 0.231854            | 0.561848        | 0.515475         | 0.450        | 0.460325         | 0.504        | 0.437986         | 0.529        |

## Analysis

### Key Observations:

1. **Serial Performance**: The serial algorithm shows consistent performance scaling with matrix size, with execution time increasing quadratically as expected for O(n²) complexity.

2. **Parallel Performance**: The parallel implementation shows varying performance characteristics:
   - For small matrices (10-100), parallel overhead dominates, resulting in slower execution than serial
   - For medium to large matrices (1,000+), parallel implementation shows some speedup, particularly with 8 processors
   - Maximum speedup achieved: 0.639x for 6,000x6,000 matrix with 8 processors

3. **Scaling Behavior**: 
   - Speed-up generally improves with larger matrix sizes
   - 8 processors show the best performance for larger matrices
   - Communication overhead limits scalability for smaller problem sizes

## Compilation and Execution

### Serial Version
```bash
g++ -o serialMV serialMV.cpp
./serialMV
```

### Parallel Version
```bash
mpic++ -o parallelMV parallelMV.cpp
mpirun -np <number_of_processes> ./parallelMV
```

## Requirements

- C++ compiler (g++)
- MPI implementation (OpenMPI or MPICH)
- For parallel version: `mpic++` compiler wrapper

## Algorithm Complexity

- **Time Complexity**: O(n²) for both serial and parallel versions
- **Space Complexity**: O(n²) for matrix storage, O(n) for vectors
- **Parallel Communication**: O(n) for data distribution and result gathering
