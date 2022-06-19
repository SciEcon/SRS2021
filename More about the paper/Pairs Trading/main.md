# Methodology


## Algorithm

Pairs trading is the first known case of Statistical Arbitrage for asset trading, it utilizes statistical methods to generate excess returns [[1]](https://doi.org/10.1080/14697680903124632)[[2]](doi.org/10.1016/j.physa.2010.01.045). [[3]](https://www.wiley.com/en-us/Pairs+Trading%3A+Quantitative+Methods+and+Analysis-p-9780471460671) traces statistical arbitrage back to the 1980s Wall Street when a team of mathematicians, physicists, and computer scientists at Morgan Stanley implemented statistical methods for financial problems [[4]](https://www.wiley.com/en-us/Pairs+Trading%3A+Quantitative+Methods+and+Analysis-p-9780471460671). [[5]](https://aisel.aisnet.org/icis2019/blockchain_fintech/blockchain_fintech/20) first introduce Machine Learning (ML) methods to economics and a subsequent study uses Neural Networks to predict IBM daily stock returns [[6]](https://aisel.aisnet.org/icis2019/blockchain_fintech/blockchain_fintech/20) [[7]](doi.org/10.1109/icnn.1988.23959) . Since then, more complex ML models have been applied to statistical arbitrage, among which are Deep Learning Models, Random Forests, and Supervised Learning algorithms for classifications [[8]](10.1016/j.ejor.2016.10.031).  In general, ML Algorithms tend to perform better. For instance, [[9]](10.1016/j.ejor.2016.10.031) shows the superior performance of their ML algorithm in times of high uncertainty such as the dot-com bubble and the 2008 financial crisis. 

Figure 1 represents the pipeline for the pairs trading case study. The idea behind pairs trading is to find pairs that have historically been moving together so that when they diverge, we short the overpriced asset and long the underpriced and then sell/payback once they converge again. In this study, we use pairs trading using two different approaches previously applied on US stocks and ETFs [[10]](http://www-stat.wharton.upenn.edu/~steele/Courses/434/434Context/PairsTrading/PairsTradingGGR.pdf) [[11]](10.1016/j.eswa.2020.113490).

The prcoedure is described in more detail in Figure 2. i) We connect to different databases, namely Yahoo Finance, Alpha Vantage API, and Coin Metrics ii) and retrieve historical data iii) we then input the prices into our Pairs Selection class which will create our portfolio. iv) Once our portfolio of assets is defined, we can generate the Buy and Sell signals v) once done, we can start trading and choose different settings for our trading e.g. the kind of spread to use. vi) To finish, we can also easily call methods to easily observe the trading decisions across the time window.

Figure 1 represents the general pipeline for pairs trading.

