# Logarithmic Bond Dimension Scaling in 2D PEPS Contraction via Successive Randomized Compression

[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/)
[![Jupyter Notebook](https://img.shields.io/badge/jupyter-notebook-orange.svg)](https://jupyter.org/)
[![LaTeX REVTeX 4-2](https://img.shields.io/badge/LaTeX-REVTeX%204--2-green.svg)](https://journals.aps.org/revtex)
[![Google Colab T4 GPU](https://img.shields.io/badge/Google%20Colab-T4%20GPU-yellow.svg)](https://colab.research.google.com/)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.20777030.svg)](https://doi.org/10.5281/zenodo.20777030)

Code and LaTeX sources supporting **"Logarithmic Bond Dimension Scaling in 2D PEPS Contraction via Successive Randomized Compression"**. Check out the repository on GitHub: [https://github.com/ayadalhusseiny/2D-SRC](https://github.com/ayadalhusseiny/2D-SRC).

2D Successive Randomized Compression (2D-SRC) is a randomized numerical linear algebra (RandNLA) algorithm for compressing boundary Matrix Product States (MPS) in 2D Projected Entangled Pair States (PEPS) contractions.

---

## Abstract

Exponential growth of virtual bond dimensions during row-by-row boundary contraction constrains the simulation of 2D quantum lattices via PEPS. The 2D Successive Randomized Compression (2D-SRC) algorithm resolves this computational bottleneck. Replacing the standard, computationally expensive singular value decomposition (SVD) with a single-pass randomized QR projection reduces the per-site complexity from $\mathcal{O}(mn^2)$ to $\mathcal{O}(mnk)$ for sketching dimension $k < n$. However, boundary sweeps on 2D lattices suffer from a unique gauge-loss deficiency: discarding the gauge remainder at the final site corrupts the partition function weight and freezes magnetization observables at unphysical saturation values. The Boundary-Weight Preservation Scheme prevents this calibration loss. Retaining the uncompressed core preserves the partition function weight at zero computational cost. Martingale tail bounds govern error accumulation. A matrix-valued Doob construction and the Matrix Freedman inequality yield a global error bound. This bound restricts the target bond dimension to logarithmic scaling with lattice size: $\bar{\chi} \sim (\xi/2)\log N$, where $\xi$ is the physical correlation length. Benchmarks on the 2D Transverse Field Ising Model (TFIM) verify these predictions. The simulation reproduces the ferromagnetic-to-paramagnetic transition. It runs $2.5\times$ faster than the deterministic SVD baseline, keeping the relative energy error at $3.9\%$ at $h/J=4.0$. At intermediate bond dimensions, the dense 2D-SRC implementation runs $10\times$ faster than standard tensor network libraries.

---

## Repository Structure

```directory
├── 2D-SRC_Experiments.ipynb          # Main simulation notebook (Ising model phase transition comparison)
├── 2D-SRC_Extended_Experiments.ipynb # Convergence vs. bond dimension and lattice scaling benchmarks
├── 2D-SRC_vs_TeNPy_Benchmark.ipynb   # Direct benchmark comparing 2D-SRC against the TeNPy library
├── Logarithmic_Bond_Dimension_Scaling_in_2D_PEPS_Contraction_via_Successive_Randomized_Compression.pdf # Compiled paper PDF
└── README.md                         # This file
```

---

## Getting Started

### Prerequisites

To run the simulation notebooks locally, you need a Python environment with the following dependencies:

```bash
pip install numpy scipy matplotlib h5py
```

To run the TeNPy benchmark notebook, you also need the `physics-tenpy` package:

```bash
pip install physics-tenpy
```

All notebooks are self-contained and run directly in Google Colab, with optional GPU acceleration for matrix multiplications.

---

## Jupyter Notebooks Overview

### Main Experiments: `2D-SRC_Experiments.ipynb`
The main simulation notebook, `2D-SRC_Experiments.ipynb`, models the 2D Transverse Field Ising Model (TFIM) on a $6\times 6$ square lattice under Open Boundary Conditions. Using Imaginary Time Evolution (ITE) via the Simple Update scheme, it compares physical observables—ground-state energy, longitudinal magnetization, and transverse magnetization—across a transverse field scan $h \in [0.0, 4.0]$ for both deterministic SVD and randomized 2D-SRC. It demonstrates how the Boundary-Weight Preservation Scheme resolves the unphysical magnetization saturation anomaly and generates the final comparison plots showcasing the $2.5\times$ speedup.

### Convergence and Scaling: `2D-SRC_Extended_Experiments.ipynb`
The convergence and scaling notebook, `2D-SRC_Extended_Experiments.ipynb`, verifies numerical stability. By sweeping the boundary bond dimension $\bar{\chi} \in [8, 24]$, it maps the exponential decay of the ground-state energy error. It shows that the unphysical magnetization overshoot disappears when $\bar{\chi} \ge 16$. The notebook also measures execution times over lattice sizes up to $10 \times 10$ to verify the scaling scaling advantage of the randomized scheme.

### TeNPy Comparison: `2D-SRC_vs_TeNPy_Benchmark.ipynb`
The third notebook, `2D-SRC_vs_TeNPy_Benchmark.ipynb`, compares our dense randomized compression against the optimized TeNPy package. By isolating a controlled 1D MPO-MPS compression subroutine, it evaluates truncation error and speed across bond dimensions $\bar{\chi} \in [8, 24]$. Directly projecting on dense NumPy arrays is $10\times$ faster than TeNPy's object-oriented structure in the intermediate bond dimension regime.

---

## Citation

To cite this work, use the following BibTeX entries:

```bibtex
@software{alhusseiny2026zenodo,
  author={Alhusseiny, Ayad},
  title={Logarithmic Bond Dimension Scaling in 2D PEPS Contraction via Successive Randomized Compression},
  month={jul},
  year={2026},
  publisher={Zenodo},
  version={v1.0},
  doi={10.5281/zenodo.20777030},
  url={https://doi.org/10.5281/zenodo.20777030}
}
```
