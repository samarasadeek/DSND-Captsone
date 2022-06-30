# Starbucks_offers

## Description:

### Overview
This is the capstone project for the Udacity DS Nanodegree and is incomplete.

Starbucks rewards program provides users with informational, BOGO (buy one get one) and discount offers to encourage purchasing of products. For the capstone project, we were given a 30 day buying data to mimic Starbucks rewards program user’s purchasing behaviour along with corresponding demographic data. The task was to use the combined demographic, transaction and offer data to determine which individuals are most response to which offers to drive customer purchasing. Here, machine learning was used to inform the Marketing strategy for the Starbucks rewards program. 

Three datasets were given: 
1.	Profile: Demographic data on reward program users including gender, age, income as well as the joining date of each program user and a user id.
2.	Portfolio: Offer data including the offer type and id, the offer duration in days, the channel which the offer was sent on (e.g. web, email, mobile), the spend required to use the offer, the money awarded for the amount spent. 
3.	Transcript: Event log including the person, the event type (e.g. offer received, offer viewed, transaction), the value of the event (either an offer id or a numerical amount of money spent for a transaction) and the time since the start of test was given. 
 

### Problem statement:
To determine which demographic groups respond best to which offer type. 

#### Metric:

For this study it was assumed that correctly predicting that a user would respond to an offer was more valuable to than correctly predicting that a user would not respond to an offer since more revenue would be generated from the user who responds to the offer. The implicit assumption here is that the costs and benefits are unequal. 
The costs of incorrectly predicting that a user would not respond to a BOGO or discount offer (i.e. false negative) was not the equal to incorrectly predicting a user would respond to an offer (i.e. false positive). Further it was assumed that benefits of correctly predicting whether or not a user would respond to an offer (true positive) or not (true negative) were not the same. 
A metric that takes this unequal costs and benefits was therefore needed to evaluate the classifier and was chosen to be the expected profit given by the equation below, a description is given in DS for Business. The final model was the one that gave the highest expected profit.


#### Input features:
The predictor variables are:
  - gender: M, F, O
  - age: 5 age groups 
  - income: low, med-low, med-high, high 

#### Output:
Each user was given a binary responsiveness variable for BOGO and discount variables.
The response variable was defined as a the responsiveness of the user i.e. how likely someone is to complete an offer if they received and viewed an offer. The proportion of offers completed per offers viewed was computed and if this ratio was greater than 0.5, the user was labelled as a responsive (or 1), if not, the user was labelled as unresponsive (or 0). This was determined for BOGO offers and discount offers. 

#### Approach:
1. Data processing:
    - Add offer_ids, column to transcript data
    - Rename 'id' column in portfolio to 'offer_ids'
    - Remove outliers (age > 100 years). This also drops people with missing gender, income data
    
2. Feature engineering:
    - 	Age The ages were categorised into 5 age buckets that could be used in the classifier. The age groups were < 25, 25 – 34, 36 – 45, 46 – 66 and 67+. It was assumed that individuals within those age categories would behave similarly. This of course could be an incorrect assumption.
    - Income: The income was categorised into 4 buckets of < 50,001 (low income), < 70,001 (med-low income), < 90,0001 (high-med income) and >= 90,0001 (high income). 
    -	All feature variables were onehotencoded  
    
3. Preprocessing: 
    - Onehotencode

4. Pipeline: 
    - Combine classifier and preprocessing in one pipeline 

5. Define metric:
    - Custom metric function made to determine expected profil per user 
    
6. GridSearchCV 
    - Use GridSearchCV to tune classifier to determine optimal parameters 
    - Use crossvalidation to train and test classifier using different parameters 

7. Fit train data:
    - RandomForestClassifier
    - Linear SVC
    - Bernoulli Naive Bayes
    
