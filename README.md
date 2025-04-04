# Brian2 JIT Compilation Optimization

This repository explores approaches to optimize the Just-In-Time (JIT) compilation system in Brian2, a simulator for spiking neural networks. The goal is to reduce compilation overhead while maintaining the ability to share memory between Python and compiled C++ code.

## The Problem

Brian2's current runtime mode uses Cython to compile neuron models dynamically. While execution is fast, the compilation process is slow due to massive code expansion - a typical 7,000 character Cython file expands to 535,000 characters of C++ code (76.8× expansion ratio).

## Approaches Explored

I've investigated three main approaches to solve this problem:

1. [**Shared Functions Approach**](./approach-1-shared-functions/): Extracting common functions into shared include files
2. [**C++ Dynamic Arrays**](./approach-2-cpp-arrays/): Implementing C++ dynamic arrays with Python wrappers
3. [**Direct Raw Pointer Access**](./approach-3-direct-pointers/): Exposing raw C++ pointers to the code generator

## Benchmark Summary

| Approach   | Code Expansion | Creation (1M) | Resize (1M) | Compilation Time  |
| ---------- | -------------- | ------------- | ----------- | ----------------- |
| Original   | 76.8×          | 0.000018s     | 0.000090s   | 1.000s (baseline) |
| Approach 1 | 53.2×          | 0.000018s     | 0.000090s   | 1.001s            |
| Approach 2 | -              | 0.000016s     | 0.000019s   | 0.870s            |
| Approach 3 | -              | 0.000016s     | 0.000019s   | 0.210s            |

For detailed benchmarks and methodology, see [Benchmarks](./docs/benchmarks.md).

## Future Directions

Based on these experiments, I propose [several future directions](./future-directions/) to further improve Brian2's JIT compilation system.
