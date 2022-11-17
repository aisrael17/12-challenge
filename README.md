# 12-challenge
Challenge 12 for Columbia FinTech Bootcamp

## Technologies
For this challenge, I used Python 3 with the following external libraries:
* numpy
* pandas
* pathlib (Path)
* sklearn (balanced_accuracy_score, train_test_split, LogisticRegression, and confusion_matrix)
* imblearn (classification_report_imbalances and RandomOverSampler)
* warnings

## Data
The data for this challenge came from a database of peer-to-peer loans from a lending services company. Each row contained information about a specific loan, including:
* The loan size
* The interest rate
* The borrower's income
* The debt-to-income ratio
* The number of accounts
* The number of derogatory marks against the borrower
* The total debt of the borrower
* Whether the loan is healthy or high-risk

## Solution
First, I split the original data into training and test data. Then, I ran a logistic regression on the original data, noting that there were a lot more healthy loans than high-risk loans (75,036 vs. 2,500), which represented ~3% of the total. The logistic regression gave 59 false negatives and 88 false positives for a precision/recall of 87%/91% for high-risk loans. 

Then, we repeated the exercise, but first oversampled the high-risk loans to improve our recall. Given the importance of flagging high risk loans when the overwhelming majority of loans are healthy, this method is preferable if it increases our ability to detect high-risk loans, which may come at the cost of mislabeling some healthy loans as high-risk. Better to be safe than sorry.

As expected, resampling accomplished this goal, increasing our false negative count to 95 but reducing our false positive count to 3 (where a positive represents a healthy loan). As a result, we were able to catch 56 more high-risk loans that the original model failed to identify, albeit at the cost of mislabeling an additional 7 healthy loans as high-risk. 