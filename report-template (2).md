# Report: Predict Bike Sharing Demand with AutoGluon Solution
#### Yousef Burhan Mohammad Ahmad

## Initial Training
### What did you realize when you tried to submit your predictions? What changes were needed to the output of the predictor to submit your results?
Five experiments were conducted:

Initial submission with raw data 
Submission after adding new features (EDA + Feature Engineering) 
Initial hyperparameter optimization (HPO) submission
HPO with Setting 1 submission
HPO with Setting 2 submission

Observation: Some experiments resulted in negative prediction values, which Kaggle doesn't accept. 
Changes made: Replaced all negative predictions with 0 before submission.
### What was the top ranked model that performed?
Tree-Based Models: (GBM, XT, XGB & RF)|KNN|0.56539 

## Exploratory data analysis and feature creation
### What did the exploratory analysis find and how did you add additional features?
The datetime feature was converted to extract the hour information.
The 'season' and 'weather' features, initially integers, were changed to categorical data.
Year, month, day, and hour were extracted as separate features from datetime and the original datetime feature was removed.
The 'casual' and 'registered' features improved RMSE scores during cross-validation but were dropped because they're not in the test dataset.
A new categorical feature 'day_type' was created based on 'holiday' and 'workingday' to categorize weekdays, weekends, and holidays.
The 'temp' and 'atemp' features had a high correlation, so 'atemp' was removed to reduce multicollinearity.
Data visualization was used to gain insights from the features.

### How much better did your model preform after adding additional features and why do you think that is?
The model's performance increased by about 138% after adding new features compared to the initial model.
Converting certain integer categorical variables to their correct data type improved the model.
Ignoring 'casual' and 'registered' features and dropping 'atemp' reduced multicollinearity.
Splitting the datetime feature into 'year', 'month', 'day', 'hour', and adding 'day_type' enhanced the model's ability to capture seasonality and historical patterns.

## Hyper parameter tuning
### How much better did your model preform after trying different hyper parameters?
Hyperparameter tuning improved model performance compared to the initial submission. Three configurations were tested. Although the tuned models performed well, the model with EDA and added features excelled on the Kaggle test data.

Observations:

Using the autogluon package for training, hyperparameter-tuned models didn't always perform optimally due to limited user-defined hyperparameter values.
The 'time_limit' and 'presets' parameters are crucial in autogluon's hyperparameter optimization.
Setting a low 'time_limit' can prevent autogluon from building models effectively.
Preset options like "high_quality" with auto_stack are resource-intensive; lighter presets like 'optimized_for_deployment' were more efficient.
Choosing between exploration and exploitation is challenging with limited hyperparameter ranges in AutoGluon.

### If you were given more time with this dataset, where do you think you would spend more time?
With more time, I'd explore running AutoGluon for longer periods using a high-quality preset and deeper hyperparameter tuning to potentially unlock better model performance and uncover more optimal configurations.

### Create a table with the models you ran, the hyperparameters modified, and the kaggle score.
|model|hpo1|hpo2|hpo3|score|
|--|--|--|--|--|
|initial|prescribed_values|prescribed_values|Presets specified:[ 'best_quality']|2.18248|
|add_features|prescribed_values|prescribed_values|Presets specified: ['best_quality']|1.93719|
|hpo|Tree-Based Models: (GBM, XT, XGB & RF)|KNN|Presets specified: ['optimize_for_deployment']|0.56539|

### Create a line plot showing the top model score for the three (or more) training runs during the project.

TODO: Replace the image below with your own.

![model_test_score.png]('model_test_score.png')

### Create a line plot showing the top kaggle score for the three (or more) prediction submissions during the project.

TODO: Replace the image below with your own.

![model_test_kagglescorepublic]('model_test_kagglescorepublic.png')

## Summary
The bike sharing demand prediction project incorporated the comprehensive AutoGluon AutoML framework for tabular data. This framework was harnessed to create both stack ensembles and individual regression models tailored for the data. It facilitated the rapid development of a baseline model.

The leading model, powered by AutoGluon, significantly enhanced results by leveraging data from thorough exploratory data analysis (EDA) and feature engineering, even without hyperparameter optimization. 

By employing AutoGluon's automatic hyperparameter tuning, model selection, and architecture search, we were able to explore and exploit the most promising configurations effectively. 

While hyperparameter tuning with AutoGluon did yield better results than our initial submission, it fell short of the model enhanced by EDA and feature engineering but without hyperparameter optimization.

We observed that using AutoGluon for hyperparameter tuning, especially without default parameters or random configurations, can be challenging. The effectiveness of this process is closely tied to factors like the time limit, chosen presets, the variety of models considered, and the hyperparameter ranges for tuning.
