# recipes-predictions
by Raghava Bandla (rbandla@ucsd.edu)

---

# Problem Identification

For this project, I wanted to predict the ***number of calories from a recipe*** and this is a ***regression type prediction***. The response variable in this prediction is calories because this gives me the number of calories in a recipe. Since this is a regression type, I will be using the root mean squared error as the metric to evaluate my model. I chose this one becuase I can tell if my model is overfitting, underfitting, or generalizing by analyzing the RMSE of the training and testing data. At the time of prediction, when the recipe is given, you would know the ingredients, number of steps, the number of carbs, proteins, etc. in this recipe. 

---

# Baseline Model

My baseline model is a linear regression model with 3 features: carbohydrates, total fat, and number of steps. All three of these features are quantitative because I don't think any non-quantitative features would be suitable to predict the number of calories. I left the carbohydrates and total fat columns untouched, but the number of steps columns I used a Binarizer to turn the column into values of 1 or 0 if the column value is greater than 9. I chose 9 becuase when I was doing my exploratory data analysis, I graphed the distribution of the number of steps and 9 was the median. I believe my model is good because I calulated the RMSE of the training and testing data and the results were:\

