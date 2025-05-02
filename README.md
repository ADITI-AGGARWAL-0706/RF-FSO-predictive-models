
# Developing Predictive Models for Hybrid RF/FSO Systems under Varied Weather Conditions

This repository contains the full pipeline for building, comparing, and evaluating predictive models to estimate RF and FSO signal attenuation under a variety of weather conditions. The project leverages machine learning techniques—specifically Random Forest regression—to create robust, weather-adaptive hybrid communication models. Both generic and weather-specific models were evaluated in Part A, while Part B introduced enhanced modeling techniques that incorporate interdependent signal prediction.

## Table of Contents
1. Introduction  
2. Dataset Description  
3. Project Workflow  
4. Code Structure  
5. Results Summary  
6. Installation and Usage  
7. Future Enhancements  

## 1. Introduction

Hybrid RF/FSO communication systems are highly sensitive to atmospheric conditions. The objective of this project is to develop machine learning models that can accurately predict signal attenuation for both RF and FSO links under a range of environmental scenarios—such as fog, rain, dust, snow, and more.

**Part A:** I implemented and compared two baseline approaches:  
- **Generic Model:** A single Random Forest trained on the full dataset.  
- **Specific Models:** Seven Random Forest models trained on data subsets based on weather conditions (SYNOP codes).  

**Part B:** I introduced two advanced models that integrate predictions between RF and FSO domains:  
- **RF-Enhanced FSO Model:** Uses predicted RF attenuation as an input to improve FSO attenuation prediction.  
- **FSO-Enhanced RF Model:** Uses predicted FSO attenuation to enhance RF attenuation modeling.  

These methods aimed to better preserve correlation structures and mutual information between the signal types, resulting in improved model performance.

## 2. Dataset Description

The dataset consists of 27 meteorological features along with RF and FSO attenuation values.

**Target Variables:**  
- `RFL_Att`: RF signal attenuation  
- `FSO_Att`: FSO signal attenuation  

**Weather Classification (SYNOP Codes):**  
- `0`: Clear  
- `3`: Dust Storm  
- `4`: Fog  
- `5`: Drizzle  
- `6`: Rain  
- `7`: Snow  
- `8`: Showers  

**Splits:**  
- Training Set: Used to build and tune models  
- Test Set: Used for performance evaluation  

## 3. Project Workflow

**Step 1: Data Preprocessing**  
- Data cleaned and standardized  
- Subsets generated per SYNOP category  
- Target columns (`RFL_Att`, `FSO_Att`) identified  

**Step 2: Feature Selection**  
- OOB (Out-of-Bag) feature importance used  
- Features removed iteratively  
- Performance tracked via RMSE and R²  

**Step 3: Model Building**  
- Generic Model trained on entire dataset  
- Specific Models trained per SYNOP weather category  
- RF-Enhanced FSO Model: RF predictions used to assist FSO model  
- FSO-Enhanced RF Model: FSO predictions used to assist RF model  

**Step 4: Hyperparameter Tuning**  
- Grid search with cross-validation was used to find optimal parameters:  
  - `n_estimators`: [50, 100, 150, 200]  
  - `max_depth`: [5, 10, 20, None]  
  - `min_samples_split`: [2, 5, 10]  
  - `max_features`: ['sqrt', 'log2', None]  

## 4. Code Structure

```
Hybrid-RF-FSO-Modeling/
├── data/
│   └── RFLFSODataFull.csv
├── notebooks/
│   ├── 1_data_preprocessing.ipynb
│   ├── 2_feature_selection.ipynb
│   ├── 3_generic_model.ipynb
│   ├── 4_specific_model.ipynb
│   ├── 5_rf_enhanced_fso.ipynb
│   ├── 6_fso_enhanced_rf.ipynb
│   ├── 7_correlation_heatmaps.ipynb
│   └── 8_results_analysis.ipynb
├── README.md
```

## 5. Results Summary

### Key Observations
- **Generic FSO Model:** Delivered consistent RMSE across weather types; Specific Model performed better in Fog and Snow.
- **Generic RF Model:** Achieved lower RMSE and higher R² than Specific RF models in most conditions.
- **Specific Models:** Strong performance in Clear, Drizzle, and Rain (in terms of R²).

### Visualizations
- RMSE and R² plots for both Generic and Specific models included.
- Comparative graphs across weather conditions provided.

## 6. Installation and Usage

### Requirements
- Python 3.8+  
- Jupyter Notebook  
- Python Libraries: `pandas`, `numpy`, `matplotlib`, `scikit-learn`

### Setup Instructions
```bash
git clone https://github.com/ADITI-AGGARWAL-0706/RF-FSO-predictive-models.git
cd RF-FSO-predictive-models
pip install -r requirements.txt
jupyter notebook
```
Open and execute notebooks sequentially from the `/notebooks` directory.

## 7. Future Enhancements

- Explore advanced feature engineering techniques to improve accuracy.
- Incorporate real-time weather data for dynamic retraining.
- Add additional environmental features to boost prediction robustness.
- Compare other ML models (e.g., XGBoost, neural networks) for extended benchmarking.
