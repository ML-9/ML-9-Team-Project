# ML-9 Team Project
### Evaluating Machine Learning Methods for Reliable Stroke Classification

# Overview

Stroke is one of the leading causes of death and disability worldwide. Early identification of high-risk individuals is crucial, but many datasets—like the commonly used Kaggle *Stroke Prediction Dataset*—exhibit extreme class imbalance, where stroke cases represent only about 5% of samples.

Our project initially aimed to build a stroke prediction model, but as we progressed it became clear that the core challenge was determining **which machine learning method performs most reliably under severe class imbalance**.

To address this, we focused on:

- Cleaning and preprocessing the data
- Augmentating the minority class using SMOTE and related techniques
- Training and evaluating multiple ML and DL models
- Determining which approach provides the **most robust, accurate classification** of stroke vs. non-stroke cases

Our final conclusion: **Random Forest is the most reliable and best-performing method** for this dataset once class imbalance is addressed.

# Stakeholders

### Primary Stakeholders
- **Healthcare providers** – benefit from improved tools for identifying high-risk patients.
- **Public health planners** – gain insights into risk profiles across populations.
- **Patients** – particularly those with cardiovascular disease risk factors.

### Secondary Stakeholders
- **Researchers in medical ML**
- **Healthcare systems**

# Narrative Summary

After reviewing multiple datasets, we selected the Kaggle Stroke Prediction Dataset due to its clinical relevance and rich feature variety.

However, we identified that the dataset suffers from severe class imbalance. To overcome this, we:

1. Cleaned and preprocessed data
2. Applied SMOTE augmentation
3. Trained Logistic Regression, Random Forest, and FCNN models
4. Evaluated with ROC-AUC, recall, F1, and confusion matrices
5. Analyzed feature importance

# Dataset Description

Dataset: https://www.kaggle.com/datasets/fedesoriano/stroke-prediction-dataset

Contains **5110 rows and 11 features** including demographics, comorbidities, lifestyle factors, and the binary stroke target.

# Methodology
We developed a systematic approach to set up and evaluate multiple machine learning methods under severe class imbalance:

## Preprocessing
To begin with, we handled data quality issues:
- BMI median imputation to address missing values
- Encoding categorical variables with one-hot encoding 
- Standardization for neural networks

## Addressing Class Imbalance
Given the extreme class imbalance (only ~5% affirmative stroke cases), we implemented several strategies:
- SMOTE
- Balanced class weights
- Stratified train/test splits

## Models Tested
We evaluated three main models:
- **Logistic Regression** – interpretable baseline
- **Random Forest** – most stable and accurate
- **FCNN** – prone to overfitting due to dataset size

## Evaluation Metrics
The following metrics were used to assess model performance:
- ROC-AUC; to measure overall discrimination
- Precision, Recall, F1; to evaluate minority class performance
- Confusion matrices; to visualize true vs. predicted classes
- SHAP values (Random Forest); to interpret feature importance

# Insights & Results
In looking at the findings from our experiments, we looked at the stated evaluation metrics:

## Random Forest Outperformed All Other Models
We found, after looking at our results, that Random Forest was the best model by several key metrics:
- Highest ROC-AUC
- Best stroke-case recall
- Most balanced across metrics
- Most stable across splits

## Neural Networks Underperformed
Challenges with FCNN we discovered included:
- Overfitting
- Inconsistent performance
- Lower minority recall

## Logistic Regression Was Too Simple
We expected LR to underperform, as we were simply using it as a baseline. Here were its issues if we were to look at it for direct use:
- Low recall for minority class
- Underfit nonlinear interactions

## Predictive Features (Random Forest)
We identified key predictive features using SHAP values from the Random Forest model(because it was the best performing model). Top features included:
- Age
- Avg glucose level
- Hypertension
- Heart disease
- BMI
- Smoking status

## Data Augmentation Was Essential
A critical insight from our experiments was the impact of data augmentation, particularly SMOTE:
Without augmentation:
- Minority recall was near zero
- Models predicted almost exclusively “no stroke”

With augmentation:
- Metrics became meaningful
- Random Forest clearly best

# Risks and Limitations
This dataset and approach have several limitations:
- Class imbalance persists even after augmentation
- Small dataset limits DL performance
- Dataset may not generalize to wider populations
- Synthetic oversampling can introduce noise

# Reproducibility & Setup Instructions

## Local Setup
### Clone
```
git clone <repo-url>
cd ml9-team-project
```

### Install
```
conda create -n ml9 python=3.11
conda activate ml9
pip install -r requirements.txt
```

### Run
```
jupyter lab
```

# Docker (Reproducible Environment)

Included files:
- Dockerfile
- docker-compose.yml
- .dockerignore

## Quick Start
### Build
```
docker build -t ml9-team-project:latest .
```

### Run
```
docker-compose up --build
```

### Access Jupyter
```
http://localhost:8888
```

# References

[1] Vyas et al., Stroke 2023  
[2] Vu et al., J Cardiovasc Dev Dis 2024  
[3] Moulaei et al., Sci Rep 2024
