# KIPS: Kinase Inhibitor Profiling Set

## Where to find the KIPS data

- `Data/KIPS_Dataset.csv`: The full dataset, 1,553 compounds and 468 kinase constructs
- `Output/Intermediate/KIPS_Curated/KIPS_380_Kinases.csv`: The curated set, 1,538 compounds and 380 wild-type human kinases
- `Output/Intermediate/KIPS_Curated/KIPS_Curated_SI65.csv`: The curated compounds with SI65 and promiscuity class
- `Output/Intermediate/KIPS_Curated/KIPS_Train.csv` and `KIPS_Test.csv`: The training (1,230) and test (308) compounds
- `Output/Intermediate/KIPS_Curated/KIPS_Full.csv`: The full dataset with standardized SMILES

## System requirements

- Operating system: Windows (untested on Linux/macOS)
- Python: 3.10.20

All dependencies are listed in `environment.yml`. Key packages: rdkit 2024.3.2, numpy 1.26.4, pandas 2.3.3, scikit-learn 1.7.2, xgboost 2.1.4, optuna 4.8.0, shap 0.49.1, mmpdb 3.1.4, networkx 3.4.2, umap-learn 0.5.11, scipy 1.15.3, statsmodels 0.14.6, seaborn 0.13.2, matplotlib 3.7.5, aiohttp 3.13.5, tqdm 4.67.3, kneed 0.8.6, upsetplot 0.9.0.

## Installation

1. Install Anaconda or Miniconda
2. Create and activate the environment:

   ```
   conda env create -f environment.yml
   conda activate KIPS
   ```

3. Launch Jupyter with `jupyter notebook`

Typical installation time is 10-20 minutes.

## Running the notebooks

Run the notebooks in `Notebooks/` in this order:

1. `01_Binding_Type.ipynb`: Identifies covalent and allosteric compounds using reference datasets
2. `02_BindingDB.ipynb`: Extracts kinase and non-kinase inhibitor sets from BindingDB
3. `03_Statistical_Analysis.ipynb`: Curates KIPS, computes promiscuity metrics, and runs the descriptor, scaffold, enrichment and chemical space analyses
4. `04_MMPA.ipynb`: Analyzes matched molecular pairs and promiscuity changes
5. `05_Promiscuity_Modeling.ipynb`: Trains and evaluates the models and generates SHAP explanations and robustness analyses
6. `06_Production_Model.ipynb`: Demonstrates predictions and SHAP explanations with the saved model

Notebooks 01 and 02 need internet access. The full pipeline takes about 24 hours on a standard desktop, nearly all of it in notebook 05. To reproduce the manuscript results, do not change `RANDOM_SEED` (2026).

## Data versions

The paper used the October 2025 BindingDB release, UniProt data from October 2025, KLIFS queried in October 2026, and ChEMBL and Chemical Probes Portal exports from 13 September 2026.

The files derived from these sources are provided in `Data/`: `Binding_Type.csv`, `BindingDB_Kinase_Inhibitors.csv` and `BindingDB_Non_Kinase_Inhibitors.csv`. Notebook 03 uses them by default, so notebooks 01 and 02 are not needed to reproduce the paper.

Notebook 02 downloads the current release of BindingDB Data. Because BindingDB and KLIFS change over time, re-running notebooks 01 and 02 may alter results slightly. Their new files are written to `Output/Intermediate/Regenerated_Inputs/`, and setting `USE_PAPER_INPUTS = False` in notebook 03 uses them.

## Output folders

- `Output/Figures/`: Paper figures, in `Main` and `Supplementary`
- `Output/Tables/`: Paper tables, in `Main`, `Supplementary_Information` and `Supplementary_Data`
- `Output/Intermediate/`: Files used by later steps, including the curated KIPS files, the final model and figure panels
- `Output/Supporting/`: Various additional results that were not included in the paper or supplemental sections

## License

The code is released under the MIT License (see `LICENSE`). Third-party datasets in `Data/` remain under their original terms.