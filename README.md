# Drift-Aware Regression Analysis on Gas Sensor Array Data

## Project Description
This project analyzes the impact of temporal sensor drift on regression models using a publicly available gas sensor array dataset. The objective is to study how regression performance changes when models trained on early data batches are applied to later batches collected under drifted conditions, and to evaluate simple mitigation strategies.

The work focuses on understanding regression behavior under distribution shift rather than proposing new algorithms.

---

## Dataset
- **Source:** UCI Machine Learning Repository  
- **Dataset Name:** Gas Sensor Array Drift Dataset at Different Concentrations  
- **Link:** [https://archive.ics.uci.edu/dataset/251/gas+sensor+array+drift+dataset+at+different+concentrations  ](https://archive.ics.uci.edu/dataset/270/gas+sensor+array+drift+dataset+at+different+concentrations)

### Dataset Description
The dataset contains sensor responses from a gas sensor array exposed to different gas types and concentration levels. Data is collected across multiple batches over time, where each batch corresponds to a different acquisition period. This structure makes the dataset suitable for studying temporal drift.

---

## Problem Statement
Regression models trained on earlier sensor data often perform poorly on later data due to sensor drift. This project aims to:
1. Quantify performance degradation across batches  
2. Compare different regression models under drift  
3. Evaluate whether small calibration subsets can improve performance on drifted data  

---

## Methodology

### Data Preparation
- Batch-wise `.dat` files are loaded and parsed
- Sensor features are extracted and converted to numerical form
- Target variable: gas concentration
- Features are standardized using training batch statistics only

### Train–Test Split
- **Training batches:** 1–6  
- **Evaluation batches:** 7–10  

This setup evaluates generalization under temporal distribution shift.

### Models Used
- Linear Regression  
- Random Forest Regressor  
- XGBoost Regressor  

All models are trained on the same standardized training data.

### Evaluation Metrics
- Root Mean Squared Error (RMSE)  
- Mean Absolute Error (MAE)  
- R² score  

Metrics are reported batch-wise to observe drift effects.

---

## Drift Analysis and Visualization
- Principal Component Analysis (PCA) is applied to selected batches
- 2D projections are used to visualize feature drift over time
- Separation between batches indicates temporal changes in sensor behavior

---

## Drift Mitigation Approach
A simple calibration-based correction is tested:
- A small subset of samples from each test batch is used for recalibration
- Models are retrained using original training data plus calibration samples
- Performance before and after calibration is compared

---

## Results Summary
- Regression performance degrades on later batches due to drift
- Tree-based models outperform linear regression but still show degradation
- PCA confirms systematic batch-wise feature drift
- Small-batch calibration reduces prediction error on drifted batches

---

## Repository Structure
