# Memory Update Decisions as Constrained Resource Allocation in 3D Reconstruction

This repository contains the code and paper for our work on non-separable coupling in entity-level memory updates for 3D Gaussian Splatting.

## Paper

**Memory Update Decisions as Constrained Resource Allocation in 3D Reconstruction**

- Author: Agostina Silva (Independent Researcher)
- arXiv: [LINK]
- Keywords: 3D Gaussian Splatting, Resource Allocation, Q-Learning, Coupling

### Abstract

Real-time 3D reconstruction systems (e.g. 3D Gaussian Splatting) face a fundamental resource allocation problem: given thousands to millions of scene entities and limited per-frame compute, which entities should be updated? We show that entity update benefits are non-separable---the value of updating entity A depends on whether B is also updated---violating the independence assumption underlying greedy selection. We formalize this as a budgeted subset selection problem, measure coupling (κ) across entity pairs in 6 real 3DGS scenes, and train a lightweight Q-network that learns to predict marginal update benefit.

## Results

| Metric | Value |
|--------|-------|
| Mean \|κ\| (6 scenes) | 0.0008 (range 0.0006–0.0012) |
| Q improvement vs heuristic | +17.1% ± 2.8% |
| CEM improvement vs heuristic | +22.2% ± 2.9% |
| Coupled entity pairs | 22.3% on average |
| Architecture | 16→64→32→1 MLP, ~40KB |

## Repository Structure

```
├── paper/
│   ├── main.tex          # LaTeX source
│   ├── main.bbl          # Compiled bibliography
│   ├── main.bib          # BibTeX database
│   └── figures/          # Paper figures
│       ├── fig_coupling_overview.png
│       ├── fig_per_scene_mse.png
│       ├── fig_aggregated.png
│       ├── fig_improvement.png
│       ├── fig_per_k_improvement.png
│       ├── fig_ablation.png
│       └── fig_varying_n.png
└── code/
    ├── notebook.ipynb    # Main experiment notebook
    ├── results_all.json  # Per-scene results
    ├── ablation.json     # Ablation study results
    └── summary.json      # Aggregated summary
```

## Setup

```bash
pip install numpy torch matplotlib scikit-learn requests scipy
```

## Usage

1. Open `code/notebook.ipynb` in Jupyter or Kaggle
2. Run all cells
3. The notebook will:
   - Download 6 real 3DGS scenes from HuggingFace
   - Build voxel proxy worlds with N=80 meta-entities
   - Compute coupling matrix κ for each scene
   - Train a Q-network to predict update benefit
   - Evaluate: heuristic, Q-learned, CEM planner, random, frequency baselines
   - Run ablation study
   - Generate all figures

## Scenes

| Scene | Gaussians | \|κ\| mean | Coupled % |
|-------|-----------|------------|-----------|
| room | 1130 | 0.0006 | 16.5% |
| kitchen | 1685 | 0.0006 | 17.6% |
| bonsai | 273 | 0.0007 | 17.6% |
| counter | 1029 | 0.0008 | 22.2% |
| bicycle | 568 | 0.0009 | 27.1% |
| garden | 4386 | 0.0012 | 32.6% |

## Citation

```bibtex
@article{silva2026memory,
  title={Memory Update Decisions as Constrained Resource Allocation in 3D Reconstruction},
  author={Silva, Agostina},
  journal={arXiv preprint},
  year={2026}
}
```

## License

This project is licensed under the MIT License - see the LICENSE file for details.
