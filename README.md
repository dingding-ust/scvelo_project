# scVelo Project

This repository contains code, data references, and documentation for reproducing and analyzing RNA velocity using the scVelo dynamical model. The workflow demonstrates how to derive and fit a full transcriptional kinetics model from static scRNA-seq snapshots, apply the Expectation-Maximization (EM) algorithm for parameter and latent variable inference, and visualize the resulting directional flows of cellular states.

## Overview

The accompanying report (found in `docs/CASIA_report(Ding Ding).pdf`) presents the mathematical foundations, statistical inference strategies, and code implementations that integrate into the RNA velocity pipeline described in [Bergen et al., 2020](https://doi.org/10.1038/s41587-020-0591-3). Specifically, this project focuses on:

- Deriving ODE-based transcriptional dynamics models without steady-state assumptions.
- Employing the EM algorithm for parameter and latent variable inference (joint estimation of $(\alpha,\beta,\gamma)$ and $(t_i,k_i)$).
- Incorporating first- and second-order moments to stabilize and improve inference accuracy.
- Performing differential kinetics testing to determine if multiple kinetic regimes are statistically justified.
- Demonstrating a simplified EM-like simulation experiment (in `code/analysis.ipynb`) illustrating that even a crude iterative approach can recover known parameters and switching times.

**Note on Original Contribution:**
A key original element of this project is the simulation experiment within `code/analysis.ipynb` that shows how a simplified EM-inspired strategy can successfully infer parameters in a controlled scenario. This goes beyond the standard scVelo tutorials and is explicitly implemented by the author.

## Repository Structure

```
scvelo_project/
├─ code/
│  ├─ analysis.ipynb          # Main Jupyter notebook with code steps and simulations
│  └─ data/
│     └─ endocrinogenesis_day15.h5ad  # Example dataset
├─ data/                      # (Optional) Additional data directory if needed
├─ docs/
│  └─ CASIA_report(Ding Ding).pdf     # The detailed report
└─ README.md                  # This file
```

## Dependencies

- Python 3.9 or later (tested)
- `scvelo` == 0.3.3 (or compatible)
- `scanpy`, `numpy`, `matplotlib`, and other standard Python packages
- Optional: `igraph`, `louvain`, `pybind11`, `hnswlib` for efficiency and advanced features

Refer to the [scVelo documentation](https://scvelo.org) for additional environment setup details and to the [YouTube guide](https://www.youtube.com/watch?v=AUiYxtGJYtg) for tutorial-style demonstrations.

## Setup and Running the Code

1. **Create and activate environment:**

    ```bash
    conda create -n scvelo-env python=3.9 -y
    conda activate scvelo-env
    ```

2. **Install scvelo and dependencies:**

    ```bash
    pip install scvelo igraph louvain pybind11 hnswlib
    ```

3. **Clone the repository:**

    ```bash
    git clone https://github.com/dingding-ust/scvelo_project.git
    cd scvelo_project
    ```

4. **Navigate and run the notebook:**

    ```bash
    cd code
    jupyter notebook analysis.ipynb
    ```

    Open the notebook in your browser and execute cells to reproduce preprocessing, EM-based inference, velocity computations, and the original simulation scenario.

## Reproducibility and Academic Integrity

- This repository includes explicit instructions and code snippets to ensure the results are reproducible.
- The simulation experiment implemented in `analysis.ipynb` is original and not taken from existing scVelo guides.
- When existing implementations (e.g., scVelo’s built-in functions) are used, it is clearly indicated to comply with academic integrity requirements.
- The repository is maintained openly on GitHub, allowing for verification and validation of steps, results, and methodologies.

## Notes and Limitations

- The provided `endocrinogenesis_day15.h5ad` dataset is an example. For large-scale or custom data, adjust file paths and potentially run on more powerful hardware.
- Some steps (e.g., EM-based inference) may be computationally intensive for large datasets.
- The simplified EM-like simulation is conceptual and should be treated as a demonstration rather than a production-ready solution.

## References

- La Manno G., Soldatov R., Zeisel A., *et al.* (2018) RNA velocity of single cells. *Nature* **560**, 494–498.
- Bergen V., Lange M., Peidli S., *et al.* (2020) Generalizing RNA velocity to transient cell states through dynamical modeling. *Nat Biotechnol* **38**, 1408–1414.

