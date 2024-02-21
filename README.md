# isFraud_detection

# Objective 
- To develop a model for predicting fraudulent transactions for a 
financial company.

# Data Preprocessing
- **Null Values** - Luckily, we don't have any null values.
- **Outliers** - 
- **Multicollinearity** - New_Balance_Org shows with Old_Balance_Org and New_Balance_Dest with Old_Balance_Dest thus by using the method of **variance_inflation_factor** where we drop the features with vif > 5. This resolves the problem of multicollinearity.
- **Label Encoding** - In the column payment method there a 5 unique transactions ways so we encoded it with Label_Encoder.
- **Normalization** - As the values are so much variable with each other which is difficult for the model to process. Thus, normalization is done.


# EDA
- It is found that out of 5 payment methods CASH_OUT and PAYMENT are highly used for transactions.
- Most of the fraud transactions are found in CASH_OUT and TRANSFER method. Thus, we have to work on these two methods of transactions to avoid future frauds.
- Both these methods holds 50-50 percentage of fraud transactions individually.
- In the fraud column the acutual fraud transactions are found to be less then 1% this seems little imbalanced.


# Feature Selection
- Dropped the name columns like nameOrig, nameDest and isFlaggedFraud as the name of a person doesn't holds that much value sometimes.
- Selected the other columns(step, type, amount, oldbalanceOrg, newbalanceOrig, oldbalanceDest, newbalanceDest, isFraud).
- The isFlaggedFraud column seems like someone added it in dataset which are the predictions made by their model. So, either we can drop it or we can do AND operation on isFraud and isFlaggedFraud which will give a new column with 1(acutual true and predicted true or acutual false and predicted false) or 0(acutual true and predicted false or acutual false and predicted true).


# Model Selection
- **Logistic Regression** - One of the simplest model which works better for binary classification.
- **SVM** - It works well with high dimension data and it can easily classify binary problem with a hyperplane.
- **Random Forest** - It prevents overfitting in the model. Also, it works well in this case where we have imbalanced data for fraud section because everytime row selection and feature selection is performed while training base models.


# Model Evaluation
- **Accuraccy** - Both of the models gives outstanding accraccy but we can't just rely on the accraccy term.
- **Confusion Matrix** - It gives a better way to evaluate our models on the basis of **Precision**, **Recall** and **F-beta Score**.
- In our case, we mainly focus on **Recall** as we can't let go a transactions which is fraud. Thus, our model must be accurate in term of predicting fraud transactions which are acutually true. if, a transactions which is not fraud and predicted to be fraud then we can cross verify it.
- So, we must reduce the recall or select the model which have lowest recall.
- Random Forest suits well for this binary classification because it gives better **Recall** accuracy then LR model.


# Conclusion / Answer to asked Questions
1. Data cleaning including missing values, outliers and multi-collinearity.
- We didn't encounter any missing values.
- We keep the outliers for now cause there is a portion of fraud transactions in the total outliers if we remove them then there is a chance that our model/dataset behaves like biased.
- Multicollinearity is removed via Variance Inflation Factor(VIF).
2. Describe your fraud detection model in elaboration. 
- Logistic Regression as it is easy and simple to implemente and works well with binary classification problems.
- Support Vector Classification as it divides the binary classification situation with a describale hyperplane with high dimension features.
- Random Forest cause it prevents the overfitting and it works well in this case where we have imbalanced data for fraud section because everytime row selection and feature selection is performed while training base models.
3. How did you select variables to be included in the model?
- Mainly numerical value columns are choosed as they are easy to process and evaluate.
- Avoid using string/object features like name of a person cause maybe i didn't align with other numerical features.
- Otherwise, we have to encode them using NLP procedure and it will result in increasing the memory and complexity of the model.
4. Demonstrate the performance of the model by using best set of tools. 
- Generally, accuracy is used to measure the performance of a model but as we have imbalanced dataset thus we can't totally depend on accraccy.
- Recall, Precision and F-beta scores are very handfull in these situations.
- It depends on the domain expert what they want with our model to be accurate on either they want to reduce false positive or false negative.
- In this case, i assumed that reducing recall is often neccessary then precision cause we can't let slip a fraud transaction classified as false but if a non fraud transaction is classified as true then we can cross verify it.
5. What are the key factors that predict fraudulent customer? 
- Amount of money is a major factor, larger the amount of money it is often resulted in a fraud.
- There are two columns CASH_OUT and Transfer, which holds the highest number of frauds.
- Thus, taking actions on these methods of payment will help in reducing the frauds in future.
- Step size is also comes under suspect as the time for transfering amount increases then their is chance of getting under fraud also.
6. Do these factors make sense? If yes, How? If not, How not? 
- Yes, all of the mentioned factors making sense.
- Generally, amount of money is a reason of fraud they do and larger the amount they grab.
- Time of transaction is also a reason as it gives the attackers more time to breach the account and perform  fraudulent.
- Payment methods plays a role in frauds too. Online transactions are easy to be cracked and manupulated by attackers. 
7. What kind of prevention should be adopted while company update its infrastructure?
- Restriction on the amount of money can be tranfered from a accurate and also limit the deposit on receivers side.
- Can do something about payment methods and set up restriction/limit on payment methods.
- Regular updation of database and monitoring is neccessary for valid transactions between accounts.
- Can't rely totally on machine models, manual check is also needed sometimes to get deep insight and track of money.
8. Assuming these actions have been implemented, how would you determine if they work?
- After implementing all of these actions, we can monitor the next few weeks or months data to check wheather these actions are performing well or not.
- It will reduce the case of fraudulent and complains automatically from customers which is a good indicator that we are going in right direction.
- In the evolving technology and advancement, the attackers also skilling up regularly and trying new ways to do fraudulent.
- We have keep updating and evolving our ML model with new dataset time to time to keep up with new features which brings more priority for prediction.
