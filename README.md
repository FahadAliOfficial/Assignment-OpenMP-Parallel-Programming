# OpenMP Matrix Multiplication Assignment
# Matrix Multiplication: Sequential vs. OpenMP Parallelization

## Overview
This project demonstrates the performance improvement achieved through OpenMP parallelization in matrix multiplication. We compare a traditional sequential approach with a parallelized version using OpenMP, highlighting the execution time differences.

## Project Structure
- **Sequential Implementation (`sequential.c`)**: Implements matrix multiplication using a traditional loop-based approach.
- **OpenMP Implementation (`openmp.c`)**: Uses OpenMP directives to parallelize matrix multiplication for performance improvement.
- **.gitignore**: Ensures unnecessary files are ignored in the Git repository.
- **README.md**: This documentation file.

## Implementation Details

### 1. Sequential Matrix Multiplication
- Uses nested loops to perform matrix multiplication.
- Execution time is measured and averaged over 10 runs.
- Uses matrices of size **500x500**.

#### Execution Time (Sequential)
- Range: **0.411653s – 0.550991s**
- Most runs were close to **0.4s**.

#### Code Snippet (Sequential)
```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#define N 500

void multiply_matrices(int A[N][N], int B[N][N], int C[N][N]) {
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            C[i][j] = 0;
            for (int k = 0; k < N; k++) {
                C[i][j] += A[i][k] * B[k][j];
            }
        }
    }
}
```

### 2. OpenMP Parallelized Matrix Multiplication
- Utilizes `#pragma omp parallel for` for parallel execution.
- Uses **dynamic scheduling** and specifies thread count using `num_threads(NUM_THREADS)`.
- Execution time is measured and averaged over 10 runs.

#### Execution Time (Parallel - OpenMP)
- Range: **0.233341s – 0.278214s**
- Most runs were close to **0.23s**, showing significant improvement over the sequential approach.

#### Code Snippet (Parallel)
```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <omp.h>
#define N 500
#define NUM_THREADS 4

void multiply_matrices_parallel(int A[N][N], int B[N][N], int C[N][N]) {
    #pragma omp parallel for schedule(dynamic) num_threads(NUM_THREADS)
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            C[i][j] = 0;
            for (int k = 0; k < N; k++) {
                C[i][j] += A[i][k] * B[k][j];
            }
        }
    }
}
```

## Performance Comparison
| Implementation | Execution Time Range |
|---------------|----------------------|
| Sequential    | 0.411653s – 0.550991s |
| OpenMP (Parallel) | 0.233341s – 0.278214s |

## Conclusion
The use of OpenMP significantly reduces execution time by utilizing multiple threads for computation. This demonstrates the power of parallel processing in computationally expensive operations like matrix multiplication.

## How to Run
### Compile and Run (Sequential)
```sh
gcc sequential.c -o sequential.out
./sequential.out
```

### Compile and Run (Parallel with OpenMP)
```sh
gcc -fopenmp openmp.c -o openmp.out
./openmp.out
```

## Requirements
- GCC Compiler
- OpenMP Library

## Author
Fahad Ali

