# Logarithmic Bond Dimension Scaling in 2D PEPS Contraction via Successive Randomized Compression

[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/)
[![Jupyter Notebook](https://img.shields.io/badge/jupyter-notebook-orange.svg)](https://jupyter.org/)
[![LaTeX REVTeX 4-2](https://img.shields.io/badge/LaTeX-REVTeX%204--2-green.svg)](https://journals.aps.org/revtex)
[![Google Colab T4 GPU](https://img.shields.io/badge/Google%20Colab-T4%20GPU-yellow.svg)](https://colab.research.google.com/)

This repository contains the numerical experiment notebooks and the compiled PDF manuscript for the paper **"Logarithmic Bond Dimension Scaling in 2D PEPS Contraction via Successive Randomized Compression"**. The repository is hosted on GitHub at [https://github.com/ayadalhusseiny/2D-SRC](https://github.com/ayadalhusseiny/2D-SRC).

We introduce **2D Successive Randomized Compression (2D-SRC)**, a randomized numerical linear algebra (RandNLA) algorithm for compressing the boundary Matrix Product States (MPS) in 2D Projected Entangled Pair States (PEPS) contractions.

---

## 📖 Abstract

The main computational bottleneck in contracting 2D tensor networks is the multiplicative growth of the bond dimension when using the Boundary MPS method. To address this, we generalize the recently proposed Successive Randomized Compression (SRC) algorithm from 1D chain geometries to 2D networks, introducing the specialized **2D-SRC** algorithm. By replacing the standard, computationally expensive singular value decomposition (SVD) with a single-pass randomized QR projection, we reduce the per-site computational cost from $\mathcal{O}(mn^2)$ to $\mathcal{O}(mnk)$ with $k \ll n$. 

We identify and resolve a critical boundary gauge-loss deficiency unique to 2D contractions via a novel **Boundary-Weight Preservation Scheme**. Furthermore, we establish rigorous error bounds for the sequential randomized projections using a matrix-valued Doob martingale and the Matrix Freedman inequality, proving that under the area law of entanglement, the target bond dimension scales only logarithmically with the lattice size: $\bar{\chi} \sim (\xi/2)\log N$. 

We benchmark the 2D-SRC algorithm on the 2D Transverse Field Ising Model (TFIM) on a $6\times 6$ lattice, demonstrating a $2.5\times$ speedup over the deterministic SVD baseline with a relative energy error below $4\%$, and a $10\times$ speed advantage over industry-standard tensor network libraries for intermediate bond dimensions.

---

## 📂 Repository Structure

```directory
├── 2D-SRC_Experiments.ipynb          # Main simulation notebook (Ising model phase transition comparison)
├── 2D-SRC_Extended_Experiments.ipynb # Convergence vs. bond dimension and lattice scaling benchmarks
├── 2D-SRC_vs_TeNPy_Benchmark.ipynb   # Direct benchmark comparing 2D-SRC against the TeNPy library
├── Logarithmic_Bond_Dimension_Scaling_in_2D_PEPS_Contraction_via_Successive_Randomized_Compression.pdf # Compiled paper PDF
└── README.md                         # This file
```

---

## 🚀 Getting Started

### Prerequisites

To run the simulation notebooks locally, you need a Python environment with the following dependencies installed:

```bash
pip install numpy scipy matplotlib h5py
```

To run the TeNPy benchmark notebook, you also need to install the `physics-tenpy` package:

```bash
pip install physics-tenpy
```

*Note: All notebooks are fully self-contained and equipped with setup cells to run directly in Google Colab (with optional GPU acceleration for matrix multiplications).*

---

## 📓 Jupyter Notebooks Detailed Overview

### 1. Main Experiments Notebook: `2D-SRC_Experiments.ipynb`
*   **Purpose**: Simulates the 2D Transverse Field Ising Model (TFIM) on a $6\times 6$ square lattice under Open Boundary Conditions (OBC) using Imaginary Time Evolution (ITE) via the Simple Update scheme.
*   **Features**:
    *   Implements both the **Deterministic SVD** and the **Randomized 2D-SRC** boundary contraction sweep.
    *   Compares physical observables: ground-state energy per site $E/N$, longitudinal magnetization $\langle Z \rangle$, and transverse magnetization $\langle X \rangle$ for a transverse field scan $h \in [0.0, 4.0]$.
    *   Demonstrates the **Boundary-Weight Preservation Scheme** which prevents unphysical magnetization saturation.
    *   Generates `comparison_plots.png` showing the phase transition and a $2.5\times$ computational speedup.

### 2. Extended Experiments Notebook: `2D-SRC_Extended_Experiments.ipynb`
*   **Purpose**: Validates the numerical convergence and scaling behavior of the 2D-SRC algorithm.
*   **Features**:
    *   Sweeps the boundary bond dimension $\bar{\chi} \in [8, 24]$ to show the exponential decay of the ground-state energy error.
    *   Demonstrates that the unphysical magnetization overshoot ($\langle Z \rangle > 1.0$) is corrected as $\bar{\chi} \ge 16$.
    *   Measures execution time scaling over different lattice sizes $L \times L$ for $L \in \{4, 6, 8, 10\}$, verifying the scaling advantage of the randomized scheme.
    *   Generates `extended_plots.png`.

### 3. TeNPy Benchmark Notebook: `2D-SRC_vs_TeNPy_Benchmark.ipynb`
*   **Purpose**: Compares our dense randomized compression against the optimized industry-standard **TeNPy** package.
*   **Features**:
    *   Sets up a controlled 1D MPO-MPS multiplication and compression benchmark (representing the core subroutine in 2D sweeps).
    *   Evaluates relative truncation error and execution time across bond dimensions $\bar{\chi} \in [8, 24]$.
    *   Shows that our Python/NumPy implementation of 2D-SRC tracks SVD truncation errors while achieving a $10\times$ execution speed advantage due to low class-overhead in the intermediate bond dimension regime.
    *   Generates `tenpy_comparison_plots.png`.

---



## ✒️ Citation

If you use this code or refer to the manuscript in your research, please cite:

```bibtex
@article{alhusseiny2026logarithmic,
  title={Logarithmic Bond Dimension Scaling in 2D PEPS Contraction via Successive Randomized Compression},
  author={Alhusseiny, Ayad},
  journal={arXiv preprint arXiv:XXXX.XXXXX},
  year={2026}
}
```
