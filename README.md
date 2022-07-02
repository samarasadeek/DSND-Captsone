# Starbucks offers: Udacity DS Nanodegree Capstone project

### Description:

### Motivation
This is the capstone project for the Udacity DS Nanodegree. Starbucks rewards program provides users with informational, BOGO (buy one get one) and discount offers to encourage purchasing of products. For the capstone project, we were given a 30 day buying data to mimic Starbucks rewards program user’s purchasing behaviour along with corresponding demographic data. The task was to use the combined demographic, transaction and offer data to determine which individuals are most response to which offers to drive customer purchasing. Here, machine learning was used to inform the Marketing strategy for the Starbucks rewards program. 

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
  - age: < 25, 25 – 34, 36 – 45, 46 – 66 and 67+
  - income: low (<= 50k), med-low (50k < income <= 70k), med-high (70k < income <= 90k), high (>90k) 
  

#### Output:
Each user was given a binary responsiveness variable for BOGO and discount variables.
The response variable was defined as a the responsiveness of the user i.e. how likely someone is to complete an offer if they received and viewed an offer. The proportion of offers completed per offers viewed was computed and if this ratio was greater than 0.5, the user was labelled as a responsive (or 1), if not, the user was labelled as unresponsive (or 0). This was determined for BOGO offers and discount offers. 

### Results:
A multioutput classifier was built to predict the responsiveness of a Starbucks rewards programmer user to BOGO and discount offers based on user age, income and gender. All numerical data (income and age) were converted to caterogical data. All features were onehotencoded, which means that they were all treated as nominal, so the categories were not rankes. This approach was chosen because the inherent order of the data may not have affected user responsiveness. 
\n Classifiers were evaluated based on the expected profit per user. This metric was chosen since correctly identifying a user to be responsive was assumed to be more valuable than correctly identifying a user to not be responsivess. The costs of false predictions were also assumed to be unequal. The expected profit per user incorporated both unequal costs and benefits. 
\n RandomForest and Bernoulli Naive Bayes classifiers were tuned and evalutated. The Bernoulli NB classifier gave a higher performance and so was chosen as the final classifier. NB classifiers assume a equal feature importance and assume features are independent. These naive assumptions means that they are computationally fast and that they are less prone to overfitting, and hence generalise well. 
\n The Bernoulli NB classifier performs with an expected profit per user per month of USD 6.75, which was estimated to equate to $372 million per year in the US assuming 5 % of Starbucks customers in the US are rewards program users.   


## Files in repo:
1. EDA/EDA: Jupyter notebook with exploratory data analysis of all three datasets. 
2. pipeline/1_prep: Jupyter notebook with pre-processing steps to prepare data for classifier training. The input data were the unprocessed profile, portfolio and transcript data. Data was first cleaned to remove missing or erroneous data. Then categorical age and income data were feature engineered from numerical age and income data. The target variable (responsiveness) was computed and the input features and target variable was combined to produce on dataset. This combined, prepared dataset was pickled to be read into the pipeline/2_train_eval file. 
3. pipeline/2_train_eval: Jupyter notebook which contains classifier training, hypertuning documented using an experimental log and cross-validation steps.

## Libraries used:
1. Pandas 
2. Matplotlib 
3. Seaborn 
4. Pickle
5. Datetime
6. Scikit-learn


