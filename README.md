# SANS 10162-1 Beam-Column Design Notebook

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/SAEng-design/beam-column-notebook/blob/main/notebooks/E6_1_beam_column_SANS10162.ipynb)

Jupyter notebook reproducing **Example E6.1** from *Design of Structural Steelwork to SANS 10162, Edition 3 (2013)* — a braced beam-column subject to strong-axis bending.

Calculations are rendered with [`handcalcs`](https://github.com/connorferster/handcalcs) and units are managed with [`forallpeople`](https://github.com/connorferster/forallpeople), so the output reads like a hand-written calculation sheet rather than a code dump.

## How to use it

1. **Click the "Open in Colab" badge above.** The notebook opens in Google Colab in your browser.
2. In Colab: **File → Save a copy in Drive**, then rename for your job (e.g. `COL-B2-12_E6_1.ipynb`).
3. Edit the `PROJECT` dictionary near the top with your project particulars (project name, member code, engineer, checker, approver, etc.).
4. Adjust the design loads and trial section as needed.
5. **Runtime → Run all**.
6. Review results, then run the **Export to PDF** cell to produce an archive copy.

No local Python install is required. The master copy in this repository is intended to be **read-only** — each calculation should be saved as a separate file per job.

## Repository structure

```
beam-column-notebook/
├── README.md                                       This file
├── requirements.txt                                Python dependencies
├── notebooks/
│   └── E6_1_beam_column_SANS10162.ipynb            The master notebook
└── data/
    ├── h_sections.csv                              SAISC H-section properties
    └── i_sections.csv                              SAISC I-section properties
```

## What the notebook covers

The three checks required by SANS 10162-1 Clause 13.8.2 for a beam-column under combined axial compression and major-axis bending:

| Check | Clause | What it verifies |
|---|---|---|
| (i)   Cross-sectional strength       | 13.8.2          | Section can resist the combined stresses at any point along its length |
| (ii)  Overall member strength        | 13.8.2          | Member doesn't fail by overall in-plane buckling (weak-axis flexural buckling combined with bending) |
| (iii) Lateral-torsional buckling     | 13.8.2 / 13.6(a) | Beam-column doesn't fail by LTB |

It also performs the Clause 11 section classification (compression flange outstand and web in combined compression and bending).

## Scope and caveats

- Implements Example E6.1 specifically: uniaxial strong-axis bending, braced frame, double curvature.
- Other load cases — biaxial bending, sway frames, single curvature — require changes to the moment-gradient factors ($\omega_{1x}$, $\omega_2$) and the U-factor logic. See Clauses 13.8.4–13.8.5.
- Hot-rolled H-section assumed ($n = 1.34$ in Clause 13.3.1). For welded sections use $n = 2.24$.
- $f_y = 350$ MPa (Grade S355JR per worked example). Edit `f_y` for other grades and review yield reductions for thickness.
- $K_z = 1.0$ is conservative for the LTB check. A lower value may be justified with restraint details.

## Dependencies

The setup cell handles installation automatically on Colab. For local Jupyter installs:

```bash
pip install -r requirements.txt
```

## References

- SANS 10162-1:2011 — *The structural use of steel — Part 1: Limit-states design of hot-rolled steelwork*
- *Design of Structural Steelwork to SANS 10162*, Edition 3 (2013), SAISC — Example E6.1
- SAISC Red Book — Section property tables

## Licence

This calculation tool is provided as-is, intended for use by qualified structural engineers. All designs produced must be verified by a registered professional engineer. ViKO Consulting Engineers accepts no liability for designs produced using this tool.
