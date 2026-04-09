This repository contains the supporting information, datasets, and computational workflows associated with the manuscript Computational Methods for Rapid Fluorocarbon Characterization.
It provides reproducible tools for evaluating and developing thermochemical group additivity models, with a focus on fluorocarbon‑containing molecules.

Repository Structure:
.
├── BensonGAF/                    # Group additivity parameter files 
├── Data/                         # Raw and processed datasets
├── pGrAdd_with_GAF.ipynb         # Main analysis notebook 
├── LICENSE                       # MIT License
└── README.md                     # Project documentation

Project Overview:
Fluorocarbon thermochemistry is notoriously difficult due to:

Strong C–F bonds and unusual vibrational mode behavior

Sparse high‑quality reference data

Poor performance of harmonic approximations for low‑frequency modes

Limited group additivity parameters for fluorinated functional groups

This project addresses these challenges by providing:

Benson‑style group additivity workflows for enthalpy, entropy, and heat capacity

Cross‑validation and outlier detection to ensure robust parameter estimation

Fluorocarbon‑specific corrections integrated into the GAF framework

Transparent, reproducible Jupyter Notebook analysis

Main Notebook:
pGrAdd_with_GAF.ipynb
This notebook demonstrates the full workflow used in the manuscript:

Implementing GAF library for determination of H, S and Cp for any structure with groups within GAF library

Comparison to raw DFT data with absolute errors to monitor performance

Analysis Notebook:
GAF_Group_Regression.ipynb
This notebook demonstrates the full workflow used in the manuscript:

Dataset loading and preprocessing

Group assignment and feature construction

Model fitting and validation

Error analysis and visualization

Export of group contributions for downstream use

It is designed to be self‑contained and easy to run in any standard scientific Python environment.

Package Requirements
Recommended Python packages:

numpy

pandas

matplotlib

scikit-learn

ruamel.yaml

jupyter

rdkit 

pmutt

pgradd

Getting Started
Clone the repository:

bash
git clone https://github.com/PellizzeriLab/Computational-Methods-for-Rapid-Fluorocarbon-Characterization.git
Navigate into the project directory:

bash
cd Computational-Methods-for-Rapid-Fluorocarbon-Characterization
Launch Jupyter:

bash
jupyter notebook
Open pGrAdd_with_GAF.ipynb and run the workflow.

License:
This project is released under the MIT License.
See the LICENSE file for details.

Contributors:
Sam C. Eccles

Steven Pellizzeri

Contact:
For questions about the computational methods or manuscript, please contact the Pellizzeri Lab or open an issue in this repository.
