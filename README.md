# Turbofan Engine Remaining Useful Life (RUL) Prediction
**An End-to-End Predictive Maintenance Framework Built with Python and Machine Learning**

---

## 📌 Project Objective
This project transition industrial asset maintenance from traditional periodic or reactive intervals into a real-time, data-driven predictive strategy. Utilizing multivariate time-series sensor telemetry from the **NASA C-MAPPS (FD001)** dataset, this framework builds and evaluates machine learning regressors to accurately predict the Remaining Useful Life (RUL) of jet engine turbofans before operational degradation turns into catastrophic failure.

## 🛠️ Tech Stack & Libraries
- **Language:** Python
- **Data Engineering:** Pandas, NumPy
- **Visualization:** Matplotlib, Seaborn, Plotly
- **Machine Learning:** Scikit-Learn (Random Forest Regressor, K-Nearest Neighbors)

## 📊 Methodology & Key Architecture
1. **Data Preprocessing & Signal Cleaning:** Analyzed summary statistics across 21 sensors to isolate and drop zero-variance flatline signals (`op_setting_3`, and sensors `1`, `5`, `10`, `16`, `18`, `19`). This eliminated computational noise.
2. **Target Engineering:** Calculated true RUL for the training set based on run-to-failure cycle countdowns, and dynamically anchored truncated test records against external ground-truth validation matrices.
3. **Model Selection:** Built and evaluated a distance-based baseline algorithm (KNN) against a robust ensemble bagging architecture (Random Forest Regressor).

## 🏆 Model Performance & Evaluation
- **Primary Metric:** Root Mean Squared Error (RMSE) was prioritized over MAE to heavily penalize large errors, as underpredicting or overpredicting engine degradation introduces extreme asset safety risks.
- **Results:** The **Random Forest Regressor** significantly outperformed the baseline KNN model by successfully mitigating high-dimensional sensor noise spikes through tree-based voting aggregation.

## 🔍 Strategic Insights & Engineering Recommendations
* **Core Sensor Dominance:** Feature importance (Gini weights) reveals that a small subset of channels—specifically tracking **thermal stress (exhaust gas temperature)** and **rotational speed dynamics (high-pressure compressor speed)**—serve as the primary leading indicators of engine wear.
* **Operational Trigger Framework:** The model supports a three-tiered automated alerting protocol:
  - 🟢 **Green Flag (RUL > 50 Cycles):** Normal operations.
  - 🟡 **Yellow Flag (RUL 21–50 Cycles):** Schedule maintenance during the next routine stopover; pre-order wear parts.
  - 🔴 **Red Flag (RUL ≤ 20 Cycles):** Ground the asset immediately to avoid catastrophic Inflight Shutdown (IFSD).
* **Next-Stage Optimization:** Future iterations will transition to a **Piecewise Linear RUL target** (capping early target cycles at 125/130) to prevent early-lifecycle model overfitting before active system degradation begins.

---
*Developed by Samson Mayomi Matthew* *Contact: samson.m.matthew@gmail.com*