# Report: Predict Bike Sharing Demand with AutoGluon Solution
#### 

## Initial Training
### What did you realize when you tried to submit your predictions? What changes were needed to the output of the predictor to submit your results?
Kaggle requires all negative values to be replaced with zeros. Hnece for initial model,the changes to be made was to modify negative values. However, all the values were positive. Therefore there was no need for modification. 

### What was the top ranked model that performed?
The Weighted_Ensemble_L3 model, which stacks three layers of previously trained models, had the lowest root mean square error (rmse) and was ranked the highest. It achieved the highest accuracy.

## Exploratory data analysis and feature creation
### What did the exploratory analysis find and how did you add additional features?
I noted that `count` was the dependent variable and there were no missing values in the data. `atemp` and `temp` are highly correlated.
Other observations include: 
- The count of total rental bikes is high in non holidays vs in holidays; high in workingdays than in non working days.
- The count of rented bikes at 8 am as well as between 5am to 6 am is high. In contrast, the count of bikes rented between 12am and 5am is very low.
- Bike rentals is affected by weather since people rent many bikes when the weather is clear vs when there is heavy rain.
- Spring has the lowest count of bike rentals while fall has the highest count of bike rentals.
- The bike rentals are also affected by temperature, humidity and wind changes. High bike rentals occur when there is low wind, mid(neither too high , nor too low) temperatures and humidity.

I added features using the datetime column. I extracted hour from the datetime column.

### How much better did your model preform after adding additional features and why do you think that is?
There was an improvement in performance the root mean square error decreased. The initial training had a score of 52.813217 which dropped to 30.132846 
## Hyper parameter tuning
### How much better did your model preform after trying different hyper parameters?
There was a decrease in performance of both the root mean logarithmic score from 0.69094 dropping to 0.46771. I noted an increase in the root mean square score from 30.132846 to 36.101380 

### If you were given more time with this dataset, where do you think you would spend more time?
I would spend more time in feature elimination or creating new features. Finding out for example how the hour data of bike rentals varies in different months.

### Create a table with the models you ran, the hyperparameters modified, and the kaggle score.
|    | model        | hpo1                                                                                                                                                                                            | hpo2                                                                                                                                                                                 | hpo3                                                                                                                                                     |   score |
|---:|:-------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------|--------:|
|  0 | initial      | default_vals                                                                                                                                                                                    | default_vals                                                                                                                                                                         | default_vals                                                                                                                                             | 1.80731|
|  1 | add_features | default_vals                                                                                                                                                                                    | default_vals                                                                                                                                                                         | default_vals                                                                                                                                             | 0.69094 |
|  2 | hpo          | GBM (Light gradient boosting) : num_boost_round: [lower=100, upper=25], learning_rate:[lower=0.01, upper=0.3, log scale],num_leaves:[lower=3, upper=5] applying random search with 5 trials | XGB (XGBoost): n_estimators : [lower=100, upper=500], max_depth : [lower=3, upper=5], eta (learning_rate) : [lower=0.01, upper=0.3, log scale] applying random search with 5 trials | CAT (CATBoost) : iterations : 100, depth : [lower=6, upper=10], learning_rate  : [lower=0.01, upper=0.1, log scale] applying random search with 5 trials|0.46771|

### Create a line plot showing the top model score for the three (or more) training runs during the project.

![model_train_score.png](https://github.com/Jerdah/AutoGluon-Predict_Bike_Sharing_Demand/blob/main/model_train_score%20.png)

### Create a line plot showing the top kaggle score for the three (or more) prediction submissions during the project.

![model_test_score.png](https://github.com/Jerdah/AutoGluon-Predict_Bike_Sharing_Demand/blob/main/model_test_score.png)

## Summary
In summary , this project highlighted the importance of EDA , feature engineering and hyperparameter tuning to achieve optimal results. 

