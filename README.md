# Machine-Learning Prediction of Shear-Wave Velocity in the Dampier Sub-basin

Code and data for the Honours dissertation *Machine-Learning Prediction of Shear-Wave Velocity in the Dampier Sub-basin: Accuracy, Errors and Applications* by Danyah Aldosaimani (School of Earth and Planetary Sciences, Curtin University, 2026).

The notebooks predict shear-wave velocity (Vs) from standard well logs (gamma ray, density, neutron porosity, resistivity and Vp) in the five wells with measured Vs, test five models with leave-one-well-out (LOWO) validation, and check how the prediction errors affect Poisson's ratio, Young's modulus and a Gassmann brine-to-CO₂ fluid substitution.

## Contents

```
notebooks/        six Jupyter notebooks, numbered in the order they are run
data/processed/   one table per well (<Well>_with_formation.csv), read by the notebooks
data/las/         empty: place the LAS files here (see Data)
results/          LOWO accuracy tables (R², RMSE, MAE) written by the notebooks
README.md         this file
```

| Notebook | What it does | Dissertation |
|---|---|---|
| 01_Regression_Models_Linear_Ridge_Lasso | Data loading and quality control; Linear, Ridge and Lasso regression with LOWO validation; Lasso α selection; SHAP input contributions; washout check; prediction in the wells without measured Vs | Sections 3.3–3.6, 4.1–4.4 |
| 02_MLP | Multilayer perceptron with LOWO validation, and the five-seed test | Section 4.1; Table A2 |
| 03_Stacked_Ensemble | Stacked ensemble of the linear models | Section 4.1 |
| 04_Model_Comparison | Compares the accuracy of the five models | Section 4.1; Table A1 |
| 05_Elastic_Parameters | Poisson's ratio and Young's modulus from measured and predicted Vs; errors by formation and Vp/Vs analysis | Sections 3.7–3.8, 4.2–4.3, 4.5.1; Table A3 |
| 06_Fluid_Substitution | Gassmann substitution from brine to CO₂ in sand B of Lambert_8B with measured and Lasso-predicted Vs; CO₂ saturation sweep, clay-modulus sensitivity and Gassmann checks | Sections 3.9, 4.5.2; Tables A4–A6 |

Each notebook starts with a short description, followed by a **Settings** cell that holds all file paths. Notebook 05 is provided without saved outputs; its results are reported in the dissertation.

**Figures:** the notebooks reproduce all the results (numbers, tables and the data behind each figure). The figures in the dissertation were redrawn from these results with separate plotting scripts for a consistent style (colours, fonts and layout), so they look different from the notebook plots but show the same data. The notebooks also contain exploratory and diagnostic plots that are not shown in the dissertation.

## Data

- **LAS files (not included):** the edited and petrophysical LAS files (`<Well>_LQC.las`) of the eight wells (Egret_2, Lambert_8B, Nereus_1, Persephone_1, Seraph_1, Angel_1, Angel_3, Wanaea_11A) are publicly available from NOPIMS through the NEATS Public Portal (https://public.neats.nopta.gov.au), Barrow Dampier CCS Regional Study, reprocessing project ENO0810814A, document D00020854 (Barlass et al., 2024). Download them into `data/las/`.
- **Processed tables (included):** `data/processed/` holds one table per well, made from the LAS curves, with a formation name added at each depth from the regional study's formation tops.

## How to run

1. Install Python 3.12 with pandas, NumPy, scikit-learn, SHAP, lasio, rockphypy and matplotlib.
2. Download the LAS files into `data/las/` (the processed tables are already in `data/processed/`). Alternatively, change the paths in each notebook's Settings cell.
3. Run the notebooks in order from the `notebooks/` folder. Notebook 04 reads the results of 01–03, and notebook 06 reads `lasso_training_5wells.csv`, which notebook 01 writes to `results/`.

## Reference

Barlass, D., R. Hamilton, A. Parent, I. L. H. Pei, S. Mehay, and O. Schenk, 2024, Barrow Dampier CCS regional study: Report prepared by Schlumberger Australia Pty Ltd for Geoscience Australia, available from NOPIMS, reprocessing project ENO0810814A, document D00020852.
