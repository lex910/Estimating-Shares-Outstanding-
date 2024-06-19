# Estimating-Shares-Outstanding-
Using random forest and decision trees for variable selection in estimating shares outstanding 

-using 74 variables from the "fundamentals" dataset

## Build random forest model 
-split data into 70% training 30% test
Mean Squared Error OOS: 1.3024272022208782e+17

## Random forest min_samples_split=3
MSE with min_samples_split=3 Random Forest model OOS: 1.377613360667223e+17

When we use the dafault hyperparameters for a random forest model, min_samples_split=2. When we change the hyperparameters to make min_samples_split=3 the MSE increases. When it is equal to 2, the tree can split with there being a minimum of 2 samples in the model, meaning each leaf would only contain 1 observation. This can lead to overfitting since every sample is perfectly fit to its one leaf. When when change the parameter to 3, there must be 3 samples present for a split to occur. Bias may increase becasue of the lesser number of splits, but it helps prevent overfitting and prevents the model from fitting too close to any noise and being more generalized to unseen data.

## Variable importance using mean decrease in impurity and permutation feature importance 

![Screenshot 2024-06-19 at 1 16 13 PM](https://github.com/lex910/Estimating-Shares-Outstanding-/assets/101606445/b8f5039c-820b-4b1b-988a-264d1076d8af)
![Screenshot 2024-06-19 at 1 16 34 PM](https://github.com/lex910/Estimating-Shares-Outstanding-/assets/101606445/c42a0caa-c0ba-46aa-bb1f-a7085d335d71)


Mean decrease in impurity calcultaes how much each split contributes to a reduction in deviance. The variable with the largest change is the most important. Permutation feature importance first computes the deviance of the original forest. Then it shuffles on whole variable and computes the deviance again. If the deviance goes up a lot, it indicates that the varible is used often in the random forest since all of the y values go bad, indicating variable importance. Looking at the bar chart above, we can see that variables used to predict estimated shares outstanding typically appear to be more significant using mean decrease in impurity. Total equity, net cash flow, total liabilities and equity, total assets, and short term investments are the top variables using mean decrease in impurity whereas total equity, net cash flow, earnings per share, total assets,and short term investments are the top for permutation feature importance. There is only a small change with the third most important variable between the two methods.

## Compare with a lasso model 
MSE with min_samples_split=2 Random Forest model: 1.3024272022208782e+17
MSE with min_samples_split=3 Random Forest model: 1.377613360667223e+17
Lasso MSE: 1.8280438257199008e+17

Using lasso regression increases the MSE compared to the random forest model min_samples_split=3. Using a random forest model helps with overfitting when we assign an appropriate min split beacuse of the use of bootstrap to make many samples. Random forest accounts for interactions and eliminates the need for cross validation. Boostrap aggrigation ensures that all noise is averaged out accross samples so they do not effect our estimates. Random forest can also handle non-linear relationships because boootstrap is a nonparametric technique but also results in a loss of interpretability for an optimal tree. In this case, reandom forest may be a better model since lasso results in higher MSE potentially because of non-linear relationships in the data.

