# STAT3 inhibitor screening from cucurbitacin E derivatives

Code and data for the study *"Screening STAT3 inhibitors from cucurbitacin E
derivatives using a medicinal chemistry filter and molecular docking"*
(Faculty of Pharmacy, University of Medicine and Pharmacy at Ho Chi Minh City).

## Medicinal chemistry filter — run it in your browser

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/phuocchung123/stat3/blob/main/Stat3_MC_filter_colab.ipynb)

Evaluates the drug-likeness of a single compound or a CSV file of compounds
against the eight criteria used in this study. No local installation required.

## Contents

| File | Description |
|---|---|
| `Stat3_MC_filter_colab.ipynb` | Colab app with input forms for single- and multi-compound screening |
| `stat3_MC_filter.ipynb` | Descriptor calculation and filter thresholds |
| `analysis_MC_filter.ipynb` | Applies the full filter to the 1056-compound library |
| `Smina-6puw.ipynb` | Batch docking with Smina |
| `data/1056_compounds.csv` | In-house library of 1056 cucurbitacin E derivatives with descriptors |
| `data/85_compounds.csv` | The 85 compounds passing all eight criteria |
| `data/22_compounds.csv` | Active set for retrospective validation (21 compounds + SD-36) |

## Filter criteria

| Type | Criterion | Threshold |
|---|---|---|
| Rule | Lipinski (MW, LogP, HBA, HBD) | at most 1 of 4 violated |
| Rule | Pfizer 3/75 | not both LogP ≥ 3 and TPSA ≤ 75 |
| Measure | Fsp3 | ≥ 0.42 |
| Measure | MCE-18 | ≥ 45 |
| Measure | SA score | ≤ 6 |
| Alert | PAINS | no substructure match |
| Alert | BMS | no substructure match |
| Alert | Chelator | no substructure match |

Lipinski's MW cutoff was relaxed from 500 to 600 g/mol. NP score is reported but
not used to reject compounds, since all derivatives are semi-synthesised from
cucurbitacin E.

**Result:** 1056 → 88 compounds pass Lipinski → **85 pass the full filter**
(2 rejected by MCE-18, 1 by SA score > 6).

## Docking model

| Setting | Value |
|---|---|
| Target | STAT3, PDB `6NJS`, co-crystallised ligand SD-36 |
| Software | Smina (AUC = 0.58; selected over Vina and QuickVina 2) |
| Box centre | 12.599, 54.028, 1.242 |
| Box size | 25 × 25 × 25 Å |
| Parameters | `--seed 42 --exhaustiveness 150 --num_modes 100` |
| Activity threshold | −5.989 kcal/mol |

## Citation

To Van Thinh, Tran Nguyen Ngoc Tam, Nguyen Van Phuoc Chung, Truong Ngoc Tuyen, Nguyen Thi Huong Giang. *Ho Chi Minh City Journal of Medicine*. 2026;29(1):18-26.
doi:10.32895/hcjm.p.2026.01.03
