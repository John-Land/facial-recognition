# Enterprise Value to Sales Ratio (Stock Price) Prediction project

A traditional measure of whether a stock is expensive or cheap, is to use a valuation multiple. <br>
A valuation multiple relates the market value of an asset relative to a key statistic that is assumed to relate to that value. <br>

One of the most widely used valuation multiples is the Enterprise Value to Sales (Revenue) multiple, short EV/Sales. <br>
This is the ratio between the Enterprise Value of a company, divided by the company’s Revenue. <br>
The Enterprise value is the total market value of the company’s equity and net debt. <br>

In this project I try to use the fundamental drivers of the EV/Sales ratio, based on financial theory, to predict the EV/Sales ratios (pricing) for companies listed on the US stock market. 

## Required Python Packages
- Numpy
- Pandas
- Scikit Learn
- Matplotlib
- Seaborn

## Data Used
The raw data was downloaded from the data provider "Finbox" on 24/10/2021, for all companies traded on the US market with market cap >= 1 bil USD. <br>
Finbox sources their data from the leading financial data provider "S&P Global Market Intelligence".<br><br>
The raw data consists of the latest financial KPIs from the companies’ financial statements, as well as the latest analyst projections. <br>
Refer to below link: https://finbox.com/about <br>

Based on financial theory, we will use below KPIs which relate to the fundamental drivers, to predict EV/Sales. (Refer 1.1 in the notebook for derivation of fundamental drivers) <br>

| Financial KPIs used for prediction | Related Fundamental Driver | Comment |
|---|---|---|
| Revenue_Forecast_CAGR_10y | Growth | Average Revenue growth projections for the next 10 years by analysts. |
| Avg_EBITDA_Margin_Forecast_10y | Ebitda Margin | Average Ebitda Margin projections for the next 10 years by analysts. |
| Avg_Capex_Margin_5y | Re-investment requirement | Average Capex as % of Revenues paid in the past 5 years. Proxy for re-investment requirement. |
| Marginal_Tax_Rate | Taxes | Latest marginal tax rate paid. Proxy for future expected Tax expenses. |
| Net_Debt_perc_Market_Cap | Risk | The more leverage/debt the company has, the riskier it is for both equity and debt capital providers. |
| Sector | Risk | Some Sectors are riskier than others. The risk of a company is partially determined by the business it operates in. |
| Operating_Region | Risk | Some regions are riskier than others, due to political or operational risk. The risk of a company is partially determined by where it does business. |

## Training

After pre-processing and outlier removal, the dataset consisted of 3730 individual companies. <br>
This dataset was split randomly into 80% for training, and 20% for testing.

Multiple algorithms were fit via 5-fold cross-validation and grid search on the training set, to find the best hyperparameters per algorithm. <br>
For model selection, the models were compare based on average r2 on the validation folds of the training set. <br>
The best model was selected based on the highest average r2 achieved on the validation folds of the training set. <br>
For the best model, an out of sample error estimation was then obtained based on predictions on the test set.

## Evaluation and model selection with cross-validation

Below performance was achieved by the different candidate models on training set cross validation folds.

|                 Model 	| CV_r2 	| CV_mae 	| CV_rmse 	|
|----------------------:	|------:	|-------:	|--------:	|
|                 Ridge 	| 0.524 	|  2.156 	|   3.262 	|
|                 Lasso 	| 0.524 	|  2.158 	|   3.262 	|
|   KNeighborsRegressor 	| 0.576 	|  1.919 	|   3.078 	|
|            SVR linear 	| 0.513 	|  2.258 	|   3.300 	|
|               SVR rbf 	| 0.601 	|  1.715 	|   2.985 	|
|         Decision Tree 	| 0.467 	|  2.119 	|   3.456 	|
| RandomForestRegressor 	| 0.619 	|  1.780 	|   2.919 	|
|          MLPRegressor 	| 0.610 	|  1.827 	|   2.947 	|
|       VotingRegressor 	| 0.635 	|  1.720 	|   2.856 	|

The model selected with the best Cross Validation performance was the VotingRegressor, with an average cross validation r2 of 63.5%.

|           Model 	| CV_r2 	| CV_mae 	| CV_rmse 	|
|----------------:	|------:	|-------:	|--------:	|
| VotingRegressor 	| 0.635 	|  1.720 	|   2.856 	|

## Results on out of sample test-set

The model selected with the best Cross Validation performance was the VotingRegressor.
Below out of sample performance was achieved by the best model on the test set.

|           Model 	| Test_r2 	| Test_mae 	| Test_rmse 	|
|----------------:	|--------:	|---------:	|----------:	|
| VotingRegressor 	|   0.608 	|    1.732 	|     3.041 	|

The model selected with the best Cross Validation performance was the VotingRegressor, with an out of sample test set r2 of 60.8%.

## Appendix


