# Vascular Morphogenesis GPU

**Numerical simulation of vascular network formation using CUDA-accelerated Dielectric Breakdown Models (DBM).**

This repository contains a high-performance GPU-accelerated simulation for modeling vascular network growth (arteries and veins). Based on Laplacian growth principles from Fleury & Schwartz, it uses **CuPy** for large-scale biological structure simulation and hemodynamic pressure gradient analysis.

## 📌 Overview

Vascular morphogenesis models blood vessel network self-organization using a **Dielectric Breakdown Model (DBM)** driven by a pressure scalar field solving the Laplace equation.

### Key Features
- **GPU Acceleration**: `cupy` solves Laplace equation on high-resolution grids (512×512) orders of magnitude faster than CPU
- **Tunable Sensitivity ($\eta$)**: Growth probability $p \propto |\nabla P|^\eta$ controls branching morphology
- **Physiological Modeling**: Custom venous reservoir algorithm (veins in low-pressure zones)
- **Visualization**: Auto-generates PDF reports and MP4 animations

## 📂 Repository Structure

```
vascular-morphogenesis-gpu/
├── data/               # Outputs: .mp4 animations, .pdf plots, gifs
├── main.ipynb          # Main simulation + physics + visualization
├── references.bib      # References
└── README.md           # This file
```

## ⚙️ Requirements

CUDA-enabled GPU required.

### Core Dependencies
- Python 3.x
- [CuPy](https://cupy.dev/) (match your CUDA version)
- numpy, matplotlib, scipy

## Installation

```bash
pip install numpy matplotlib scipy
```

```bash
pip install cupy-cuda12x  # Adjust for your CUDA: cuda11x, cuda12x, etc.
```

## 🚀 Quick Start

```bash
jupyter lab main.ipynb
```

**Outputs in `data`**:
- `simulation_name.mp4`: Vascular tree time-evolution animation
- `simulation_name.pdf`: Final structure, pressure fields, growth metrics

## 🔬 Physics Model

Solves Laplace equation for pressure $P$:
$$\nabla^2 P = 0$$

**Boundary Conditions**:
| Type     | Condition          |
|----------|--------------------|
| Arteries | $P = 1$ (Source)  |
| Veins    | $P = 0$ (Sink)    |
| Tissue   | $\nabla P \cdot n = 0$ (Neumann) |

**Growth Rule**: $v \propto |\nabla P|^\eta$ (shear stress driven)

## 📊 Parameters

| Parameter | Range     | Description                  |
|-----------|-----------|------------------------------|
| η         | 1.0-3.0   | Growth sensitivity          |
| Grid size | 512×512+  | Simulation resolution        |
| Steps     | 10k-100k  | Growth iterations           |

## 📄 Citation

```bibtex
@misc{VascularMorphogenesisGPU2025,
  author = {Iker Lomas Javaloyes},
  title = {Vascular Morphogenesis using the Dielectric Breakdown Model (DBM)},
  year = {2025},
  howpublished = {\url{https://github.com/ikerbenidorm/vascular-morphogenesis-dbm}}
}
```

## 👤 Author

**Iker Lomas Javaloyes**  
*IFISC (UIB-CSIC), Palma de Mallorca*  

Based on: Fleury, V., & Schwartz, L. (1999). *Diffusion limited aggregation from shear stress as a simple model of vasculogenesis*. (DOI: [10.1142/S0218348X99000050](https://doi.org/10.1142/S0218348X99000050))
