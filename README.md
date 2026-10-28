![Data Cleaning Template](assets/banner.svg)

# Data Cleaning Template

**A reusable pandas workflow that turns a messy table into analysis-ready data in 10 documented steps, and leaves a before/after quality report every time it runs.**

![Python](https://img.shields.io/badge/Python-1F4E79?style=flat-square&logo=python&logoColor=white) ![pandas](https://img.shields.io/badge/pandas-1F4E79?style=flat-square&logo=pandas&logoColor=white) ![Jupyter](https://img.shields.io/badge/Jupyter-1F4E79?style=flat-square&logo=jupyter&logoColor=white) ![Data Quality](https://img.shields.io/badge/Data_Quality-1F4E79?style=flat-square)

---

## Business problem

Most analysis time goes into cleaning, and most cleaning is repeated from scratch. This template gives every new dataset the same, auditable sequence of checks, so results are faster to produce and easier to trust.

## Approach

The notebook `notebooks/data_cleaning_template.ipynb` runs these steps in order, each with a short explanation:

1. Load the raw file and keep an untouched copy
2. Inspect: shape, data types, missing values, duplicates, summary statistics
3. Remove duplicate rows
4. Standardize column names
5. Clean monetary columns (strip `$` and `,`, convert to numbers)
6. Handle missing values, with the reason for each choice written down
7. Standardize text columns (whitespace, casing)
8. Remove invalid values (negative amounts and rankings)
9. Create derived columns
10. Validate, write a before/after quality report, and export to CSV and Excel

## Key findings (demo dataset)

The demo uses a 20-row table of the highest-grossing concert tours, chosen because it has typical web-table problems: currency symbols, footnote markers and mixed types.

| Metric | Before | After |
|---|---:|---:|
| Rows | 20 | 20 |
| Missing cells | 25 | 2 |
| Numeric columns | 2 | 7 |
| Text columns | 9 | 5 |
| Duplicate rows | 0 | 0 |

The 2 remaining missing values are in `Actual_gross`, where the source value could not be read as a number. They are left blank on purpose rather than guessed, and flagged for review.

The report is saved to [`reports/data_quality_summary.csv`](reports/data_quality_summary.csv).

## How to use it on your own data

```bash
git clone https://github.com/juliocezarcarneiro/data-cleaning-template.git
cd data-cleaning-template
pip install -r requirements.txt
jupyter notebook notebooks/data_cleaning_template.ipynb
```

1. Put your raw file in `data/` and change `file_path` in the loading cell.
2. Update the column lists in steps 4 to 8 (`money_cols`, `text_cols`, the rename list) to match your data.
3. Write your own reason next to each missing-value rule.
4. Run all cells. Check `reports/data_quality_summary.csv` before you use the output.

**Good practice:** never overwrite `data/dirty-data-original.csv`; version cleaned outputs instead of replacing them.

## Folder structure

```text
data-cleaning-template/
├── data/
│   ├── dirty-data-original.csv   # raw input (never edited)
│   ├── cleaned_data.csv          # cleaned output
│   └── cleaned_data.xlsx         # cleaned output for Excel users
├── notebooks/
│   └── data_cleaning_template.ipynb
├── reports/
│   └── data_quality_summary.csv  # before/after quality report
└── assets/                       # banner
```

**Demo data source:** Wikipedia, "List of highest-grossing concert tours" (CC BY-SA).

## Contact

**Julio Carneiro** · Data Analyst · Toronto, ON
[LinkedIn](https://www.linkedin.com/in/juliocezarcarneiro/) · [Portfolio](https://github.com/juliocezarcarneiro) · [Email](mailto:juliocezarcarneiro@outlook.com)
