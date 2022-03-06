# Starbucks_offers

## Description:
This is the capstone project for the Udacity DS Nanodegree. The data set used in this project was provided by Udacity and it contains simulated data that mimics customer behavior on the Starbucks rewards mobile app. Once every few days, Starbucks sends out an offer to users of the mobile app. An offer can be merely an advertisement for a drink or an actual offer such as a discount or BOGO (buy one get one free). This project aims to determine which demographic groups respond best to which offer type. 

### Question 1:
Which group is more likely to view a BOGO offer after receiving it ?

#### Input features
- 3 binary features:
    - Old vs young: 35 years
    - Male vs Female
    - Rich vs poor: $60k

#### Output
- People who viewed offer that received BOGO offer

#### Approach
1. Data processing:
    - Add offer_ids, column to transcript data
    - Rename 'id' column in portfolio to 'offer_ids'
    - Remove outliers (age > 99 years, income > $1M) 
    - Drop people with missing age, gender, income data
    
2. Feature engineering:
    - One hot encode categorical variables
    - Gender category (male, female, other)
    - Income category (high income, low income)
    - Age category (young, old)
    
    
3. Train/test split:
    - 80/20 train/test
    - Random oversample train dataset to deal with class imbalance
    
4. Fit train data:
    - RandomForestClassifier
    
5. Evaluate on test data:
    - Confusion matrix
    - Understand feature importance

## Files: 
1. 1_prep: takes 3 input dataframes (portfolio, profile, transcript), cleans data, outputs prepared data as bogo_data.pkl
2. 2_train: imports prepared date (bogo_data.pkl), splits data and fits classifier, outputs test data (X_test.pkl, y_test.pkl) and model (classifier.pkl)
3. 3_evaluate: imports model (classifier.pkl) and test data (X_test.pkl, y_test.pkl), evaluates model, determines feature importance 
