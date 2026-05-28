# California Housing Price Prediction

## 📌 Project Overview

This project focuses on predicting **median house values** based on block-group demographics and geographic data from the California Housing Dataset.

The aim is to explore **which factors most influence housing prices** and compare multiple machine learning models for regression accuracy.

---

## 📊 Dataset Description

- **Total Records:** 20,640
- **Features:** 8 (Block-group demographics, geography, and housing stats)

### **Block-Group Profile**

| Feature | Description |
|---|---|
| `MedInc` | Median income (in $10,000s) |
| `HouseAge` | Median age of houses (years) |
| `AveRooms` | Average rooms per household |
| `AveBedrms` | Average bedrooms per household |
| `Population` | Total block-group population |
| `AveOccup` | Average household members |
| `Latitude` | Geographic latitude |
| `Longitude` | Geographic longitude |

### **Target Variable**

| Variable | Description |
|---|---|
| `MedHouseVal` | Median house value (in $100,000s), capped at $500,000 |

---

## ⚙️ Data Preprocessing

- **Outlier Treatment**
  - Extreme values in `AveRooms`, `AveBedrms`, `AveOccup`, and `MedHouseVal` were retained — they reflect real-world variability.
  - Tree-based models handle outliers naturally; log transformation was applied for Linear Regression.

- **Log Transformation**
  - Applied on highly skewed features (`AveRooms`, `AveBedrms`, `AveOccup`) to stabilize variance.
  - Original features kept for tree-based models; transformed versions used for Linear Regression.

- **Correlated Features**
  - `Longitude` removed for Linear Regression due to high collinearity with `Latitude`.
  - All features retained for tree-based models.

- **Feature Scaling**
  - `StandardScaler` applied for Linear Regression only.
  - Tree-based models (Decision Tree, Random Forest) do not require scaling.

---

## 🔍 Feature Selection

### **Correlation Analysis**

- **Strongest Predictor:** `MedInc` — highest positive correlation with house value.
- `Latitude` / `Longitude` are highly correlated with each other.
- `AveRooms` is highly correlated with `MedInc`.

### **Random Forest Feature Importance**

- **Top Predictors:** `MedInc`, `Latitude`, `Longitude`
- **Moderate Predictors:** `HouseAge`, `AveRooms`, `AveOccup`
- **Low Predictors:** `Population`, `AveBedrms`

### **Overall Insight**

- **Core Predictors:** `MedInc`, `Latitude`, `Longitude`
- **Supportive Predictors:** `HouseAge`, `AveRooms`, `AveOccup`
- **Weak Predictors:** `Population`, `AveBedrms`

---

## 🤖 Model Implementation

### 1. **Linear Regression**
- Requires scaled + log-transformed features.
- Struggles with non-linear relationships in the data.

### 2. **Decision Tree Regressor**
- No scaling required; handles non-linearity well.
- Prone to overfitting without pruning.

### 3. **Random Forest Regressor**
- Ensemble of decision trees; most robust model.
- Best performance across all metrics.

---

## 📈 Model Comparison

| Metric | Linear Regression | Decision Tree | Random Forest |
|---|---|---|---|
| MAE | Higher | Medium | **Lowest** |
| MSE | Higher | Medium | **Lowest** |
| RMSE | Higher | Medium | **Lowest** |
| R² Score | Lower | Medium | **Highest** |

---

## ✅ Conclusion

- **Random Forest is the best model** → Lowest error and highest R² score.
- **Decision Tree also solid** → Handles non-linearity well but less robust than Random Forest.
- **Linear Regression weakest** → Struggles with skewed features and non-linear patterns.
- **Median Income (`MedInc`) is the most influential feature** in determining house prices.
