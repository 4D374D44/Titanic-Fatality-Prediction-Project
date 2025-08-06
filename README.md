### Kaggle Competition - Titanic: Machine Learning from Disaster  
**M. Belal ALKASSAB**

---

## Introduction

Date : November 2023

Link : [Submitted Competition Notebook](https://www.kaggle.com/code/mbelalalkassab/titanic-fatality-prediction-project)

This competition is a great way to challenge students in **data preparation**, **feature engineering**, and **machine learning**. The goal is to build a classification model that predicts whether a passenger aboard the Titanic survived, based on features such as:

- Name  
- Age  
- Gender  
- Socio-economic class  
- Other passenger data  

This task assumes that a passenger’s attributes correlate with their survivability, which is an assumption supported by historical analysis, despite luck playing a role.

Achieving a high score involves:

- Understanding interactions between passengers' features (for example the correlation between gender or socio-economic position and survivability, etc)
- Interpreting the historical context (e.g., the crash reason and position, time of incident, etc)
- Exploring statistical patterns in survivability

Knowledge gained from this project can be applied to **post-disaster analysis** and **risk modeling** in real-world disaster studies.

---

## Methodology and Feature Engineering

### 1. Acquiring and Understanding the Data

The dataset was downloaded from [Kaggle Titanic Competition](https://www.kaggle.com/competitions/titanic). It includes a training and test split.

#### Training Dataset Features:
1. `PassengerId`: Unique identifier  
2. `Survived`: 1 = Survived, 0 = Did not survive  
3. `Pclass`: Ticket class (1 = 1st, 2 = 2nd, 3 = 3rd)  
4. `Name`: Passenger's name  
5. `Sex`: Gender  
6. `Age`: Age  
7. `SibSp`: Number of SIBlings/SPouses aboard  
8. `Parch`: Number of PARents/CHildren aboard  
9. `Ticket`: Ticket number  
10. `Fare`: Passenger fare  
11. `Cabin`: Cabin number  
12. `Embarked`: Port of embarkation (C=Cherbourg, Q=Queenstown, S=Southampton)

### 2. Data Cleaning and Interpretation

- Titles (e.g., Mr., Mrs., Master) were extracted from the `Name` field to better estimate missing ages.
- Missing `Age` values were filled in using median age of passengers of similar gender and title.
- Missing `Embarked` values were filled in using the most common port (`S`), because there's only two entries missing.
- Missing single `Fare` value was filled in using the median fare for 3rd class travelers.
- Missing `Cabin` values were labeled as `U` (Unknown).

### 3. Feature Simplification

- `Cabin` column was simplified to just its initial letter.
- `SibSp` and `Parch` were combined into a `FamilyOnBoard` feature:  
  `FamilyOnBoard = SibSp + Parch + 1`

### 4. Feature Binning

- `Age` was binned into 9 quantiles
- `Fare` into 13 quantiles
- `FamilyOnBoard` was categorized:
  - `1`: Solo  
  - `2–4`: Small  
  - `5–6`: Medium  
  - `7+`: Large

### 5. Ticket Grouping

To identify passengers traveling in groups of friends (not family), a new `TicketCount` feature was added. It reflects how many times a given ticket number appears in the dataset.

### 6. Label Encoding

The following columns were label-encoded to transform categorical data into numerical format:
- `Sex`, `Age`, `Fare`, `Cabin`, `Embarked`, `Title`, `FamilyOnBoard`

---

## Training and Evaluation

### 1. Preparing the Data

The PassengerId, Ticket, Name columns of the datasets are dropped and only the important columns are kept for training.

### 2. Selected Models

The following classifiers were tested:

- **Random Forest Classifier**
- **K-Nearest Neighbor**
- **Support Vector Classifier**
- **Gaussian Naive Bayes**

### 3. Model Evaluation

- Different model parameters were tested.
- Final predictions were validated using the actual labels from the Kaggle dataset.
- Accuracy was calculated using `sklearn.metrics.accuracy_score`.
- The model with the highest score was selected for final submission.
