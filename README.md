# AMES-Housing-Price-Project
This project covers the processes of missing data handling, data cleaning, modeling, and interactive visualization (Dash Dashboard) on the Ames Housing Dataset.
The project begins with a deterministic (reproducible) and optimized data cleaning pipeline, followed by multicollinearity (VIF) elimination, linear regression model construction, and model performance visualization.


> ⚠️ **Important Note**
> 1. This project was developed **for learning purposes** and will be **revised in future versions**.  
> 2. The dataset was obtained from **Kaggle’s [Ames Housing Dataset](https://www.kaggle.com/datasets/shashanknecrothapa/ames-housing-dataset)**.


## 🎯 Project Objectives

- To address the missing data problem in a systematic and reliable way  
- To design a deterministic (reproducible) data cleaning pipeline  
- To develop a linear regression model that predicts housing prices based on the Ames Housing dataset  
- To statistically validate the model assumptions  
- To visualize exploratory data analysis (EDA) and model results through a user-friendly, Dash-based interactive dashboard


## 🧩 Analysis Steps

### 0️⃣ Deterministic Environment Setup
- Randomness is controlled to ensure reproducible results by fixing `random`, `numpy`, and `PYTHONHASHSEED` with (`SEED=42`).

### 1️⃣ Required Libraries
- Main libraries used:
  - `pandas`, `numpy`
  - `sklearn` (IterativeImputer, OrdinalEncoder, LinearRegression, etc.)
  - `plotly`, `dash` (for visualization and dashboard)
  - `statsmodels` (for VIF and Durbin–Watson test)

### 2️⃣ Data Loading
- The `AmesHousing.csv` file is loaded.  
- Column names are cleaned (spaces and special characters are removed).

### 3️⃣ Missing Data Summary
- The number and percentage of missing values are calculated for each variable.  
- The missing data summary table (`missing_df`) is printed to the terminal.

### 4️⃣ Missing Value Indicators
- For each column with missing values, a binary flag column named `*_was_missing` is created  
  (0: not missing, 1: was missing).

### 5️⃣ Structural Missing (Categorical) Filling
- Structural categorical missing values (`Pool_QC`, `Alley`, `Fence`, `Garage_*`, `Bsmt_*`, etc.) are filled with `"None"`.

### 6️⃣ Numeric & Categorical Column Separation
- Numeric and categorical variables are separated using `select_dtypes()`.

### 7️⃣ Numeric Missing Value Imputation (MICE)
- Numeric missing values are filled using `IterativeImputer` (MICE method).  
- The process is **deterministic** (reproducible) with `random_state=SEED`.

### 8️⃣ Categorical Missing Value Imputation (Mode)
- Missing values in categorical columns are filled with the **most frequent value (mode)**.

### 9️⃣ Encoding Categorical Variables
- Categorical variables are encoded into numeric values using `OrdinalEncoder`.  
- Unknown categories are assigned `unknown_value=-1`.

### 🔟 Saving the Clean Data
- The processed dataset is saved as `AmesHousing_Clean.csv`.

---

## 🧠 Modeling and Statistical Controls

### 1️⃣ VIF (Variance Inflation Factor) Cleaning
- Multicollinearity is checked among features.  
- Variables with VIF values above 10 are iteratively removed.  
- The cleaned dataset is stored in `X_vif_clean`.

### 2️⃣ Model Construction
- Model pipeline: **RobustScaler + LinearRegression**  
- Target variable: `SalePrice`  
- Dataset split: **80% train**, **20% test**.

### 3️⃣ Durbin–Watson Test
- **Durbin–Watson statistic** is calculated to measure residual independence.  
- If 1.5 < DW < 2.5, autocorrelation is considered absent.

### 4️⃣ Model Evaluation
- **RMSE** and **R²** metrics are calculated on the test set.  
- Predicted prices are stored as a new column named `Predicted_Price`.

---

## 📊 Dash Dashboard Structure

### Tabs:
- **📊 Exploratory Data Analysis (EDA):**
  - Interactive visualizations with filters for Neighborhood, Kitchen Quality, and SalePrice  
  - Includes Scatter, Boxplot, and Histogram charts

- **🤖 Model & Prediction:**
  - Comparison of actual vs predicted prices  
  - Analysis with the same filter options as EDA

### Components Used:
- `dcc.Dropdown` → filter selection  
- `dcc.RangeSlider` → price range selection  
- `dcc.Graph` → interactive Plotly visualizations  

---

## 💾 Outputs

- ✅ Cleaned dataset: `AmesHousing_Clean.csv`  
- ✅ Model results (RMSE, R², and DW values printed in the terminal)  
- ✅ Interactive web application (Dash Dashboard)


