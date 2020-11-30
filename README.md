# Predicting-Employee-Attrition

# Table of Contents

### Reports
- [Presentation Notebook](https://github.com/Jaccomando/Predicting-Employee-Attrition/blob/main/notebooks/Final_Notebook.ipynb)
- [Presentation Slides](https://github.com/Jaccomando/Predicting-Employee-Attrition/blob/main/reports/Capstone_Presentation.pdf)

### Exploratory Notebook
- [EDA](https://github.com/Jaccomando/Predicting-Employee-Attrition/blob/main/notebooks/EDA.ipynb)

# Business Understanding 
Employee churn is a significant expense for companies. The Society for Human Resource Management estimates the average replacement cost of a salaried employee is the equivalent of six to nine months’ salary. Creating a classification model to help better predict when an employee is a flight risk will help management identify flight risk employees before they leave the company allowing for an opportunity to intervene early. This can help reduce employee churn and the the cost of replacing and training new employees.

# The Data
The data set used for this project is the <a href="https://www.kaggle.com/pavansubhasht/ibm-hr-analytics-attrition-dataset">IBM HR Analytics Employee Attrition & Performance dataset</a> from Kaggle and created by IBM. It contains 23,436 rows representing individual employees. There are 32 different features including age, education, gender, marital status, overtime worked, etc. Attrition is the target.

## Reproduction Instructions
The dataset may be downloaded from Kaggle <a href="https://www.kaggle.com/pavansubhasht/ibm-hr-analytics-attrition-dataset">here.</a>

## Preparing the Data
The dataset is a clean dataset with one CSV file. The CSV file is imported and converted to a Pandas data frames.

## Exploratory Data Analysis (EDA)
CRISP - DM techniques are used to understand and prepare the data for modeling. Initial EDA reveals a relatively clean dataset with easy to understand rows and columns with few missing values.

## Visualizing the Data
I am interested in identifying the top correlations to the target "Attrition" as I will want to compare them to the models' top features. 
We see that 'Age', 'Stockoptionlevel', 'Yearsincurrentrole', 'Totalworkingyears', and 'Joblevel' are the highest correlated features. 

### <center>Feature Correlations to Attrition</center>

![Feature Correlations to Attrition](/reports/figures/corrs.png)

### <center>Attrition by Age</center>

![Attrition by Age](/reports/figures/age_dist.png)

### <center>Attrition by Stock Options</center>

![Attrition by Stock Options](/reports/figures/stock_dist.png)

### <center>Attrition by Years in Role</center>

![Attrition by Years in Role](/reports/figures/years_role_dist.png)

## Pre-processing
I drop NAs, remove six columns that either contain no unique values, or are not useful for modeling, and convert the target "Attrition" to "Current employee" = 0, and "Voluntary Resignation" = 1. Next the target is split from the data and I create a train test split and validation set for training, validating, and eventually testing the model. Numeric columns are isolated, scaled, and one hot encoded before being rejoined with categorical columns. The training data is then smoted in advance of the first simple model.  

# Models

## First Simple Model
Logistic Regression is used for a first simple model. After several attempts at tuning parameters, the model does not perform well on training or validation data. The accuracy score is .69 and an F1 score of .70. I decide to move onto other models which may be better suited to binary classification. 

## Additional Models
I try Support Vector Machine, Random Forest Classifier, K Nearest Neighbor, and stacking Random Forest Classifer and K Nearest Neighbor as base learners with Logistic Regression as the meta learner. While the stacked model performs best on the validation data with 7 false negatives and 1 false positive as well as the complete training data with 0 false negatives and 2 false positives, it would not prove to do so on test data. 

## Best Model Evaluation
K - Nearest Neighbor proves to perform best on test data with accuracy of .97 and F1 score of .98. It accurately predicts 3837 employees will not churn and that 674 will churn. It incorrectly predicts that 40 employees will churn when they actually stay, and that 90 employees will stay when they actually churn. 

### <center>"K - Nearest Neighbor Confusion Matrix</center>

![K - Nearest Neighbor Confusion Matrix](/reports/figures/knn_cm.png)

## Model Feature Importances
Of my top three performing models, only Random Forest has a feature importances function from Scikit-learn. It identifies 'Age', 'DailyRate', 'MonthlyIncome', 'DistanceFromHome' and 'JobSatisfaction' as the top 5 feature importances. Assuming that 'DailyRate' and 'MonthlyIncome' are the same, we could find the next highly rated feature importance not related to salary which would be 'TotalWorkingYears'.

### <center>Feature Importances Model</center>

![Feature Importances Model](/reports/figures/model_feat.png)

## Future Development Ideas
1. Build more models, including a Neural Network Model.
2. Explore the role gender plays in attrition. 
3. Explore the role Covid 19 plays in attrition.

# Summary
By using CRISP - DM tecniques and machine learning algorithms I create a binary classification model with .97 accuracy. This model, used alongside an understanding of the business and employee base is helpful in accurately predicting when an employee will voluntarily leave the company. 

My initial data exploration finds a close correlation between age and attrition. Additionally, it identifies stock option level, years in current role, total working years, and job level as in the top five highest correlated features to attrition. 

My model feature importances also identify age as a top five feature importance. And if we assume daily rate, monthly income, hourly rate and monthly rate to be highly correlated with each other, then the next highest feature importance becomes total working years. Note this is also the fourth highest correlated feature identified in initial data exploration.

# Recommendations
1. Carefully evaluate employee age. More employee churn occurs between the ages of 25 and 35 years old so a company should focus on employees within that age group to monitor overall satisfaction. 
2. Look at employee total working years. Employees with more total working years chrun more but also have more experience which could be used to mentor younger employees. This could even potentially reduce churn in the 25 to 35 year old age group. 
3. Employees with no stock option plans churn more than employees with stock option plans. This provides an opportunity. Owning company stock is a siginificant motivator which could improve performance and employee attrition.  
4. Other features such as job satisfaction, income, distance from home also play a role in employee attrition and should be addressed. 