![Pairs trading Analysis: The Algorithm](https://github.com/SciEcon/SRS2021/blob/main/fig/fig2_4.png)
*Figure 1: Pairs trading: the algorithm. The algorithm starts from the left with the inputs (pink), we get our data sources from Alpha Vantage API (https://www.alphavantage.co/documentation/). The raw input variables will be historical closing prices and the subsets of assets to be tested will be divided into two groups, namely S\&P500 stocks only and Digital Currencies (DeFi tokens and Cryptocurrencies) only. Once the historical data and the subset of assets to trade are determined, we perform our analysis (blue) which is the pairs selection process using either Machine Learning or Brute Force. Then we calculate the spread using either a normalized or a simple spread which is explained in detail in section Spread. The spread then allows defining the thresholds which are then used to produce the first element of the output dashboard (green), namely the buy/sell/exit signals. Lastly, we will evaluate the performance by using ROI and Sharpe Ratio.

### Pair Selection
The process of Pairs Selection can be computed in several ways. The first method to be analyzed in this section is based on the work from Gatev, Goetzmann, and Rouwenhorst (1998) [[12]](http://www-stat.wharton.upenn.edu/~steele/Courses/434/434Context/PairsTrading/PairsTradingGGR.pdf) This can be considered a brute force algorithm since it consists of comparing every possible pair, which implies that there will be in total $\frac{n(n+1)}{2}$ different pairs to compare. The metric used by the authors to determine the pairs that have been historically moving together is called a Sum of Standard Deviations ($SDD$) which can be defined as

    $SDD = \sum_{t\in F}\left(\frac{P^X_t}{P^X_1} - \frac{P^Y_t}{P^Y_1}\right)$

Where $t$ is a day in the Formation period $F$.

However, comparing every single pair results computationally very expensive. Furthermore, some pairs behave completely differently from each other but we still dedicate the same amount of resources to them than to pairs that are more similar to each other. Therefore, we also implemented a Machine Learning solution [[13]](https://www.sciencedirect.com/science/article/abs/pii/S0957417420303146). By using an unsupervised learning approach, it is possible to reduce the energy consumption on pairs trading.

The first step using the Machine Learning approach is to compute the daily returns $ROI_t$

    $ROI_t = \frac{P_t}{P_{t-1}}-1 $

through the formation period. We then perform Principal Component Analysis (PCA) to reduce the number of dimensions for each data point. Then, we input the resulting matrix into an Unsupervised Learning algorithm, namely OPTICS, which clusters data into different subsets and excludes those that are too far apart to be clustered.

This process allows to reduce the time complexity from $O(n^2)$ to $O(n^2_1 + n^2_2 + ... + n^2_k)$ where $k << n$ and $n_i << n$. Therefore, $O(n^2_1 + n^2_2 + ... + n^2_k) << O(n^2)$.

### Criteria
One of the most significant differences, however, is the way pairs are filtered out. While [[14]](http://www-stat.wharton.upenn.edu/~steele/Courses/434/434Context/PairsTrading/PairsTradingGGR.pdf) only focus on the Sum of Standard Deviations to determine whether two stocks have been historically moving together [[15]](http://www-stat.wharton.upenn.edu/~steele/Courses/434/434Context/PairsTrading/PairsTradingGGR.pdf), [[16]](https://www.sciencedirect.com/science/article/abs/pii/S0957417420303146) implement additional criteria to not only determine a historical relationship by applying a co-integration test [[17]](https://www.jstor.org/stable/1913236), but also the feasibility of trading with such pair by testing on the features of the Spread (Hurst exponent, Half-life, and the number of times it crosses the mean).

### Spread

Lastly, these papers propose two different forms of calculating the spread between two pairs. [[18]](http://www-stat.wharton.upenn.edu/~steele/Courses/434/434Context/PairsTrading/PairsTradingGGR.pdf) use what we call a simple spread $S_{\text{simple}}$


    $S_{\text{simple}} = \sum_{t\in F}\left(P^A_t - P^B_t\right)$


Where $P^X_t$ is the price of asset $X$ at time $t$. On the other hand, Sarmento and Horta (2020) use what we call a normalized spread $S_{\text{normal}}$

    $S_{\text{normal}} = \sum_{t \in F} \left(\frac{P^A_t}{P^A_0} - \frac{P^B_t}{P^B_0}\right)$

Where $P^X_0$ is the price of asset $X$ at the beginning of the Formation period $F$. Also notice that $SDD$ and $S_{\text{normal}}$ are equivalent but serve two different purposes, hence, we differentiate between these two.


## Data

We used data from Alpha Vantage API for Pairs Formation and backtesting. A description of the raw data can be found in Table 1.

| **Variable name** | **Frequency** | **Unit**   |
|:-----------------:|:-------------:|:----------:|
| Date              | daily         | YYYY-MM-DD |
| Close             | daily         | USD        |
| Asset Name        | -             | -          |

*Table 1: Pairs Trading: Data 
Data Source: Alpha Vantage API. This table shows the raw data that we retrieved from the APIs. Close corresponds to close price corresponding to the given asset at a given date.*


Besides the raw data, we later produced data corresponding to each pair of assets which can be found in Table 2. The p-value is obtained after performing the cointegration test [[19]](doi.org/10.2307/1913236). The closer the value it is to zero, the more likely it is to reject the null hypothesis, in other words, the closer to zero the more likely it is that the two assets' historical prices are correlated.
The Hurst Exponent is a test to assess the mean-reverting or trending characteristic of a time series [[20]](https://www.wiley.com/en-us/Algorithmic+Trading:+Winning+Strategies+and+Their+Rationale-p-9781118460146). Our time series here is the spread of two assets. When the Hurst exponent is closer to 0, it means that it behaves more like a mean-reverting time-series, when it is equal to 0.5 then it means it is similar to a random walk, and when it is closer to 1 then it means the series is increasingly trending.
The Half-life test will return a value $\lambda$ that tells how long does it take for the spread to mean-revert [[21]](https://www.wiley.com/en-us/Algorithmic+Trading:+Winning+Strategies+and+Their+Rationale-p-9781118460146).
The last metric is just a counter of how many times the Spread goes across the mean.

| **Variable name**       | **Description**                                                                                                    |
|:-----------------------:|:------------------------------------------------------------------------------------------------------------------:|
| P-value                 | P-value from Engle and Granger's cointegration test                                                                |
| Hurst Exponent          | The Hurst exponent is a value between 0 and 1 that serves to evaluate the mean-reversion property of a time-series |
| Half-life               | A value $\lambda$ that tells how long it takes for a time series to mean-revert                                    |
| Times Crossing the Mean | Times the spread goes across the mean during the formation period                                                  |


*Table 2: Pairs Trading: Calculated Variables. This table shows a detailed description of each of the calculated variables as in [[22]](doi.org/10.2307/1913236)[[23]](https://www.wiley.com/en-us/Algorithmic+Trading:+Winning+Strategies+and+Their+Rationale-p-9781118460146)*

### Pairs Trading Conditions
Trading signals are generated in the following way. We short Asset A and buy Asset B when the spread goes above the short signal. Similarly, we buy Asset A and short Asset B when the spread goes below the buy signal. Finally, when the spread goes across the exit signal we exit the position (sell or payback accordingly). The thresholds are set up according to Table 3. Where $\sigma$ is the standard deviation of the given spread and $\mu$ is the average of that same spread.

| **Threshold** | **Value Using $\text{S}_{\text{simple}}$** | **Value Using $\text{S}_{\text{normal}}$** |
|:-------------:|:------------------------------------------:|:------------------------------------------:|
| Short         | $2\sigma$                                  | $\mu + 2\sigma$                            |
| Buy           | $-2\sigma$                                 | $\mu - 2\sigma$                            |
| Exit          | $0$                                        | $\mu$                                      |   |

*Table 3: Pairs Trading: Trading Signals 
 This tells us the values that the thresholds will get given the Spread chosen. Short, Buy, and Exit represent the short threshold, buy threshold, and exit threshold accordingly.*


# Result
  
Since the Pairs Trading strategy analyses many assets at a time, we decided that it was worth it to build portfolios instead of trading single pairs. Because we had two different approaches to choosing how to trade the assets, we have defined two methods: the Machine Learning method [[24]](doi.org/10.1016/j.eswa.2020.113490) and the Brute Force method [[25]](http://www-stat.wharton.upenn.edu/~steele/Courses/434/434Context/PairsTrading/PairsTradingGGR.pdf).

We build 8 different portfolios using S\&P500 and Digital Currencies (which includes Cryptocurrencies and DeFi tokens). For the first 4 portfolios we only formed pairs using S\&P500 data, we tested using a normal spread and a simple spread as well as using both the Machine Learning and the Brute Force approach. For the next 4, we used a similar approach, except that instead of using S\&P500 we used the list of Digital Currencies available in AlphaVantage API. Hence, we got the following Portfolios shown in Table 4.



| **ID** | **Assets**         | **Spread**          | **Selection Method** |
|:------:|:------------------:|:-------------------:|:--------------------:|
| 1      | S&P                | S$_{\text{normal}}$ | Machine Learning     |
| 2      | S&P                | S$_{\text{normal}}$ | Brute Force          |
| 3      | S&P                | S$_{\text{simple}}$ | Machine Learning     |
| 4      | S&P                | S$_{\text{simple}}$ | Brute Force          |
| 5      | Digital Currencies | S$_{\text{normal}}$ | Machine Learning     |
| 6      | Digital Currencies | S$_{\text{normal}}$ | Brute Force          |
| 7      | Digital Currencies | S$_{\text{simple}}$ | Machine Learning     |
| 8      | Digital Currencies | S$_{\text{simple}}$ | Brute Force          |



*Table 4: Pairs Trading: Portfolios. S\&P500 includes all stocks listed in the S\&P500 by 3/12/2022. Digital Currencies includes all digital currencies listed in Alpha Vantage by 3/12/2022/. The Machine Learning method makes reference to the method described in [[26]](doi.org/10.1016/j.eswa.2020.113490), while Brute Force makes reference to the one described in [[27]](http://www-stat.wharton.upenn.edu/~steele/Courses/434/434Context/PairsTrading/PairsTradingGGR.pdf).*

On a single pair level, however, we are able to disseminate the results. Here, we analyse a pair in portfolio \#5, we have a pair composed of Binance USD token (BUSD) and the EOS.IO token (EOS).

Figure 3 shows how are the trading signals defined. There, the pink continuous line represents EOS closing price. The blue continuous line represents BUSD closing price. The black dashed line represents the normal spread $\text{S}_{\text{normal}}$. And the pink dashed line is the short threshold while the blue dashed line is the buy threshold. 
As previously discussed we short Asset A (BUSD in this case) and buy Asset B (EOS in this case) when the spread line goes above the short threshold. The opposite happens when the spread goes below the buy threshold. Lastly, we exit the position when it goes across the exit signal (sell or payback accordingly).

Figure 4 shows the cash flow of Pairs Trading on BUSD and EOS. In addition to depicting cash, holding, and total, we depict debt which is the amount of money that we owe when we short an asset. It can be observed that cash is mainly steady, however, this can be misleading. We first use cash to buy one asset, then we borrow and simultaneously sell the second asset, therefore, while that extra amount of cash is reflected in the cash flow, it rests in the form of debt. Therefore, $Total$ is nothing but $Cash + Holding - Debt$. In Figure 4, we observe that the total amount is overall increasing over time.

As we can observe in Figure 5, shoring EOS becomes profitable because its price drops between the two signals, hence, the debt drops. While BUSD remains almost steady. We still produced an ROI of 24.92\% which is significantly better than Buy \& Hold's ROI of 0.00\% on that same pair. Similarly, the Sharpe Ratio for the pairs trading strategy is 0.819 while that of Buy \& Hold is only 0.141.

![BUSD \& EOS Buy \& Sell Signal: Pairs Trading](https://github.com/SciEcon/SRS2021/blob/main/fig/fig3_4_a.png)
*Figure 3: BUSD \& EOS Buy \& Sell Signal: Pairs Trading*

![BUSD \& EOS Portfolio time series: Pairs Trading](https://github.com/SciEcon/SRS2021/blob/main/fig/fig3_4_b.png)
*Figure 4: BUSD \& EOS Portfolio time series: Pairs Trading*

![BUSD \& EOS Gross ROI: Pairs Trading vs buy-and-hold; Pairs Trading strategy ROI: 24.92\% ; Buy \& hold strategy ROI: 0.00\%](https://github.com/SciEcon/SRS2021/blob/main/fig/fig3_4_c.png)
*Figure 5: BUSD \& EOS Gross ROI: Pairs Trading vs buy-and-hold; Pairs Trading strategy ROI: 24.92\% ; Buy \& hold strategy ROI: 0.00\%*


# Appendix

Figures below show the generated buy-and-sell signals using the pairs trading strategy, the portfolio evolution, the ROI, and the Sharpe Ratio for a pairs of stocks in portfolio \#3--namely Kellogg (K) and Kimberly Clark Corp (KMB).

![K and KMB Buy-and-sell Signal: Pairs Trading](https://github.com/SciEcon/SRS2021/blob/main/fig/fig5_4_a.png)
*Figure 6: K and KMB Buy-and-sell Signal: Pairs Trading*


![K and KMB Portfolio Time Series: Pairs Trading](https://github.com/SciEcon/SRS2021/blob/main/fig/fig5_4_b.png)
*Figure 7: K and KMB Portfolio Time Series: Pairs Trading*

![K and KMB Gross ROI: Pairs Trading vs Buy-And-Hold; Pairs trading ROI: 3.50 \%; Buy \& hold strategy ROI: -0.04\%](https://github.com/SciEcon/SRS2021/blob/main/fig/fig5_4_c.png)
*Figure 8: K and KMB Gross ROI: Pairs Trading vs Buy-And-Hold; Pairs trading ROI: 3.50 \%; Buy \& hold strategy ROI: -0.04\%*

![K and KMB Sharpe Ratio: Pairs Trading vs Buy-And-Hold; Pairs trading Sharpe Ratio: 0.95; Buy \& hold strategy Sharpe Ratio: -0.45](https://github.com/SciEcon/SRS2021/blob/main/fig/fig5_4_d.png)
*Figure 9: K and KMB Sharpe Ratio: Pairs Trading vs Buy-And-Hold; Pairs trading Sharpe Ratio: 0.95; Buy \& hold strategy Sharpe Ratio: -0.45*

