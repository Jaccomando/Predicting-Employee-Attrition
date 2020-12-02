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
I drop NAs, remove six columns that either contain no unique values, or are not useful for modeling, and convert the target "Attrition" to "Current employee" = 0, and "Voluntary Resignation" = 1. Next the target is split from the data and I create a train test split and validation set for training, validating, and testing the model. Numeric columns are isolated, scaled, and one hot encoded before being rejoined with categorical columns. The training data is then smoted in advance of the first simple model.  

# Models

## Model Metrics
I decide to use Accuracy and F-1 Score (a balance of Precision and Recall) as my primary metrics. In this business case, minimizing the number of False Negatives (the number of employees predicted to stay that actually leave) is important and is generally measured by a Recall Score. But a case can be made that minimizing False Positives (the number of employees predicted to leave that actually stay) is also important and is generally measured by a Precision Score. So an F-1 Score is considered to be a nice balanced metric between Precision and Recall. 

## First Simple Model
Logistic Regression is used for a first simple model. After several attempts at tuning parameters, the model does not perform well on training on training data. The accuracy score is .69 with an F1 score of .79. I decide to move onto other models which may be better suited to binary classification. 

## Additional Models
I try Support Vector Machine, Random Forest Classifier, K Nearest Neighbor, and stacking Random Forest Classifer and K Nearest Neighbor as base learners with Logistic Regression as the meta learner. The stacked model performs best on training and validation data yielding perfect accuracy and F-1 scores with Random Forest also performing well with a 98% accuracy and 99% F-1 score. 

## Best Model Evaluation
I decide to choose the Stacked Model as my best model and check it against test data. As expected it performs very well correctly predicting that 3,873 employees will not leave the company, and that 744 employees will leave the company. It incorrectly predicts that 4 employees will leave, when they actually stay and that 20 will stay when they actually leave.

### <center>Stacked Model Confusion Matrix</center>

![Stacked Model Confusion Matrix](/reports/figures//stacked.png)

## Model Feature Importances
Of my top three performing models, only Random Forest has a feature importances function from Scikit-learn. It identifies 'Age', 'DailyRate', 'MonthlyIncome', 'JobRole_Research Scientist' and 'DistanceFromHome' as the top 5 feature importances. Assuming that 'DailyRate' and 'MonthlyIncome' are the same, we could find the next highly rated feature importance not related to salary which would be 'TotalWorkingYears'.

### <center>Feature Importances Model</center>

![Feature Importances Model](/reports/figures/model_feat.png)

## Future Development Ideas
1. Build more models, including Decision Tree, Naive Bayes, Boosting Classifiers, and a Neural Network model.
2. Explore the role gender plays in attrition. Gender equality is a very important issue and it would be interesting to delve deeper into this dataset to specifically look at gender.
3. Explore the role Covid 19 plays in attrition. Once data from 2020 is available it will be critical to analyze it. The workforce has changed in so many ways since March 2020 including many more people working remotely. How will this impact employee attrition?

# Summary
By using CRISP - DM tecniques and machine learning algorithms I create a binary classification model with .99 accuracy and a perfect F-1 Score. This model, used alongside an understanding of the business and employee base is helpful in accurately predicting when an employee will voluntarily leave the company. 

My initial data exploration finds a close correlation between age and attrition. Additionally, it identifies stock option level, years in current role, total working years, and job level as in the top five highest correlated features to attrition. 

My model feature importances also identify age as a top five feature importance. And if we assume daily rate, monthly income, hourly rate and monthly rate to be highly correlated with each other, then the next highest feature importance becomes total working years. Note this is also the fourth highest correlated feature identified in initial data exploration.

# Recommendations
1. Carefully evaluate employee age. More employee churn occurs between the ages of 25 and 35 years old so a company should focus on employees within that age group to monitor overall satisfaction. 
2. Look at employee total working years. Employees with more total working years churn more but also have more experience which could be used to mentor younger employees. This could even potentially reduce churn in the 25 to 35 year old age group. 
3. Employees with no stock option plans churn more than employees with stock option plans. This provides an opportunity. Owning company stock is a siginificant motivator which could improve performance and employee attrition.  
4. Other features such as job satisfaction, income, distance from home also play a role in employee attrition and should be addressed. 









