# Predicting Purchase Value from Clickstream Data

<div align="center">
  <img src="https://img.shields.io/badge/Kaggle-Compete-blue?style=for-the-badge&logo=kaggle" alt="Kaggle Competition"/>
  <img src="https://img.shields.io/badge/Python-3.11-blueviolet?style=for-the-badge&logo=python" alt="Python Version"/>
  <img src="https://img.shields.io/badge/XGBoost-Ensemble-orange?style=for-the-badge&logo=xgboost" alt="Model Used"/>
</div>

---

## 📋 Project Objective

The goal of this project is to build a robust regression model that predicts the **`purchaseValue`**—the total amount a customer spends during a session on a large-scale digital commerce platform. By accurately forecasting this value using detailed session-level data, businesses can gain insights into customer intent, optimize marketing campaigns, and improve resource allocation.

The model is trained on a comprehensive dataset that includes user behavior metrics, device attributes, traffic sources, and geographical information.

---

## ✨ Key Features & EDA Insights

This project follows a structured approach, starting with Exploratory Data Analysis (EDA) and leading to a robust modeling pipeline.

### 1. **Exploratory Data Analysis (EDA)**
   - **Target Distribution**: The `purchaseValue` is extremely right-skewed, with most sessions having zero or low purchase values. This indicates that high-value purchases are rare but significant.
   - **Feature Correlation**: `totalHits`, `pageViews`, and `sessionNumber` show the highest positive (but moderate) correlation with `purchaseValue`.
   - **Redundancy**: `totalHits` and `pageViews` are almost perfectly correlated (0.99), suggesting one can be removed to avoid multicollinearity.
   - **Categorical Insights**: The average purchase value varies significantly by `geoNetwork.continent`, and the `browser` type shows a highly concentrated distribution.

### 2. **Data Preprocessing & Feature Engineering**
   - **Missing Values**: Features with over 60% missing values were dropped to reduce noise. Remaining numerical NaNs were imputed with the median.
   - **Feature Transformation**:
     - **Date Features**: The `date` column was converted to extract `dayofweek` and `month` to capture temporal patterns.
     - **Mean Encoding**: High-cardinality features like `userId` and `browser` were safely mean-encoded based on the training set's `purchaseValue` to create powerful predictive signals.
     - **Frequency Encoding**: Other categorical features were encoded by their frequency to convert them into a numerical format.
   - **Feature Creation**:
     - **Interaction Features**: New features were created by combining `pageViews`, `totalHits`, and `sessionNumber` (e.g., `pageViews_per_session`) to capture non-linear relationships.
     - **User Aggregates**: User-level statistics (mean, sum, count) for key metrics were generated to model habitual behavior across sessions.
   - **Scaling**: All numerical features were standardized using `StandardScaler` to bring them to a similar scale.

### 3. **Modeling and Evaluation**
   - **Model Selection**: Three tree-based models were evaluated: **XGBoost**, **LightGBM**, and **Random Forest**.
   - **Ensembling**: To improve robustness and reduce variance, an ensemble of 5 `XGBRegressor` models was trained, each with a different random seed.
   - **Validation Strategy**: The data was split into training (80%) and validation (20%) sets to evaluate model performance on unseen data.

---

## 🛠️ Tech Stack & Libraries

| Category             | Technology / Library                                                                                                                                                                                                                                 |
| :------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Data Manipulation** | ![NumPy](https://img.shields.io/badge/NumPy-013243?style=flat&logo=numpy&logoColor=white) `NumPy`, ![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white) `Pandas`                                                 |
| **Data Visualization** | ![Matplotlib](https://img.shields.io/badge/Matplotlib-3776AB?style=flat&logo=matplotlib&logoColor=white) `Matplotlib`, ![Seaborn](https://img.shields.io/badge/Seaborn-3776AB?style=flat&logo=seaborn&logoColor=white) `Seaborn`                       |
| **Machine Learning** | ![Scikit-learn](https://img.shields.io/badge/Scikit--learn-F7931A?style=flat&logo=scikit-learn&logoColor=white) `Scikit-learn`, ![XGBoost](https://img.shields.io/badge/XGBoost-0066CC?style=flat&logo=xgboost&logoColor=white) `XGBoost`, `LightGBM` |



## 🚀 How to Run

1. **Clone the repository**:
   ```sh
   git clone [https://github.com/your-username/your-repo-name.git](https://github.com/your-username/your-repo-name.git)
   cd your-repo-name
