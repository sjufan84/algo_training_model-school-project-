# algo_training_model
A machine learning model to optimize investment returns based on various technical indicators

### We are initially going to se the SVC classifier model from SKLearn's support vector machine (SVM) learning method to fit the training data and make predictions based on the testing data. The initial train/test split will be three months training and 4092 days testing.  The following are the results from our classification report related to this model --  

           precision    recall  f1-score   support

        -1.0       0.43      0.04      0.07      1804
         1.0       0.56      0.96      0.71      2288

    accuracy                           0.55      4092
   macro avg       0.49      0.50      0.39      4092
weighted avg       0.50      0.55      0.43      4092  

**We can immediately notice that this model is much more accurate predicting 1.0 signals (or buy signals) vs. -1 or sell signals.  

### Next we will adjust the parameters of our train/test split to 256 days training (double the initial training time) and reducing the testing data by 128 days.  The following is the resulting classification report --  

        precision    recall  f1-score   support

        -1.0       0.43      0.07      0.13      1649
         1.0       0.56      0.92      0.70      2115

    accuracy                           0.55      3764
   macro avg       0.49      0.50      0.41      3764
weighted avg       0.50      0.55      0.45      3764  

**After adjusting the train/test split, we notice that the accuracy for our sell signals is slightly better and the accuracy for the buy signals is about the same.  There is very little difference in the overall accuracy performance of the model.  

*There is however a distinct difference in returns vs. the first model... the 2nd model did not outperform the actual returns and significantly underperformed the 1st model's returns.  For reference the model plots are saved in the 'model_plots' folder of the repository.

### Now we adjust the windows for our moving averages from the first model while keeping the train/test split the same.  We kept the short window the same but reduced the long window to 50 periods.  This is the resulting classification report --  

               precision    recall  f1-score   support

        -1.0       0.42      0.13      0.19      1826
         1.0       0.56      0.86      0.68      2321

    accuracy                           0.54      4147
   macro avg       0.49      0.49      0.43      4147
weighted avg       0.50      0.54      0.46      4147  

**Interestingly this model outperformed our initial model in prediction accuracy with sell signals, but underperformed with buy signals.  The overall accuracy was very similar.  It might be worth investigating further tweaks to the short and long windows since this had a larger impact on accuracy than adjusting the train/test split.  

*The return performance of our 3rd model was slightly worse than our initial model, but much better than our 3rd model.  Refer to plots for detailed evaluation.

### Overall the first svm model performed the best.  Although accuracy scores were relatively similar across the models, returns were clearly best for the first model, especially as compared with the 2nd.

### Lastly we are going to use a Stochastic Gradient Descent (SGD) model which is a simple yet very efficient approach to fitting linear classifiers and regressors under convex loss functions such as (linear) Support Vector Machines and Logistic Regression.  We fit the model to our original training data and predict using original testing data.  The resulting classification report is below -- 

     precision    recall  f1-score   support

        -1.0       0.44      0.37      0.40      1804
         1.0       0.56      0.63      0.59      2288

    accuracy                           0.51      4092
   macro avg       0.50      0.50      0.50      4092
weighted avg       0.51      0.51      0.51      4092  

**For reference, the original report for our svm model was --  

  precision    recall  f1-score   support

        -1.0       0.43      0.18      0.25      1791
         1.0       0.56      0.81      0.66      2278

    accuracy                           0.53      4069
   macro avg       0.49      0.50      0.46      4069
weighted avg       0.50      0.53      0.48      4069  

**We can see that the SGD model performed better with predicting sell signals than the svm model, but worse with buy signals.  The overal accuracy of the model is pretty similar.  

*Looking at the plot of the SGD model's return performance is quite interesting... while at the end of the period the returns are similar to our initial SVM model, there is a period right before the end of the plot where the model significantly outperformed the actual returns.  It would certainly be worth investigating if by adjusting the parameters of the SGD model we could generate much higher returns than our SVM models.

