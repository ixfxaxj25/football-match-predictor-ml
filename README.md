# Football Match Predictor AI

A machine learning system developed to predict whether the **home team will win or not** in English Premier League (EPL) football matches.

The project combines football data scraping, data preprocessing, feature engineering and machine learning to generate predictions for upcoming fixtures. Three machine learning models were developed and compared: **XGBoost, Random Forest and Multi-Layer Perceptron (MLP)**. XGBoost achieved the strongest overall performance and was selected as the final prediction model.

---

## Project Overview

The aim of this project was to develop a data-driven system capable of predicting Premier League match outcomes using historical football statistics.

The prediction target is binary:

* `1` = Home team win
* `0` = Home team does not win (draw or loss)

The system was designed to:

* Collect historical Premier League football data
* Scrape updated match information from FBref
* Clean and preprocess the dataset
* Engineer additional performance-based features
* Train and compare multiple machine learning models
* Optimise model hyperparameters
* Generate predictions for upcoming fixtures
* Provide predictions to a separate web application

The complete project consists of a **machine learning pipeline** and a **web application** for displaying the generated predictions.

---

## Machine Learning Pipeline

```text
Football Match Data
        ↓
Data Collection / Web Scraping
        ↓
Data Cleaning & Preprocessing
        ↓
Feature Engineering
        ↓
Chronological Data Split
        ↓
Model Training
        ↓
Bayesian Hyperparameter Optimisation
        ↓
Prediction
        ↓
Model Evaluation
        ↓
Predictions for Web Application
```

The dataset is processed chronologically to reduce the risk of future information influencing predictions. Rolling averages are also calculated using previous matches only, helping to avoid lookahead bias.

---

## Data Collection

The project initially explored the use of football APIs, including SportMonks. Due to restrictions such as API call limits and limitations on historical data, the project moved to **web scraping** instead.

**FBref** was selected as the main football data source because it provides detailed match statistics and regularly updated Premier League data. The project uses scraping to collect information such as:

* Match dates
* Teams
* Goals
* Expected goals (xG)
* Possession
* Shots
* Shots on target
* Home/away information

## The data collection process was implemented using Python web-scraping tools including Selenium and BeautifulSoup.

## Data Preprocessing

The raw data required several preprocessing steps before it could be used for machine learning.

These included:

* Filtering the dataset to Premier League fixtures
* Cleaning unnecessary columns
* Standardising team names
* Standardising match dates
* Creating home and away representations of matches
* Encoding venue information
* Creating the binary prediction target
* Combining historical and scraped datasets
* Adding future fixtures for prediction

## The initial Kaggle dataset was subsequently supplemented with FBref data to provide additional and more up-to-date match information.

## Feature Engineering

Additional features were created to capture team performance and recent form.

Examples include:

* Goal difference
* Possession difference
* Expected goals difference
* Clean-sheet ratio
* Head-to-head statistics
* Recent team performance
* Home/away performance indicators
* Rolling performance averages

Three-match rolling averages were calculated for relevant statistics. The current match was excluded from the rolling calculation so that only information available before the match was used. This was done to reduce lookahead bias.
Feature importance analysis showed that head-to-head features and recent performance-related features were among the more influential predictors in the XGBoost model.

---

## Machine Learning Models

Three classification models were developed and compared using the same dataset and feature engineering approach:

### XGBoost

XGBoost was used as the main gradient-boosting model. It was selected because of its ability to model nonlinear relationships between football performance features.

### Random Forest

Random Forest was used as an ensemble-based comparison model consisting of multiple decision trees.

### Multi-Layer Perceptron

A Multi-Layer Perceptron (MLP) neural network was also implemented to investigate whether a neural-network approach could identify more complex relationships within the data.

---

## Training & Hyperparameter Optimisation

The project used a chronological approach to model evaluation.

For XGBoost and Random Forest, **TimeSeriesSplit** was used to preserve the chronological order of football matches. The MLP used a standard train/test split.

**Bayesian Optimisation** was used to tune model hyperparameters and improve model performance.

The optimisation process found that increasing the number of iterations beyond 20 provided limited benefits and could increase the risk of overfitting. Twenty iterations provided a better balance between model complexity and generalisation.

---

## Model Evaluation

The models were evaluated using:

* Accuracy
* Precision
* Recall
* F1-score
* Confusion matrices

The final evaluation compared the models on their ability to predict both:

* Home team wins
* Home team non-wins

This was particularly important because the two classes were not perfectly balanced.

### Final Model

**XGBoost was selected as the final model.**

It achieved:

| Metric            |  XGBoost |
| ----------------- | -------: |
| Accuracy          |  **67%** |
| Weighted F1-score | **0.68** |

For predicting home wins, XGBoost achieved a recall of **0.68** and precision of **0.55**. It also provided a stronger overall balance between the two classes than Random Forest and MLP.

The confusion-matrix analysis also showed that XGBoost provided a balanced trade-off between false positives and false negatives compared with the other models.

---

## Technologies Used

### Machine Learning

* Python
* Pandas
* NumPy
* Scikit-learn
* XGBoost
* TensorFlow / Keras

### Data Collection

* Selenium
* BeautifulSoup

### Optimisation & Analysis

* Scikit-optimize
* Matplotlib
* Seaborn

### Database & Web Platform

* MySQL
* Spring Boot
* Java
* React

The machine learning pipeline was developed in Python, while the prediction platform used React, Spring Boot and MySQL.

---

## Repository Structure

```text
football-match-predictor-ml/
│
├── DatabaseUpdate.py
├── KaggleDatabasePreprocess.py
├── MatchUpdateScraping.py
├── NN.py
├── RandomForest.py
├── Scraping.py
├── XGBV2.py
│
├── data/
│
├── README.md
├── requirements.txt
└── .gitignore
```

The repository contains the Python components used for data collection, preprocessing, database updates, model development and prediction generation.

---

## Prediction System

The machine learning pipeline generates predictions for future Premier League fixtures.

Future matches are added to the dataset without completed-match statistics. Once those matches have been played, the scraping process can collect the updated results and statistics and update the dataset. This allows the prediction pipeline to continue using more recent information.

---

## Web Application

The predictions generated by this repository are used by a separate web application.

The web platform was developed using:

* **React** for the frontend
* **Spring Boot / Java** for the backend
* **MySQL** for the database

The frontend communicates with the backend, which retrieves prediction data from the database and presents upcoming match predictions to users.

**Related repository:** Football Match Predictor Web Application

---

## Project Report

A full academic report documenting the project's background, methodology, design, implementation, testing, evaluation and conclusions is available separately.

**Project title:**
*Developing an AI-Powered Web Platform for Football Match Outcome Prediction*

---

## Future Improvements

Potential future improvements identified during the project include:

* Automating regular dataset updates
* Adding more player-level performance features
* Incorporating weather information
* Expanding the range of predictive features
* Continuing model retraining as new match data becomes available

The report also notes that model performance can change as additional seasons and match data are added, making continued evaluation important.

---

## Author

**Ifaj Tajwar Khan**

BSc (Hons) Computer Science
Brunel University London
