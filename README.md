# ELISA Analyzer

> [!IMPORTANT]
> This README describes a WIP project and is subject to change

Automated ELISA export parser and analyzer.

## Summary

ELISA Analyzer is a Python tool to parse instrument-exported Excel workbooks (example: `exportAll.xlsx`), extract plate metadata and well-level optical density (OD) readings, perform preprocessing and QC (blank subtraction, replicate handling, outlier detection), fit a standard curve (4-parameter logistic or linear fallback), and output calibrated concentrations and visual reports.

## Motivation

Instrument exports frequently mix metadata and plate grids in a human-oriented layout. Manually extracting concentrations is time-consuming and error-prone. This project automates that workflow and produces reproducible, checked outputs for lab use or analysis.

## Example input

- `example_input/exportAll.xlsx` — workbook containing per-plate sheets (e.g. `Plate 1 - Sheet1`, `Plate 2 - Sheet1`) with metadata rows followed by plate grids.

The implementation will be robust to similar instrument exports and include documentation about supported formats.

## Outputs

- Cleaned tabular data (CSV/TSV) with one row per well: plate, well (A1..H12), raw OD, corrected OD, concentration, QC flags.
- Per-plate plots (PNG/PDF): plate heatmap, standard curve with fit and residuals.
- Optional interactive HTML report for exploration.

## Technical approach

1. Parse Excel workbook and detect metadata blocks and plate grids.
2. Normalize plate data into tidy table (well identifier, replicate handling).
3. Preprocess and QC: blank subtraction, replicate averaging, flagging outliers and out-of-range values.
4. Fit standard curve (4PL preferred; linear fallback). Compute concentrations and confidence bounds.
5. Export cleaned data and generate visual reports.

## Tech stack (planned)

- Python 3.11+ (virtualenv)
- pandas, openpyxl for parsing
- numpy, scipy (or lmfit) for fits
- matplotlib / seaborn for plotting
- pytest for tests

## Installation (placeholder)

When implemented the repo will include a `requirements.txt`. Example install commands:

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Usage (planned)

Planned command-line scripts (to be added):

- `parse_elisa.py --input exportAll.xlsx --out data.csv` — parse and export tidy table
- `analyze_elisa.py --input data.csv --out report.pdf` — compute concentrations and generate report

## Validation & success criteria

- Correctly parse the provided `exportAll.xlsx` (both Plate 1 and Plate 2 sheets).
- Produce concentrations that match manual calculations for at least one plate with known standards.
- Generate clear QC flags and readable reports.

## Risks & mitigations

- Instrument export variability: implement flexible detection and document supported formats; include example inputs for testing.
- Curve-fitting instability: provide fallback fits and clear warnings; include unit tests.

## Deliverables

- `README.md` (this proposal)
- Scripts to parse and analyze ELISA exports
- Example outputs (CSV, PNG/PDF) derived from `example_input/exportAll.xlsx`
- Tests and installation instructions

---
This proposal was prepared for the WIS Python course project and links to the course repository: https://github.com/Code-Maven/wis-python-course-2026-03
