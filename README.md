# Hybrid Quantum PDE Solver

Hybrid classical-quantum PDE solver with hand-optimized CUDA kernels for quantum matrix inversion.

**Author:** [Your Name]  
**Institution:** [Your College]  
**Challenge:** Airbus Global Quantum + AI Challenge 2026

## Architecture

| Layer | Hardware | Role |
|-------|----------|------|
| Classical | CPU | Grid setup, matrix A + vector b assembly |
| Quantum (PennyLane) | GPU | Amplitude encoding, unitary dilation |
| Quantum (Custom CUDA) | GPU | Hand-written kernels for bottlenecks |

## CUDA Optimization

- **Amplitude encoding:** Custom kernel with coalesced memory access
- **Unitary application:** Shared memory tiling
- **Reductions:** Warp-shuffle L2 norm

| Metric | PennyLane Default | Custom CUDA | Speedup |
|--------|-----------------|-------------|---------|
| Encode (N=4096) | TBD | TBD | TBD |
| Inversion (N=4096) | TBD | TBD | TBD |
| Memory bandwidth | TBD | TBD | — |

## Run

```bash
# Compile CUDA kernels
make cuda

# Run TGV at Re=100
python examples/run_tgv_re100.py

# Profile with Nsight
make profile RE=100
