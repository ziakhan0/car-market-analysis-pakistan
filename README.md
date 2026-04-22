# 🚗 PakWheels Used Car Market — Exploratory Data Analysis

> *A complete end-to-end EDA pipeline on Pakistan's largest used car marketplace.*

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?logo=pandas)](https://pandas.pydata.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter)](https://jupyter.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

---

## 📌 Overview

This project performs a thorough **Exploratory Data Analysis (EDA)** on the
[PakWheels Used Car Dataset (October 2022)](https://www.kaggle.com/datasets/muhammadwaqargul/pakwheels-used-car-dataset-october-2022)
from Kaggle. Raw listing data is cleaned, standardised, and visualised to uncover
meaningful trends in Pakistan's pre-owned car market.

---

## 🎯 Objectives

- ✅ Load and inspect raw listing data
- ✅ Convert price text (`lakh` / `crore`) into numeric PKR values
- ✅ Clean mileage and engine capacity fields
- ✅ Handle missing values strategically (drop critical / impute non-critical)
- ✅ Standardise inconsistent categorical labels
- ✅ Visualise distributions, proportions, and inter-feature relationships
- ✅ Export a clean, analysis-ready dataset

---

## 📁 Project Structure

```
pakwheels-eda/
│
├── pakwheels_eda.ipynb        # Main Jupyter notebook (full pipeline)
├── pakwheels.csv              # Raw dataset (download from Kaggle)
├── pakwheels_cleaned.csv      # Output: cleaned dataset
│
├── plots/                     # Auto-saved visualisations
│   ├── plot_distributions.png
│   ├── plot_categorical.png
│   ├── plot_pie.png
│   ├── plot_price_by_category.png
│   ├── plot_body_transmission.png
│   ├── plot_price_mileage.png
│   ├── plot_model_year.png
│   └── plot_correlation.png
│
└── README.md
```

---

## 🛠️ Technologies

| Library | Purpose |
|---------|---------|
| `pandas` | Data loading, cleaning, manipulation |
| `numpy` | Numerical operations |
| `matplotlib` | Base plotting |
| `seaborn` | Statistical visualisations |
| `scipy` | Pearson correlation significance test |

---

## 📊 Pipeline Walkthrough

### 1 · Data Loading
```python
df = pd.read_csv('pakwheels.csv')
df.drop(columns=[c for c in df.columns if 'Unnamed' in c], inplace=True)
```

### 2 · Price Cleaning
Raw prices are strings like `"10 lakh"` or `"1.5 crore"`.
A custom `parse_price()` function converts them to numeric PKR:

| Input | Output (PKR) |
|-------|-------------|
| `10 lakh` | `1,000,000` |
| `1.5 crore` | `15,000,000` |
| `850,000` | `850,000` |

### 3 · Mileage & Engine Cleaning
- `"45,000 km"` → `45000.0`
- `"1300 cc"` → `1300.0`

### 4 · Missing Value Strategy

| Column Type | Strategy |
|-------------|---------|
| Critical fields (`location`, `mileage`, `transmission`, etc.) | Drop rows |
| Numerical columns | Fill with **median** |
| Categorical columns | Fill with **mode** |

### 5 · Standardisation
```python
df['assembly'] = df['assembly'].replace('Imported Cars', 'Imported')
df['car_age']  = 2022 - df['model_year']   # derived feature
```

---

## 📈 Visualisations

| Plot | What it shows |
|------|--------------|
| **Distribution histograms** | Price, mileage, engine cc, car age — with median lines |
| **Horizontal bar charts** | Top categories per feature (engine type, body type, colour…) |
| **Pie charts** | Proportional split for transmission, assembly, engine type |
| **Box plots** | Price spread broken down by transmission, assembly, body type |
| **Scatter + regression** | Price vs mileage with Pearson r and p-value annotation |
| **Line chart** | Median listing price trend across model years |
| **Correlation heatmap** | Pairwise correlation between all numerical features |
| **Stacked bar** | Body type vs transmission (absolute + percentage) |

---

## 💡 Key Insights

1. **Automatics cost more** — Automatic transmission cars command a clear price premium.
2. **Imported vs Local** — Local-assembled cars dominate volume; imports skew higher in price.
3. **Petrol rules, hybrids rising** — Petrol is most common; hybrid share climbs sharply post-2018.
4. **Mileage hurts value** — Negative Pearson correlation between mileage and price is statistically significant.
5. **Newer = Pricier** — Median price rises steeply for post-2015 models.
6. **SUVs lead on price** — Despite lower listing volume, SUVs have the highest median resale value.

---

## 🚀 Quick Start

### 1. Clone / download the repo
```bash
git clone https://github.com/your-username/pakwheels-eda.git
cd pakwheels-eda
```

### 2. Install dependencies
```bash
pip install pandas numpy matplotlib seaborn scipy jupyterlab
```

### 3. Add the dataset
Download `pakwheels.csv` from [Kaggle](https://www.kaggle.com/datasets/muhammadwaqargul/pakwheels-used-car-dataset-october-2022)
and place it in the project root.

### 4. Run the notebook
```bash
jupyter notebook pakwheels_eda.ipynb
```
Or run all cells from the terminal:
```bash
jupyter nbconvert --to notebook --execute pakwheels_eda.ipynb
```

---

## 👤 Author

**Zia Rehman**

---

*Dataset credit: [Muhammad Waqar Gul](https://www.kaggle.com/muhammadwaqargul) — Kaggle*
