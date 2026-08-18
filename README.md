# Computational Methods for Rapid Fluorocarbon Characterization

Supporting information, datasets, and computational workflows for the manuscript
*Computational Methods for Rapid Fluorocarbon Characterization*.

This repository provides reproducible tools for developing and evaluating
Benson-style group-additivity (GA) thermochemical models, with a focus on
fluorocarbon-containing molecules.

## Citation

If you use this repository, its data, or its workflows in your work,
please cite the associated manuscript:

Eccles, S. and Pellizzeri, S. *Expanded Group Additivity Framework for Thermochemical Prediction of Fluorocarbons and PFAS from Large Scale DFT Data*, J. Phys. Chem. A (2026), DOI: [10.1021/acs.jpca.6c03256](https://doi.org/10.1021/acs.jpca.6c03256).

---

## Repository Structure

```
.
├── BensonGAF/                          # BensonGAF group-additivity library
│   ├── library.yaml                    # Library entry point (lists included parameter files)
│   ├── scheme.yaml                     # Group-matching patterns (SMARTS-like rules)
│   └── gas_benson/
│       └── fluorocarbon_groups.yaml    # Fitted fluorocarbon group parameters
├── Data/                               # Datasets and regression notebook
│   ├── fluorocarbon_DFT_thermochemistry.csv   # DFT-derived H, S, Cp reference data
│   ├── fluorocarbon_molecule_list.csv          # SMILES and names for training molecules
│   ├── fluorocarbon_group_matrix.csv           # Group-count matrix (molecules × groups)
│   └── GAF_Group_Regression.ipynb      # Notebook: fit GA parameters from DFT data
├── pGrAdd_with_GAF.ipynb               # Notebook: predict thermochemistry with BensonGAF
├── requirements.txt                    # Python package dependencies
├── LICENSE                             # MIT License
└── README.md
```

---

## Project Overview

Fluorocarbon thermochemistry is challenging due to:

- Strong C–F bonds and unusual vibrational mode behavior
- Sparse high-quality reference data
- Limited Benson group-additivity parameters for fluorinated functional groups

This project addresses these challenges by providing:

- Benson-style GA workflows for enthalpy (H), entropy (S), and heat capacity (Cp)
- DFT-derived reference data computed with statistical-mechanics corrections
- Cross-validation and Grubbs' outlier detection for robust parameter estimation
- A ready-to-use `BensonGAF` library compatible with the `pgradd` Python package

---

## Notebooks

### `pGrAdd_with_GAF.ipynb` — Predict Thermochemistry

Uses the fitted `BensonGAF` library to:

- Estimate H, S, and Cp for any fluorocarbon SMILES with groups covered by the library
- Batch-compare predictions against the DFT reference dataset and report absolute errors

### `Data/GAF_Group_Regression.ipynb` — Fit Group Parameters

Fits new Benson GA parameters from DFT data:

- Loads Gaussian log files and extracts thermochemical properties via statistical mechanics (pmutt)
- Builds a group-count matrix from SMILES using pgradd
- Fits group contributions by least-squares regression with k-fold cross-validation
- Removes statistical outliers using an iterative Grubbs' test
- Exports the fitted parameters to `BensonGAF/gas_benson/fluorocarbon_groups.yaml`

---

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/PellizzeriLab/Computational-Methods-for-Rapid-Fluorocarbon-Characterization.git
cd Computational-Methods-for-Rapid-Fluorocarbon-Characterization
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Install the BensonGAF library into pgradd

`pgradd` looks for named libraries inside its own `data/` directory.
Copy the `BensonGAF/` folder there so that `GroupLibrary.Load('BensonGAF')` works:

```bash
# Find the pgradd data directory
python -c "import pgradd, os; print(os.path.join(os.path.dirname(pgradd.__file__), 'data'))"
```

Then copy the library folder into that path, for example:

```bash
cp -r BensonGAF/ /path/to/pgradd/data/BensonGAF
```

The `BensonGAF/` folder must contain `library.yaml`, `scheme.yaml`, and the
`gas_benson/` sub-directory with `fluorocarbon_groups.yaml`.

### 4. Run the notebooks

```bash
jupyter notebook
```

Open `pGrAdd_with_GAF.ipynb` to predict thermochemical properties, or
`Data/GAF_Group_Regression.ipynb` to re-fit the group parameters from scratch.

---

## Data Files

| File | Description |
|------|-------------|
| `Data/fluorocarbon_DFT_thermochemistry.csv` | DFT-derived H, S, and Cp (300–1500 K) for all training molecules |
| `Data/fluorocarbon_molecule_list.csv` | SMILES strings and common names for all fluorocarbon training molecules |
| `Data/fluorocarbon_group_matrix.csv` | Pre-built group-count matrix used as the regression feature matrix |
| `BensonGAF/gas_benson/fluorocarbon_groups.yaml` | Fitted Benson group contributions — load with `GroupLibrary.Load('BensonGAF')` |

---

## License

This project is released under the MIT License. See the [LICENSE](LICENSE) file for details.

---

## Contributors

- Sam C. Eccles
- Steven Pellizzeri

## Contact

For questions about the computational methods or manuscript, please contact the
[Pellizzeri Lab](https://github.com/PellizzeriLab) or open an issue in this repository.
