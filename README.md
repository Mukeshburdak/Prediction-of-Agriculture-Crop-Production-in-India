# 🌾 Prediction of Agriculture Crop Production in India

![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python&logoColor=white)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-ML-orange?logo=scikit-learn&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?logo=pandas&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-11557C)
![License](https://img.shields.io/badge/License-MIT-green)
![Status](https://img.shields.io/badge/Status-Internship%20Project-yellow)

> A machine learning project to predict crop yield (Quintal/Hectare) across Indian states using cultivation cost data from 2001–2014. Three regression algorithms are compared — **Linear Regression**, **Random Forest**, and **Gradient Boosting** — with Gradient Boosting achieving the highest accuracy (**R² = 0.943**).

---

## 📌 Table of Contents

- [Project Overview](#-project-overview)
- [Dataset Description](#-dataset-description)
- [Project Structure](#-project-structure)
- [ML Algorithms Used](#-ml-algorithms-used)
- [Results](#-results)
- [Visualizations](#-visualizations)
- [Installation](#-installation)
- [How to Run](#-how-to-run)
- [Sample Prediction](#-sample-prediction)
- [Technologies Used](#-technologies-used)
- [Acknowledgements](#-acknowledgements)

---

## 📖 Project Overview

India is the world's second-most populous country with over **1.3 billion people**, and agriculture is the backbone of its economy. This project uses real crop cultivation and production data to:

- Analyze crop yield patterns across Indian states
- Identify the impact of cultivation costs on yield
- Build and compare ML models to **predict crop yield**
- Help farmers and policymakers make data-driven decisions

---

## 📂 Dataset Description

**Source:** [data.gov.in](https://data.gov.in/) — Fully Licensed  
**Coverage:** Indian Agriculture Data, 2001–2014

| File | Description | Rows |
|------|-------------|------|
| `datafile__1_.csv` | Crop-wise cost of cultivation & yield by state | 49 |
| `datafile__2_.csv` | Production, area & yield index (2006–2011) | 55 |
| `produce.csv` | Agricultural production time-series | 429 |
| `datafile.csv` | Year-wise crop production index | — |
| `datafile__3_.csv` | Crop variety & recommended zone info | — |

### Key Columns (Primary Dataset)

| Column | Type | Description |
|--------|------|-------------|
| `Crop` | String | Crop name (e.g., ARHAR, WHEAT, PADDY) |
| `State` | String | Indian state where cultivated |
| `Cost of Cultivation A2+FL` | Float | Paid-out cost + family labour (₹/Hectare) |
| `Cost of Cultivation C2` | Float | Comprehensive cost (₹/Hectare) |
| `Cost of Production C2` | Float | Production cost per quintal (₹/Quintal) |
| `Yield (Quintal/Hectare)` | Float | **Target variable** |

**Crops Covered:** ARHAR, COTTON, GRAM, GROUNDNUT, MAIZE, MOONG, PADDY, RAPESEED & MUSTARD, SUGARCANE, WHEAT  
**States Covered:** 13 major Indian agricultural states

---

## 📁 Project Structure

```
agriculture-crop-prediction/
│
├── data/
│   ├── datafile__1_.csv        # Cost & yield dataset (primary)
│   ├── datafile__2_.csv        # Production index dataset
│   ├── datafile__3_.csv        # Crop variety info
│   ├── datafile.csv            # Year-wise index
│   └── produce.csv             # Time-series production data
│
├── agriculture_ml.py           # Main ML script
├── requirements.txt            # Python dependencies
└── README.md
```

---

## 🤖 ML Algorithms Used

### 1. 📉 Linear Regression *(Baseline)*
A simple approach to model the linear relationship between cultivation costs and yield. Used as a baseline to compare against ensemble methods.

### 2. 🌲 Random Forest Regressor
An ensemble of **200 decision trees** trained on random subsets of data and features. Robust to outliers and captures non-linear patterns effectively.

```python
RandomForestRegressor(n_estimators=200, max_depth=10, random_state=42)
```

### 3. 🚀 Gradient Boosting Regressor *(Best Model)*
Sequentially builds **300 weak learners**, each correcting the errors of the previous. Delivers the highest accuracy in this project.

```python
GradientBoostingRegressor(n_estimators=300, learning_rate=0.05,
                           max_depth=4, subsample=0.8, random_state=42)
```

---

## 📊 Results

| Model | MAE | RMSE | R² Score | CV R² (5-Fold) |
|-------|-----|------|----------|----------------|
| Linear Regression | 116.76 | 140.98 | 0.780 | -23.30 |
| Random Forest | 29.22 | 74.05 | 0.939 | 0.559 |
| **Gradient Boosting** ⭐ | **25.97** | **72.00** | **0.943** | **0.862** |

> **🏆 Best Model: Gradient Boosting** with R² = 0.943 and CV R² = 0.862

### Metric Definitions
- **MAE** — Mean Absolute Error (lower is better)
- **RMSE** — Root Mean Squared Error (lower is better)
- **R²** — Coefficient of Determination (closer to 1 is better)
- **CV R²** — Average R² over 5 cross-validation folds (tests generalization)

---

## 📈 Visualizations

The script generates a **9-panel figure** displayed inline in Jupyter and saved as `agriculture_ml_results.png`:

| # | Plot | Description |
|---|------|-------------|
| 1 | R² Score Comparison | Bar chart of all 3 models |
| 2 | MAE vs RMSE | Grouped error comparison |
| 3 | 5-Fold CV R² | Cross-validation generalization |
| 4 | RF: Actual vs Predicted | Scatter with perfect-fit line |
| 5 | GB: Actual vs Predicted | Scatter with perfect-fit line |
| 6 | Feature Importance | Random Forest feature ranking |
| 7 | Avg Yield by Crop | Horizontal bar chart |
| 8 | Cost vs Yield Scatter | Colored by crop type |
| 9 | Residual Plot | Gradient Boosting error distribution |

---

## ⚙️ Installation

```bash
# 1. Clone the repository
git clone https://github.com/your-username/agriculture-crop-prediction.git
cd agriculture-crop-prediction

# 2. (Optional) Create a virtual environment
python -m venv venv
source venv/bin/activate        # macOS/Linux
venv\Scripts\activate           # Windows

# 3. Install dependencies
pip install -r requirements.txt
```

**`requirements.txt`**
```
pandas
numpy
matplotlib
seaborn
scikit-learn
```

---

## ▶️ How to Run

### Option A — Jupyter Notebook (Recommended)
```bash
jupyter notebook
# Open agriculture_ml.py or paste code into a new notebook cell
# Plots will render inline automatically when the cell runs
```

### Option B — Google Colab
1. Upload all CSV files to Colab
2. Paste the script into a code cell
3. Run — plots display automatically inline

### Option C — Python Script
```bash
python agriculture_ml.py
# Plot is saved as agriculture_ml_results.png
```

---

## 🔮 Sample Prediction

```python
# Predicting yield for ARHAR crop in Uttar Pradesh
sample = {
    "Crop"                    : "ARHAR",
    "State"                   : "Uttar Pradesh",
    "Cost_A2FL (₹/Hectare)"  : 9794.05,
    "Cost_C2   (₹/Hectare)"  : 23076.74,
    "Cost_Production (₹/Qtl)": 1941.55
}
```

| Model | Predicted Yield | Actual Yield |
|-------|----------------|--------------|
| Random Forest | **9.73** Quintal/Hectare | 9.83 |
| Gradient Boosting | **9.85** Quintal/Hectare | 9.83 |

> Gradient Boosting predicted within **0.02 Quintal/Hectare** of the actual value!

---

## 🛠️ Technologies Used

| Tool | Purpose |
|------|---------|
| `Python 3.8+` | Core programming language |
| `Pandas` | Data loading & manipulation |
| `NumPy` | Numerical computations |
| `Scikit-learn` | ML models, preprocessing, evaluation |
| `Matplotlib` | Plotting & visualization |
| `Seaborn` | Statistical visualizations |
| `Jupyter Notebook` | Interactive development |

---

## 🙏 Acknowledgements

- **Dataset Source:** [data.gov.in](https://data.gov.in/) — Open Government Data Platform India
- **Inspiration:** Solving real-world challenges in Indian agriculture to help over 1.3 billion people dependent on crop production
- Built as part of an **internship project** on Machine Learning for Agricultural Prediction

---

## 📄 License

This project is licensed under the **MIT License** — feel free to use, modify, and distribute.

---

<p align="center">Made with ❤️ for Indian Agriculture | Internship Project 2026</p>
