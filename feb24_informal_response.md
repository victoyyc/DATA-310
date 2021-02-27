# Feb.24 Informal Response: Calculate MSE
### Victoria Yuanyuan Chang

From your 400+ observations of homes for sale, calculate the MSE for the following:

The 10 biggest over-predictions

The Mean Squared Error is:  117253042143085.14

The 10 biggest under-predictions

The Mean Squared Error is:  3363182525541.278

The 10 most accurate results (use absolute value)

The Mean Squared Error is:  87637616.5438368

In which percentile do the 10 most accurate predictions reside? Did your model trend towards over or under predicting home values?

The 10 most accurate predctions is ranked by ascend at number 114-123 out of 290 valid data points, so they are at about 41th percentile. Therefore, my model trended toward overstimation.

Which feature appears to be the most significant predictor in the above cases?

It seems like for the most accurate predictions and the biggest underestimations, the number of bedrooms is the most significant predictor. While for the biggest over-estimations number of bathrooms seems to play a larger role. This may also be due to the fact that the
overstimations tend to be the one with higher prices, thus more rooms and square footage. These large houses tend to have similar amount of bedrooms-six or seven-while the bathroom count varies more.

Code:
```
data_sorted=data.sort_values(by=['difference'])
under=data_sorted[:10]

x=np.array(under['prediction'])
y=np.array(under['prices'])
summation = 0  #variable to store the summation of differences
n = 9 #finding total number of items in list
for i in range (0,n):  #looping through each element of the list
  difference = x[i] - y[i] #calculating the difference between observed and predicted value
  squared_difference = difference**2  #taking square of the differene
  summation = summation + squared_difference  #taking a sum of all the differences
MSE = summation/n  #dividing summation by total values to obtain average
print ("The Mean Squared Error is: " , MSE)


over=data_sorted[-10:]
x=np.array(over['prediction'])
y=np.array(over['prices'])
summation = 0  #variable to store the summation of differences
n = 9 #finding total number of items in list
for i in range (0,n):  #looping through each element of the list
  difference = x[i] - y[i] #calculating the difference between observed and predicted value
  squared_difference = difference**2  #taking square of the differene
  summation = summation + squared_difference  #taking a sum of all the differences
MSE = summation/n  #dividing summation by total values to obtain average
print ("The Mean Squared Error is: " , MSE)


data['adsolute_diff']=abs(data['difference'])
accu_data=data.sort_values(by=['adsolute_diff'])
accu=accu_data[:10]

x=np.array(accu['prediction'])
y=np.array(accu['prices'])
summation = 0  #variable to store the summation of differences
n = 9 #finding total number of items in list
for i in range (0,n):  #looping through each element of the list
  difference = x[i] - y[i] #calculating the difference between observed and predicted value
  squared_difference = difference**2  #taking square of the differene
  summation = summation + squared_difference  #taking a sum of all the differences
MSE = summation/n  #dividing summation by total values to obtain average
print ("The Mean Squared Error is: " , MSE)

```
