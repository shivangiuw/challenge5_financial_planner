# Financial Planning and Analysis tools 
(with APIs and Simulations using Jupyter Notebook)

## * A financial planner for emergencies. 

1. This tool allows to calculate current balance of saving portfolio which may consist of assests like cryptocurrency, bonds and stocks by obtaining the upto date prices from APIs.
2. It also enables the individual to determine whether the current balances in savings are enough to savings to build an emergency fund into their financial plan, which is considered as thrice the monthly income.

## * A financial planner for retirement. 

1. This tool can be used to plan the retirement portfolio value  and plan the combinations of equity and bonds in the portfolio according to the risk tolerance and risk appetite to acheive the goal at the time of retirement.
2. It also helps in determining if the retirement goal portfolio value can be achieved earlier than planned, with the changes in portfolio weightage and number of years  and running simulations, if somebody chooses to go for early retirement.

## Technologies

This tool leverages python 3.7 with the following packages:

* [pandas] (https://pandas.pydata.org/docs/getting_started/index.html)- for data analysis
* [jupyter lab] (https://jupyterlab.readthedocs.io/en/stable/)- to work with notebooks, code, data and plots
* [matlplotlib] (https://matplotlib.org/stable/users/installing/index.html) - for data visualization 
* [alpaca_trade_api] (https://pypi.org/project/alpaca-trade-api/)- to interact with the Alpaca API.
* [requests] (https://docs.python-requests.org/en/master/)- to send request and access data via APIs.
* [.env] (https://www.ibm.com/docs/en/aix/7.1?topic=files-env-file)- to store the API keys for accessing data from APIs
* [load_dotenv] (https://pypi.org/project/python-dotenv/)- to read key-value pairs from a .env file
* [json] (https://www.json.org/json-en.html)- to get the data from an API in a readable format.
* [MCSimulation] (https://www.rdocumentation.org/packages/decisionSupport/versions/1.106/topics/mcSimulation)
                  - to run Montecarlo simulations with the data for forecast 

## Installation Guide

```
 conda install pandas
 pip install jupyterlab
 python -m pip install -U matplotlib
 pip install alpaca-trade-api

 ```
## Usage

## Part 1: Create a Financial Planner for Emergencies
The members will be able to use this tool to visualize their current savings. The members can then determine if they have enough reserves for an emergency fund.
To do this,we implement the following steps:

1. Current savings are determined by obtaining the current balance of different assets in current portfolio, like cryptocurrency, equity and bonds using API calls to obtain current prices of the assets.
* `For obtaining data from API, API keys need to be obtained separately.`
2. To determine if the total saving portfolio is large enough to fund the emergency funds, a comparison between current balance in portfolio and emergency fund amount `(generally emergency fund should equal to three times the member’s monthly income.)`is done using if-else statements.

## Part 2: Create a Financial Planner for retirement 

This tool will forecast the performance of the retirement portfolio in 30 years using MonteCarlo simulations which can be run with different weight adjustments given to equity and bonds to analyse and determine the best combination between the two.
It is done through following steps:

1. The tool makes an Alpaca API call via the Alpaca SDK to get historical price data of tickers of current stock and bond portfolio, for use in Monte Carlo simulations for 30 years.
2. Runs a Monte Carlo simulation of 500 samples and 30 years for the 60/40 portfolio, and then plot the results ans generate summary of results.
3. Using the current value of only the stock and bond portion of portfolio and the summary statistics generated from the Monte Carlo simulation, it can calculate lower and upper bounds for the expected value of the portfolio with a 95% confidence interval.


## Analysis & Observations:

### Financial Planner for Emergencies

1. Evaluate the Cryptocurrency Wallet
In this section,we determine the current value of a member’s cryptocurrency wallet by collecting the current prices for the Bitcoin and Ethereum cryptocurrencies using API and Python Requests library for current date prices.
* Assume that the member holds the 1.2 Bitcoins (BTC) and 5.3 Ethereum coins (ETH) and monthly income is USD 12000.
* The wallet balance will differ slightly as the using API here is picking current prices of the cryptocurrencies.

`Results:`The current cryptocurrency wallet balance is USD USD 67832.83 where current price of BTC is USD USD 42426.00 and current price of ETH is USD 3192.76.

2. Evaluate the Stock and Bond Holdings by Using the Alpaca SDK
In this section, we determine the current value of a member’s stock and bond holdings. We make an API call to Alpaca via the Alpaca SDK to get the current closing prices of the SPDR S&P 500 ETF Trust (ticker: SPY) and of the iShares Core US Aggregate Bond ETF (ticker: AGG) for the date '2021-12-31' .
* Assume that the member holds 110 shares of SPY, which represents the stock portion of their portfolio, and 200 shares of AGG, which represents the bond portion.

`Results:`The current balance of stock and bond portion of portfolio is USD 75055.90 wherein current value of stock portfolio is USD 52237.90  with SPY closing price is 474.89, and current value of bond portfolio is USD 22818.00 with AGG closing price: 114.09.

3. Evaluate the Emergency Fund
In this section, we add the valuations of the cryptocurrency wallet to that of the stock and bond portions of the portfolio and compare the entire savings portfolio value to the emergency saving fund value (three times of monthly income) using conditional if-else statements to determine if enough savings are available to build an emergency fund into financial plan.
 
`Results:`The total value of entire savings portfolio is USD USD 142888.73 whereas the emergency funds required are USD 36000.00 (assuming the monthly income USD 12000.00). Here we have enough money in the savings for emergency fund.

![](images/portfolio_composition.png)


### Financial Planner for Retirement

* Because a random number generator is used to run each live Monte Carlo simulation, results will differ slightly from the below mentioned statistical results and plots.

1. Creating the Monte Carlo Simulation
In this section, we use the Alpaca API to get historical closing prices for three year period between'2018-12-31 and '2021-12-31 for the retirement portfolio tickers.
Further, we then run Monte Carlo simulations  with a traditional portfolio split: 60% stocks (SPY) and 40% bonds (AGG) to forecast the portfolio performance for 30 years from now using MCForecastTools library to create a Monte Carlo simulation of 500 samples and plot the results with generating summary statistics

`Results:`

![](images/500_MCsimulations_30 years.png)

![](images/probability_distribution _30_years.png)

The summary statistics from the 30-year Monte Carlo simulations are:
count            500.000000
mean             104.577924
std              102.871575
min                6.213693
25%               47.047875
50%               79.273617
75%              130.190033
max             1374.766273
95% CI Lower      16.915594
95% CI Upper     331.432303
Name: 7560, dtype: float64

2. Analyze the Retirement Portfolio Forecasts

`Results:` With a traditional 60/40 portfolio split: 60% stocks (SPY) and 40% bonds (AGG) over the next 30 years, there is a 95% chance that current balance of USD 75,055.90 in the portfolio will end within in the range of USD USD 1,269,615.12 and USD 24,875,949.79 as calculated by running a Monte Carlo simulation of 500 samples.

3. Forecast Cumulative Returns in 10 Years
Here, we adjust the retirement portfolio weights to the composition of 20% bonds and 80% stocks and run a new Monte Carlo simulation for 10 years to find out if the changes will allow members to retire earlier and plot the results with generating summary statistics.Because of the shortened investment horizon (30 years to 10 years), the portfolio needs to invest more heavily in the riskier asset—that is, stock—to help accumulate wealth for retirement.
`Results:`

![](images/10_year_MC simulation.png)

![](images/probability_distribution_10_year _MC.png)


The summary statistics from the 10-year Monte Carlo simulations are:
count           500.000000
mean              6.856147
std               3.989233
min               1.172067
25%               4.236635
50%               5.951870
75%               8.288956
max              29.833402
95% CI Lower      1.998723
95% CI Upper     17.336753
Adjusting the retirement portfolio weights to the composition of 20% bonds and 80% stocks(running Monte Carlo Simulation)for 10 years , there is a 95% chance that current balance of USD 75,055.90 in the portfolio will end within the range of USD 150,015.95 and USD 1,301,225.59. 


`Will weighting the portfolio more heavily to stocks allow the credit union members to retire after only 10 years?`
Answer: Above observations confirm that if the person aims to achieve a retirement goal of minimum USD 1,269,615.12,it `may be` achieved over the next 10 years if more weightage is given to stocks to earn higher returns with higher risk as compared to traditional portfolio split, which is evident from upper value of the range i.e. USD 1,301,225.59 at 95% confidence intervals obtained using Monte Carlo simulation for the next 10 year.
However at the same time there are equal chances that portfolio may end up with the lower value of USD 150,015.95 in 10 years. 
So, running more simulations for different weights for equity and bonds and higher time periods than 10 years with the retirement goal value and risk appetite in consideration, it can provide an answer to the number of member's early retirement years or vice versa.
