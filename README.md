# New York Stock Exchange Analysis

This repository contains code written in Python in order to deal with a fun problem involving the Kaggle "[Huge Stock Market Dataset](https://www.kaggle.com/borismarjanovic/price-volume-data-for-all-us-stocks-etfs/version/3)", which contains the daily prices and volumes of all U.S. stocks and ETFs until 11/10/2017. The story goes like this:

> Suppose you've found a way to trade stocks in any date in the past, starting from 1/1/1960 with a bank account of 1$. The goal is to find a sequence of N trades, where N ≤ 100000, that maximizes your profit using a heuristic approach (i.e. avoid reinforcement learning or optimization). The rules are the following:
> - The allowed types of trades (actions) are *buy* and *sell*.
> - Trades can be performed at three distinct time windows within a day: the *open* window, which precedes the *low* and *high* window, which in turn precede the *close* window. All trades have to be performed in chronological order within the same day. For example, you cannot acquire 10 units of one stock at low and sell them at open of the same day.
> - The money used to buy stocks, or the stocks for sale, need to be available before performing each window's trades. For example, you can sell at high 30 units that you bought at open of the same day, however you can't sell them if you bought them at low, since low and high belong in the same time window.
> - The total number of a stock's units bought/sold during a day cannot exceed 10% of the stock's volume during that day.
> - Supposing that before the open window of a day you have n ≥ 0 units of a specific stock, you are not allowed to buy more than n+1 units of this stock during that day. For example, if you have 20 units of AAPL before the open window of a day, then you can buy **at most** 21 units of AAPL during that day, even if you intend to sell them before the close window.

The first solution that comes to mind involves intra-day trading: sort the buy-open/sell-high and buy-low/sell-close sequences of actions for every day by descending order of profit and perform as many such transactions as possible, without breaking the 100000 total transactions limit. However, this approach is completely negated due to the final restriction, which requires already having n units of one stock in order to be able to acquire up to n+1 additional units. This means that one must first find a way to accumulate stocks before proceeding to perform intra-day trading with them. A proposed solution is the algorithm presented in the following scheme.

<p align="center">
  <img src="https://srigas.me/github/stocks-scheme.png" width="800" />
</p>

With some preprocessing and exploratory analysis of the stocks and with a run-time of less than one minute in wall time, this algorithm achieves a profit of **707 billion dollars** in just **73880 transactions**, as seen in the valuation graph below, where the Balance corresponds to the available money (in the wallet), while the Portfolio corresponds to the stock market value of any unsold stocks.

<p align="center">
  <img src="https://srigas.me/github/stocks-valuation.png" width="800" />
</p>
