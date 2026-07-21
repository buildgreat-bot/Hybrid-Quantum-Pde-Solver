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


---

## The TGV Config (`plugins/taylor_green_vortex.py`)

```python
"""
Taylor-Green Vortex configuration for Airbus Challenge.
10-line PDE profile.
"""

CONFIG = {
    "name": "taylor_green_vortex",
    "dimension": 2,
    "domain_length": 6.28318530718,  # 2*pi
    "grid_size": 64,  # N x N
    "vortex_velocity": 1.0,  # V0
    "convection_x": 1.0,  # Uc
    "convection_y": 0.0,  # Vc
    "density": 1.0,  # rho
    "reynolds_number": 100,  # Re
    "background_pressure": 0.0,  # p0
    "time_step": 0.001,  # dt
    "final_time": 1.0,  # t_final
    "viscosity": lambda cfg: cfg["vortex_velocity"] * cfg["domain_length"] / cfg["reynolds_number"],
}

# Profile with Nsight
make profile RE=100
