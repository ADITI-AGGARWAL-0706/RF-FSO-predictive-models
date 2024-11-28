# Developing Predictive Models for Hybrid RF/FSO Systems under Varied Weather Conditions

This repository contains the Jupyter Notebook code and data used for our research on developing and comparing Generic and Specific Random Forest models for predicting RF and FSO channel attenuation under various weather conditions.

Table of Contents
    1.Introduction
    2.Dataset Description
    3.Project Workflow
    4.Code Structure
    5.Results Summary
    6.Installation and Usage
    7.Future Enhancements

1.Introduction

Hybrid RF/FSO communication systems are highly sensitive to environmental conditions. This project aims to improve the accuracy of attenuation predictions by     leveraging Machine Learning models. We implemented and evaluated two approaches:
    1.Generic Model: A single Random Forest trained on the entire dataset.
    2.Specific Model: Seven Random Forest models trained on weather-specific subsets of the dataset.
The primary focus is to compare the predictive performance of these models across various environmental conditions, including Clear Weather, Dust Storm, Fog,     Drizzle, Rain, Snow, and Showers.

2.Dataset Description
The dataset includes 27 features derived from weather parameters and RF/FSO attenuation values:
    -Target Variables: RFL_Att (RF attenuation) and FSO_Att (FSO attenuation).
    -Weather Conditions: Categorized using SYNOP codes:
      - Clear Weather (0), Dust Storm (3), Fog (4), Drizzle (5), Rain (6), Snow (7), Showers (8).

For preprocessing, the dataset was split into:
    -Training Dataset: Used to train Generic and Specific models.
    -Test Dataset: Used to validate and calculate RMSE and R2R2.

3.Project Workflow
Step 1: Data Preprocessing

    -Data was cleaned and standardized.
    -Subsets were created for each weather condition using SYNOP codes.
    -Target columns (RFL_Att and FSO_Att) were identified.

Step 2: Feature Selection

    -A feature importance ranking algorithm was applied using Out-of-Bag (OOB) scores.
    -Features were iteratively removed based on importance, and RMSE and R2R2 were recorded at each step.

Step 3: Model Creation

    1.Generic Model: A single Random Forest model trained on the entire dataset.
    2.Specific Model: Separate Random Forest models for each weather condition, trained on respective subsets.

Step 4: Model Evaluation

    -Performance was evaluated using RMSE and R2R2 metrics for both Generic and Specific models.
    -Comparative analysis highlighted strengths and weaknesses across weather conditions.

4.Code Structure

Hybrid-RF-FSO-Modeling
├── data/
│   ├── RFLFSODataFull.csv         
├── notebooks/
│   ├── 1_data_preprocessing.ipynb 
│   ├── 2_feature_selection.ipynb 
│   ├── 3_generic_model.ipynb     
│   ├── 4_specific_model.ipynb     
│   ├── 5_results_analysis.ipynb  
├── README.md                      

5.Results Summary
Key Observations

    -Generic FSO Model: Delivered consistently better RMSE across most weather conditions, except Fog and Snow, where the Specific Model performed better.
    -Generic RF Model: Achieved lower RMSE and higher R2R2 compared to Specific RF models across all weather conditions.
    -Specific Models: Excelled in Clear Weather, Drizzle, and Rain conditions for R2R2.

Visualizations

    -RMSE and R2R2 plots for both Generic and Specific models are included in the results notebook.
    -Comparative graphs illustrate performance across weather conditions.

6.Installation and Usage
Requirements

    Python 3.8+
    Jupyter Notebook
    Libraries:
        pandas
        numpy
        matplotlib
        sklearn

Steps to Run

1.Clone the repository:
git clone https://github.com/your_username/Hybrid-RF-FSO-Modeling.git
cd Hybrid-RF-FSO-Modeling

2.Install required Python libraries:
pip install -r requirements.txt

3.Run Jupyter Notebook:
jupyter notebook

4.Open the notebooks in the /notebooks folder and execute them sequentially.

7.Future Enhancements

Future work can focus on:

    -Exploring advanced feature engineering techniques to improve model accuracy.
    -Incorporating real-time weather data for dynamic model retraining and prediction.
    -Extending the approach to include additional environmental parameters for enhanced predictive capability.
    -Comparing other machine learning models to evaluate their performance in this scenario.
