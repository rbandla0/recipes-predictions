# HOW MANY CALORIES ARE IN THIS MEAL?
by Raghava Bandla (rbandla@ucsd.edu)

---

# Problem Identification

For this project, I wanted to predict the ***number of calories from a recipe*** and this is a ***regression type prediction***. The response variable in this prediction is calories because this gives me the number of calories in a recipe. Since this is a regression type, I will be using the root mean squared error as the metric to evaluate my model. I chose this one becuase I can tell if my model is overfitting, underfitting, or generalizing by analyzing the RMSE of the training and testing data. At the time of prediction, when the recipe is given, you would know the ingredients, number of steps, the number of carbs, proteins, etc. in this recipe. 

---

# Baseline Model

My baseline model is a linear regression model with 3 features: carbohydrates, total fat, and number of steps. All three of these features are quantitative because I don't think any non-quantitative features would be suitable to predict the number of calories. I left the carbohydrates and total fat columns untouched, but the number of steps columns I used a Binarizer to turn the column into values of 1 or 0 if the column value is greater than 9. I chose 9 becuase when I was doing my exploratory data analysis, I graphed the distribution of the number of steps and 9 was the median. I believe my model is good because I calulated the RMSE of the training and testing data and the results were:\
\
***Baseline Model Training Data RMSE:*** 102.63272690417527\
***Baseline Model Testing Data RMSE:*** 115.41697770169566\
\
Based on these results, the RMSE aren't too far apart from each other, meaning the model wasn't overfitting or underfitting, but generalized just fine. This is why I believe this baseline model is good. 

---

# Final Model

The features I added were including the protein column in my prediction model, while also standardizing the carbohydrates, total fat, and protein columns. Then I used a quantile transformer to make these three features a normal distribution. The binarizer stayed the same but I changed its parameter. I added the protein column because through researching more about calories and its correlation with nutrients, I realized proteins are a big part of determining how many calories are in a meal. I standardized those three columns because it scales the values to the variance, decreasing the range and preventing the wide range from dominating the model. I used a quantile transformer because it reduced the impact of outliers and exemplified the most frequent values.\
\
The model I chose was a linear regression model with multiple features and the hyperparameters that ended up performing the best were:\
\
***threshold : 4\
n_quantiles : 15000***\
\
I used GridSearchCV to select the best hyperparameters and the result was the Binarizer threshold being 4 and the number of quantiles in the QuantileTransformer being 15000. This made a significant imporvement on my baseline model because the RMSE decreased with the final model. The lower the RMSE, the better the model is at predicting data. Also, my training and testing data were very similar, meaning the model is good at predicting the data.\
\
***Final Model Training Data RMSE:*** 47.329709539841424\
***Final Model Testing Data RMSE:*** 47.413034319796395\
\

---

# Fairness Analysis

***Group X:*** Recipes taking less than or equal to 60 minutes (short recipes)\
\
***Group Y:*** Recipes taking longer than 60 minutes (long recipes)\
\
***Evaluation Metric:*** Root Mean Squared Error (RMSE)\
\
***Null Hypothesis:*** My model is fair. Its RMSE for short recipes and long recipes are roughly the same, and any differences are due to random chance.\
\
***Alternative Hypothesis:*** My model is unfair. Its RMSE varies depending on if the recipe is short or long.\
\
***Test Statistic:*** Absolute Difference\
\
***Significance Level:*** 0.05\
\
***Resulting P-value:*** 0.727\
\
***Conclusion:*** Since the p-value is greater than the significance level, we fail to reject the null because there isn't enough statistical evidence to reject it. 
