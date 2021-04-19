# Project 3
### Victoria Yuanyuan Chang

Using two machine learning methods predict population values at 100 x 100 meter resolution throughout your selected country.
Validate the two models using different methods presented in this class, write a report assessing the two approaches and which of the two models was more accurate. Be sure to account for spatial variation throughout your selected location and provide substantive explanations for why those variations occurred.

The country I chose for this project is Liberia. Below is a map of the country. As shown in the map, Monrovia is the capital of Liberia. The capital area is the most densely populated region of the country.
![](map.png)

### 1. Linear Regression Model:
13 variables were used to predict the population of each region. The actual population data comes from the Worldpop data of Liberia's population distribution in 2019. Data were splitted into training and testing sets and a linear regression model is trained and used to predict the population distribution.

Linear regression results are shown below:

![](lr_results.png)

The relatve importance of each factor in predicting the population:

![](lr_importance.png)

The plotted predicted population (left) as compared to the actual distribution of population (right):
![](lr_popsum.png) ![](actual_pop.png)

#### Model Validation
Comparing the image of the predicted population and the actual population, the model seems to 
Diff Sums:
![](lr_diffsum.png)
3D plot of diff sums:
![](lr_3d.png)

As shown in the plot, the model tends to underpredict the population, except for the capital area. This is likely due to the relatively larger number of populations in the capital area.
MSE vs. MAE

MSE:
![](lr_mse.png)

MAE:
![](lr_mae.png)

Calculated using CellStats, MAE = 1852354 and MSE = 15902959.

### 2. Random Forest

The relatve importance of each factor:

![](rf_importance.png)

Population sums: 

![](rf_popsum.png)

Diff Sums:

![](rf_diffsum.png)

3D plot of diff sums:

![](rf_3d.png)

As shown in the plot, the model tends to underpredict the population, except for the capital area. This result is similar to that of the linear regression.

Model validation: MSE vs. MAE

MSE:

![](rf_mse.png)

MAE:

![](rf_mae.png)

Calculated using CellStats, MAE = 1906480 and MSE = 15953265.

## 3. Comparison of the two models:
Judging from the resulting plots, the two models do not differ much in terms of predictive power and accuracy. Comparing the MSE and MAE of the two models, on the other hand, the linear regression model out-perform the random forest model.
