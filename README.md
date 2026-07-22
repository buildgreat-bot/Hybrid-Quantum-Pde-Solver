# Hybrid Quantum-Classical PDE Solver

**A modular hybrid engine for solving discretized PDEs with classical + quantum (PennyLane + CUDA) components.**

## Aim
Engineering problems in heat transfer, fluid dynamics, and aerodynamics require solving large linear systems from discretized PDEs. Classical methods struggle with memory and time at high resolution.  

This project explores a **hybrid approach**:  
- Classical CPU layer handles grid discretization and physics assembly.  
- Quantum/GPU layer accelerates the linear solve via amplitude encoding and unitary methods.  
- Goal: Demonstrate practical hybrid workflows, scaling behavior, and validation for benchmarks like the 2D Taylor-Green Vortex (relevant to Airbus challenge).

**Current Status**: Early construction / prototype phase. Core architecture defined, basic flow partially implemented. Not production-ready.

## Architecture Overview

**Key Layers**:
- **Input/Config**: PDE-specific plug-ins (e.g., `taylor_green_vortex.py`) define parameters (N, dt, Re).
- **Classical Setup**: Grid generation, stencil computation, assembly of sparse Matrix A and vector b.
- **Quantum Solve**: Amplitude encoding + unitary dilation solve on GPU (PennyLane Lightning + custom CUDA kernels for performance).
- **Post-Processing**: Physical field reconstruction, L2 error vs. analytic solution, plots.
- **Benchmarking**: CPU vs GPU comparison, memory bandwidth, occupancy analysis with Nsight.

## Project Structure (High-Level)
- `plugins/` — Domain-specific PDE configurations
- `src/classical/` — Grid, stencils, assembly
- `src/quantum/` — Encoding, solving, circuit setup
- `src/cuda/kernels/` — Hand-optimized CUDA kernels
- `benchmarks/` — Performance comparisons and profiling
- `examples/` — End-to-end run scripts
- `tests/` — Validation against analytic solutions

## Current Progress
- Architecture and data flow fully designed.
- Core classical layers and basic PennyLane integration in progress.
- Custom CUDA kernels planned for performance optimization.
- Taylor-Green Vortex plug-in and benchmarking framework targeted next.

Everything is under active development. Expect breaking changes.


python examples/run_tgv_re100.py
