# 🧹 Data Cleaning Project

An end-to-end data cleaning and exploratory visualization workflow built with **Python, Pandas and Matplotlib**. The notebook takes a raw employee dataset with missing values, duplicates, inconsistent text and salary outliers, and turns it into a clean, analysis-ready CSV.

**Author:** Thiraviaraj R

---

## 📂 Repository Structure

```
├── CleaningData_ThiraviarajR.ipynb                                   # Main notebook (cleaning + visualization)
├── sample_data_cleaning_project - Sample_data_cleaning_project.csv   # Raw input dataset
├── Cleaneddataset.csv                                                # Cleaned output dataset
└── README.md
```

## 📊 Dataset

Employee records with the following columns:

| Column       | Description                           | Type (raw) |
|--------------|---------------------------------------|------------|
| `Name`       | Employee name                         | string     |
| `Age`        | Employee age (has missing values)     | float      |
| `Salary`     | Annual salary (missing values + outliers) | float  |
| `Join_Date`  | Date of joining (`M/D/YYYY` strings)  | string     |
| `Department` | HR / Finance / IT                     | string     |

The raw file has **43 rows**, with **4 missing `Age`** and **7 missing `Salary`** values.

## 🔧 Cleaning Pipeline

| Step | Task | Approach |
|------|------|----------|
| 1 | Load data | `pd.read_csv()` |
| 2 | Detect missing values | `data.isnull().sum()` |
| 3 | Handle missing values | `Age` → filled with **median**; `Salary` → filled with **mean**; rows with null `Join_Date` dropped |
| 4 | Standardize text | Strip whitespace and convert all text columns to lowercase |
| 5 | Remove duplicates | `drop_duplicates(subset=['Name', 'Age'])`, verified with `data.duplicated().sum()` (= 0) |
| 6 | Handle outliers | **IQR method** on `Salary` (keep values within `Q1 − 1.5·IQR` and `Q3 + 1.5·IQR`) |
| 7 | Fix data types | `Join_Date` converted to `datetime64` using `pd.to_datetime()` |
| 8 | Encode categoricals | One-hot encoding of `Department` with `pd.get_dummies(drop_first=True)`, cast to integers |
| 9 | Export | Saved to `Cleaneddataset.csv` |

**Result:** 43 raw rows → 29 clean rows, with no missing values, no duplicates, and consistent formatting.

## 📈 Visualizations

After cleaning, the notebook reloads `Cleaneddataset.csv` and plots:

- **Bar chart**: Department distribution (HR vs IT)
- **Histogram**: Salary distribution
- **Line plot**: Salary vs Age
- **Scatter plot**: Salary vs Age, colour-coded by department

## 🚀 Getting Started

### Prerequisites

- Python 3.8+
- pandas
- matplotlib
- Jupyter Notebook / JupyterLab

### Installation

```bash
git clone https://github.com/<your-username>/<your-repo-name>.git
cd <your-repo-name>
pip install pandas matplotlib jupyter
```

### Run

```bash
jupyter notebook CleaningData_ThiraviarajR.ipynb
```

Run the cells top to bottom. Make sure the raw CSV is in the same folder as the notebook.

## 🛠️ Tech Stack

![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?logo=pandas&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557c)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?logo=jupyter&logoColor=white)

## 📝 Notes & Possible Improvements

- Salary is mean-imputed **before** outlier removal, so extreme values (e.g. very large salaries) pull the mean up. Imputing with the **median**, or removing outliers first, would give more realistic fills.
- Duplicates are detected on `Name` + `Age`; adding `Join_Date` or `Department` to the key would make this stricter.
- With `drop_first=True`, **Finance** is the baseline department (encoded as `Department_hr = 0` and `Department_it = 0`).
- Possible extensions: a correlation heatmap, boxplots for outlier visualization, and a reusable cleaning function or script.

## 📬 Contact

**Thiraviaraj R**
B.E. CSE (AI & ML), Rathinam Technical Campus, Coimbatore

---

⭐ If you found this useful, consider giving the repo a star!
