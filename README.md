# Decision Tree Model and Logistics Regression Model for Study On Credit Default Behaviour 
## To Predict Customer Default Based on Credit Behavour

### Input features of the dataset
The dataset contains information about the credit card payment patterns and profile of Taiwanese customers, and whether they had defaulted on the payments.

**Binary (Categorical):** ID, Sex, Education, Marriage, Pay_X (where X =0, 2 to 6), default payment next month 

**Continuous:** Limit Balance, Age, Bill_AmtX (where X = 1 to 6), Pay_AmtX (where X = 1 to 6)
<br /> Dataset contains binary variables “Education”, “Marriage” and “Pay_X (where X =0, 2 to 6)” which individually represents more than two categories each.  “Education” has 4 categories, “Marriage” has 3 categories while “Pay_X (where X =0, 2 to 6)” has 3 categories.

In particular for Logistic Regression, in order to be able to examine the individual effect of the different categories present in the 3 binary variables, one hot encoding had to be carried out using the one to many node.

In general, the continuous variables “Limit Balance” and “Age” were of different magnitudes and thus were normalized for better comparison. A Z-score normalization was used.

### Class Label Distribution
Pie Chart of Defaulters vs Non-Defaulters
 
The dataset is unbalanced with respect to the number of defaulters versus the number of non-defaulters. The number of non-defaulters is represented by the orange colour in the pie chart and is 78% of the population. This is essentially more than three quarters of the population.
The equal sized sampling node was used in Knime to deal with this large imbalance of class to help make the distribution fairer when it came to running the models.
Stratified sampling was also used for the two models to help to deal with this imbalance.





Pie Chart of Defaulters vs Non-Defaulters (After Balancing)
 

Predictive Models Used
1.	Decision Tree Model
2.	Logistic Regression Model

Decision Tree

Reasons for choice of Decision Tree
1.	Capable of handling both continuous and binary (categorical) variables
2.	Able to provide a clear indication of which fields are most important for prediction 

Parameter Optimization Details and Findings
The decision tree model was ran on both the unbalanced and balanced datasets. For a more accurate and fairer view, we will be looking mainly at the balanced dataset.
Method used: K-Fold Cross-Validation
•	Chosen because this method ensures that every observation from the original dataset has the chance of appearing in both the training and test set.
No. of folds: 10 
•	Too small a number of folds will result in more computation time, whereas the larger the number of folds, the lesser the accuracy. As such, I have chosen 10 because I find it to be a good balance of both efficiency in computation time and accuracy.
Choice of random seed: 1234
Parameter for tuning: Minimum Number of Records
Objective Function to Optimize: Maximization of Accuracy 
Optimized Hyper parameter for Unbalanced Set:  46
Optimized Hyper parameter for Balanced Set:  33

Decision Tree Findings on Risk Factors

Based on the Decision Tree formed (balanced dataset), customers who paid their credit card payments in full or paid the minimum amount generally did not default.

Most defaulters were found to be customers who had delayed their credit card payments by 1 or 2 months. In general, customers who had delayed their credit card payments by 1 or more months were found to have a high likelihood of defaulting.

In terms of absolute figures, the greatest number of defaulters were found to have delayed their credit card payments by 2 months.
Evaluation of Decision Tree Model

Unbalanced Dataset (Original)

Sensitivity	Specificity	Accuracy
0.33	0.958	0.819

Balanced Dataset (Equal Sized Sampling)

Sensitivity	Specificity	Accuracy
0.568	0.809	0.688

Overall, the accuracy of the Decision Tree Model is reduced when the dataset is balanced after undergoing the equal sized sampling treatment via the Knime node. In return, the sensitivity increases as a result and the model is better able to correctly predict the number of defaulters. However, in both cases (unbalanced vs balanced datasets), the Decision Tree Model is still better suited to predicting the total number of non-defaulters.

Logistic Regression

Reasons for choice of Logistic Regression
1.	It can be multinomial in nature. The dependent variable can have three or more possible types.	
2.	The coefficient size can provide a measure of the strength of the predictor as well as the direction of its association (positive or negative)
3.	Less inclined to over-fitting. Can run regularization L1 and L2 techniques to prevent/avoid over-fitting.
4.	It can interpret model coefficients as indicators of feature importance.

Parameter Optimization Details and Findings
The Logistic Regression model was ran on both the unbalanced and balanced datasets. For a more accurate and fairer view, we will be looking mainly at the balanced dataset.
Method used: K-Fold Cross-Validation
•	Chosen because this method ensures that every observation from the original dataset has the chance of appearing in both the training and test set.
No. of folds: 10 
•	Too small a number of folds will result in more computation time, whereas the larger the number of folds, the lesser the accuracy. As such, I have chosen 10 because I find it to be a good balance of both efficiency in computation time and accuracy.
Choice of random seed: 1234
Regularization Method: L2 Ridge
Parameter for tuning: Variance 
•	Variance is inversely proportional to lambda. So essentially the aim is to find the optimal lambda figure.
Objective Function to Optimize: Maximization of Accuracy 
Optimized Hyper parameter for unbalanced dataset:  1.7
Optimized Hyper parameter for balanced dataset: 1  

Logistic Regression Model Findings on Risk Factors
Looking at P Value > 0.05, the significant risk factors were identified to be the limit balance, sex and the different marriage statuses. 
In particular, females who were not married or single were more most prone to defaulting on their credit card payments. This was then followed by females who were married and then females who were single in descending order of likelihood to default.







Evaluation of Logistic Regression Model
Unbalanced Dataset (Original)

Sensitivity	Specificity	Accuracy
0.344	0.955	0.82

Balanced Dataset (Equal Sized Sampling)

Sensitivity	Specificity	Accuracy
0.55	0.833	0.691

Overall, the accuracy of the Logistic Regression Model is reduced when the dataset is balanced after undergoing the equal sized sampling treatment via the Knime node. In return, the sensitivity increases as a result and the model is better able to correctly predict the number of defaulters. However, in both cases (unbalanced vs balanced datasets), the Logistics Regression Model is still better suited to predicting the total number of non-defaulters.

Comparison of Decision Tree and Logistic Regression Models

Both models have similar accuracy figures. The Logistic Regression Model has a higher specificity than that of the Decision Tree Model. However, the Decision Tree Model has a higher sensitivity than the Logistic Regression Model. As we are more interested in detecting and predicting credit card defaulters, where defaulters in both models are defined as being the positive class, the Decision Tree Model would be the preferred model. 

But it is important to note that the Decision Tree Model only edges out very slightly on sensitivity. Both models generally have very similar performance statistics. 

Credit Card Defaulter Profiling
Looking at both predictive models, a credit card defaulter is likely to have the following profile:
•	Has a high limit balance
•	Female who is not married or single
•	Delays credit card payments by 1 or 2 months
