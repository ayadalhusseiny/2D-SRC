# Logarithmic Bond Dimension Scaling in 2D PEPS Contraction via Successive Randomized Compression

[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/)
[![Jupyter Notebook](https://img.shields.io/badge/jupyter-notebook-orange.svg)](https://jupyter.org/)
[![LaTeX REVTeX 4-2](https://img.shields.io/badge/LaTeX-REVTeX%204--2-green.svg)](https://journals.aps.org/revtex)
[![Google Colab T4 GPU](https://img.shields.io/badge/Google%20Colab-T4%20GPU-yellow.svg)](https://colab.research.google.com/)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.20777030.svg)](https://doi.org/10.5281/zenodo.20777030)

This repository hosts the code and LaTeX sources for **"Logarithmic Bond Dimension Scaling in 2D PEPS Contraction via Successive Randomized Compression"**. You can access the project on GitHub at [https://github.com/ayadalhusseiny/2D-SRC](https://github.com/ayadalhusseiny/2D-SRC).

We implement 2D Successive Randomized Compression (2D-SRC), a randomized numerical linear algebra (RandNLA) scheme designed to compress boundary Matrix Product States (MPS) during the contraction of 2D Projected Entangled Pair States (PEPS).

---

## Abstract

Boundary contraction of 2D Projected Entangled Pair States (PEPS) suffers from exponential growth in virtual bond dimensions, limiting simulation scale. We resolve this bottleneck using 2D Successive Randomized Compression (2D-SRC). By replacing the standard singular value decomposition (SVD) with a single-pass randomized QR projection, we reduce the per-site complexity from $\mathcal{O}(mn^2)$ to $\mathcal{O}(mnk)$ for sketching dimension $k < n$. Yet, 2D boundary sweeps exhibit a critical gauge-loss anomaly: discarding the gauge remainder at the final sweep site corrupts the partition function weight, forcing magnetization observables to saturate at unphysical values. Our Boundary-Weight Preservation Scheme avoids this calibration loss entirely. Retaining the uncompressed core costs nothing computationally while fully preserving the partition function weight. To analyze error accumulation, we construct a matrix-valued Doob martingale and apply the Matrix Freedman inequality. This analysis yields a global error bound restricting the required bond dimension to logarithmic scaling with lattice size, $\bar{\chi} \sim \xi\log N$, where $\xi$ denotes the physical correlation length. Numerical tests on the 2D Transverse Field Ising Model (TFIM) confirm these predictions. Our implementation reproduces the ferromagnetic-to-paramagnetic transition and runs $2.5\times$ faster than the deterministic SVD baseline. At $h/J=4.0$, the relative ground-state energy error remains below $3.9\%$. For intermediate bond dimensions, our dense implementation outperforms standard tensor network libraries by a factor of ten.

---

## Repository Structure

```directory
├── 2D-SRC_Experiments.ipynb          # Main simulation notebook (Ising model phase transition comparison)
├── 2D-SRC_Extended_Experiments.ipynb # Convergence vs. bond dimension and lattice scaling benchmarks
├── 2D-SRC_vs_TeNPy_Benchmark.ipynb   # Direct benchmark comparing 2D-SRC against the TeNPy library
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

Every notebook is self-contained and executes directly in Google Colab. You can enable GPU acceleration to speed up matrix multiplications.

---

## Jupyter Notebooks Overview

### Main Experiments: `2D-SRC_Experiments.ipynb`
We model the 2D Transverse Field Ising Model (TFIM) on a $6\times 6$ open-boundary square lattice in `2D-SRC_Experiments.ipynb`. By executing Imaginary Time Evolution (ITE) via the Simple Update scheme, the code scans the transverse field $h \in [0.0, 4.0]$ to compare deterministic SVD against randomized 2D-SRC. Observables collected include ground-state energy, longitudinal magnetization, and transverse magnetization. The notebook demonstrates how the Boundary-Weight Preservation Scheme eliminates the unphysical magnetization saturation anomaly while producing the final comparison plots that confirm the $2.5\times$ speedup.

### Convergence and Scaling: `2D-SRC_Extended_Experiments.ipynb`
Numerical stability and scaling are verified in `2D-SRC_Extended_Experiments.ipynb`. Sweeping the boundary bond dimension $\bar{\chi} \in [8, 24]$ maps the exponential decay of the ground-state energy error. Magnetization overshoots vanish when $\bar{\chi} \ge 16$. To establish the scaling advantage of our randomized scheme, the notebook measures execution runtimes across lattice dimensions up to $10 \times 10$.

### TeNPy Comparison: `2D-SRC_vs_TeNPy_Benchmark.ipynb`
To contrast dense randomized compression against the optimized TeNPy library, use `2D-SRC_vs_TeNPy_Benchmark.ipynb`. We isolate a controlled 1D MPO-MPS compression step to measure truncation error and execution speed across bond dimensions $\bar{\chi} \in [8, 24]$. In the intermediate bond dimension regime, projecting directly on dense NumPy arrays is $10\times$ faster than TeNPy's object-oriented framework.

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
