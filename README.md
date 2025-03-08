# Hospital Length of Stay Classification Repository

## Overview

This repository documents our research on classifying hospital length of stay (LOS) for diabetic patients at Hartzfeld Hospital. Our primary objective was to evaluate whether temporal patterns extracted through Knowledge-Based Temporal Abstraction (KBTA) and pattern mining techniques improve LOS classification compared to standard baseline features. Additionally, we assessed the impact of different observation windows (7 days vs. 14 days) on classification performance.

The research followed a sequential approach, beginning with preliminary regression models to predict exact LOS values, before transitioning to our main focus: binary classification of whether a patient's stay would be above or below the median LOS.

## Repository Structure

The repository contains four primary notebooks:

### Initial LOS Prediction Models

- **14Days_LOS_Prediction_Model_With_Temporal_Features.ipynb**: Using incorporating temporal patterns alongside baseline features, using data from the first 14 days of hospitalization..
- **14Days_LOS_Prediction_Model_Only_BaseLine.ipynb**: Only baseline features for comparison purposes, using data from the first 14 days of hospitalization.

### Primary LOS Classification Models

- **7Days_LOS_Classification.ipynb**: Classification model using data from the first 7 days of hospitalization.
- **14Days_LOS_Classification.ipynb**: Classification model using data from the first 14 days of hospitalization.

## Research Methodology

### Dataset

Our research utilized data from Hartzfeld Hospital in Gedera, Israel, which specializes in geriatric rehabilitation. The dataset comprised records from 4,104 diabetic patients, with an average of 5,000 time-stamped records per patient, including demographics, vital signs, laboratory results, and medication logs.

### Temporal Abstraction Process

We employed Knowledge-Based Temporal Abstraction (KBTA) to transform raw clinical data into meaningful interval-based abstractions. This process utilized:

1. The Temporal Abstraction Knowledge (TAK) language for defining clinical temporal concepts.
2. The Mediator Framework for applying KBTA to clinical data.
3. Transformation of continuous parameters into symbolic intervals representing states and trends.

### Temporal Pattern Mining

We utilized the KarmaLego framework to identify Temporal Interval Relation Patterns (TIRPs) by analyzing relationships between time intervals. We focused on three fundamental Allen's interval relations:

- Before: Event A occurs strictly before event B.
- Overlaps: Event A and event B share a partial time overlap.
- Meets: Event A ends exactly when event B begins.

This approach reduced computational complexity while maintaining clinical relevance of the extracted patterns.

### Feature Extraction

We created three distinct feature sets for model evaluation:

1. **Baseline Features**:

   - Demographic data (age, gender, comorbidities)
   - Statistical summaries of vital signs and lab values (min, max, mean, standard deviation)
   - Frequency counts of measurements in clinically significant ranges

2. **Pattern-Based Features**:

   - Temporal Interval Relation Patterns (TIRPs) extracted through KarmaLego
   - Encoded as numerical features representing pattern presence and frequency

3. **Combined Features**:
   - Integration of both baseline and pattern-based features

### Machine Learning Implementation

We implemented and evaluated three classification algorithms:

- Random Forest
- Support Vector Machine (SVM)
- XGBoost

Hyperparameter optimization was performed using Optuna to ensure optimal model configuration. Additional techniques included:

- Feature scaling (particularly for SVM)
- SMOTE for handling class imbalance (in XGBoost)
- Comprehensive evaluation using Accuracy, Precision, Recall, F1 Score, and AUC-ROC

## Research Process

Our research followed a systematic approach:

1. **Initial Exploration**: We started with regression models to predict exact LOS values, utilizing both temporal features and baseline features.

2. **Primary Classification Focus**: Based on initial findings, we transitioned to a classification approach, categorizing patients according to whether their stay would be above or below the median LOS.

3. **Observation Window Comparison**: We implemented classification models using both 7-day and 14-day observation windows to assess the impact of extended monitoring periods.

4. **Feature Set Evaluation**: For each observation window, we compared the performance of models trained on pattern-based features, baseline features, and combined features.

5. **Model Optimization**: We tuned hyperparameters using Optuna and applied appropriate preprocessing techniques for each algorithm.

## Key Findings

Our research demonstrated several important insights:

1. Pattern-based features exhibited high precision but lower recall, while baseline features provided more balanced performance metrics.

2. The combined feature set typically offered the best overall performance, maintaining high precision while improving recall.

3. Temporal patterns provided valuable additional signal beyond what could be captured by statistical summaries alone, highlighting the importance of capturing the temporal dynamics of patient care.

4. Classification performance generally improved when extending the observation window from 7 days to 14 days, particularly when using combined feature sets.
