# Project 1
### Victoria Yuanyuan Chang

Project 2, due Wednesday, March 24th by midnight

## Model 1
Using the R script provided, split and sample your DHS persons data and evaluate the AUC - ROC values you produce.
#### 1. Which "top_model" performed the best (had the largest AUC)?

The top_models are the following:
```
  penalty .metric .estimator  mean     n std_err .config              
      <dbl> <chr>   <chr>      <dbl> <int>   <dbl> <chr>                
 1 0.0001   roc_auc hand_till  0.617     1      NA Preprocessor1_Model01
 2 0.000127 roc_auc hand_till  0.617     1      NA Preprocessor1_Model02
 3 0.000161 roc_auc hand_till  0.617     1      NA Preprocessor1_Model03
 4 0.000204 roc_auc hand_till  0.617     1      NA Preprocessor1_Model04
 5 0.000259 roc_auc hand_till  0.617     1      NA Preprocessor1_Model05
 6 0.000329 roc_auc hand_till  0.617     1      NA Preprocessor1_Model06
 7 0.000418 roc_auc hand_till  0.617     1      NA Preprocessor1_Model07
 8 0.000530 roc_auc hand_till  0.616     1      NA Preprocessor1_Model08
 9 0.000672 roc_auc hand_till  0.616     1      NA Preprocessor1_Model09
10 0.000853 roc_auc hand_till  0.616     1      NA Preprocessor1_Model10
11 0.00108  roc_auc hand_till  0.616     1      NA Preprocessor1_Model11
12 0.00137  roc_auc hand_till  0.615     1      NA Preprocessor1_Model12
13 0.00174  roc_auc hand_till  0.614     1      NA Preprocessor1_Model13
14 0.00221  roc_auc hand_till  0.613     1      NA Preprocessor1_Model14
15 0.00281  roc_auc hand_till  0.612     1      NA Preprocessor1_Model15

```
lr_best returns ```0.00108 roc_auc hand_till  0.616     1      NA Preprocessor1_Model11```, therefore model 11 performed the best.

#### 2. Are you able to use the feature selection penalty to tune your hyperparameter and remove any potentially irrelevant predictors? Provide justification for your selected penalty value? 

I selected a penality value of 0.00108, as it is the penalty value f model11, the best performing model. With this penalty value the model seems to have the largest AUC, so it should be able to remove some irrelevant predictors. 

#### 3. Finally, provide your ROC plots and interpret them. How effective is your penalized logistic regression model at predicting each of the five wealth outcomes.
![](lr_auc.png)

Above is the ROC plot of the best-performing penalized logistic regression model. As shown in the graph, the penalized logistic regression model is best at identifying the 5th wealth outcome from the general population. It has some predictive power for the 4th and the 1st outcome, but it's less distinguishable than the 5th. The AUC for the 2nd and 3rd wealth outcomes are quite small, so its performance on predicting these two stratas are pretty bad.

## Model 2
Using the R script provided, set up your random forest model and produce the AUC - ROC values for the randomly selected predictors, and the minimal node size, again with wealth as the target.
#### 1. How did your random forest model fare when compared to the penalized logistic regression?
The best-performing random forest models are the following:
```  mtry min_n .metric .estimator  mean     n std_err .config              
  <int> <int> <chr>   <chr>      <dbl> <int>   <dbl> <chr>                
1     2    34 roc_auc hand_till  0.624     1      NA Preprocessor1_Model21
2     2    36 roc_auc hand_till  0.624     1      NA Preprocessor1_Model18
3     2    31 roc_auc hand_till  0.623     1      NA Preprocessor1_Model07
4     2    24 roc_auc hand_till  0.623     1      NA Preprocessor1_Model12
5     2    20 roc_auc hand_till  0.623     1      NA Preprocessor1_Model14
```
Comparing the AUC-ROC values of the random forest models to that of the logistic regression, the performance of the random forest is better han the penalized logistic regression. Comparing the AUC plots, on the other hands, shows than the random forest model and the logitsic regression model have very similar performance.

#### 2. Provide your ROC plots and interpret them.
![](rf_auc.png)

As shown in the graph, the performance of the random forest model is quite similar to that of the logistic regression. It is best at predicting the 5th wealth strata; it has some validity in predicting the 1st and the 4th strata, while it has limited capacity in identifying the 2nd and the 3rd stratas.

#### 3. Are you able to provide a plot that supports the relative importance of each feature's contribution towards the predictive power of your random forest ensemble model?

![](last_rf_fit.png)

## Model 3
Using the python script provided, train a logistic regression model using the tensorflow estimator API and your DHS data, again with wealth as the target. Apply the linear classifier to the feature columns and determine the accuracy, AUC and other evaluative metrics towards each of the different wealth outcomes. Then continue with your linear classifier adding the derived feature columns you have selected in order to extend capturing combinations of correlations (instead of learning on single model weights for each outcome). 

logistic regression result = {'accuracy': 0.6977188, 'average_loss': 0.5830904, 'loss': 0.5830221, 'global_step': 11310}

#### 1. produce your ROC curves and interpret the results.
The ROC curve plot: ![](linear_roc.png)

As shown in the ROC curve plot, the model has a performance slightly better than random prediction as the curve is slightly higher than a straight diagnal line. 

## Model 4
Using the python script provided, train a gradient boosting model using decision trees with the tensorflow estimator. Provide evaluative metrics including a measure of accuracy and AUC. Produce the predicted probabilities plot as well as the ROC curve for each wealth outcome and interpret these results.

### Analyze all four models. According to the evaluation metrics, which model produced the best results? Were there any discrepancies among the five wealth outcomes from your DHS survey dataset?
