# Brian2 JIT Compilation Optimization

This repository explores approaches to optimize the Just-In-Time (JIT) compilation system in Brian2, a simulator for spiking neural networks. The goal is to reduce compilation overhead while maintaining the ability to share memory between Python and compiled C++ code.

## The Problem

Brian2's current runtime mode uses Cython to compile neuron models dynamically. While execution is fast, the compilation process is slow due to massive code expansion - a typical 7,000 character Cython file expands to 535,000 characters of C++ code (76.8× expansion ratio).

## Approaches Explored

I've investigated three main approaches to solve this problem:

1. [**Shared Functions Approach**](./approach-1-shared-function/README.md): Extracting common functions into shared include files
2. [**C++ Dynamic Arrays**](./approach-2-cpp-arrays/README.md): Implementing C++ dynamic arrays with Python wrappers
3. [**Direct Raw Pointer Access**](./approach-3-direct-pointers/README.md): Exposing raw C++ pointers to the code generator

## Future Directions

Based on these experiments, I propose [several future directions](./future-directions/README.md) to further improve Brian2's JIT compilation system.
