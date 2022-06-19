# Methodology
## Algorithm

Public mood is another valuable indicator to predict the change in market value of financial assets. Moreover, the advances in computational algorithms, coined Sentiment Analysis or Emotion AI, make public mood quantifiable. Teclock [[1]](https://onlinelibrary.wiley.com/doi/10.1111/j.1540-6261.2007.01232.x) first proposes a newsreader algorithm that utilizes the information in news, tweets, blogs, and surveys to predict stock price. 
Previous research applied a variety of methods in Natural Language Processing (NLP) to quantify sentiments, which significantly improves the prediction of stock prices [[2]](https://www.sciencedirect.com/science/article/pii/S187775031100007X?via%3Dihub) [[3]](https://www.tandfonline.com/doi/full/10.1080/14697688.2012.672762).

A majority of studies have examined Twitter’s predictive power on stock market value such as Dow Jones Industrial Average (DJIA) and S\&P 500 [[2]](https://www.sciencedirect.com/science/article/pii/S187775031100007X?via%3Dihub) [[4]](https://www.researchgate.net/publication/261843641_Stock_Prediction_Using_Event-Based_Sentiment_Analysis) [[5]](https://www.sciencedirect.com/science/article/pii/S1877042811023895) [[6]](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2517025) [[7]](https://econpapers.repec.org/article/eeeintfin/v_3a65_3ay_3a2020_3ai_3ac_3as104244312030072x.htm). These works follow a general event study framework including sentiment analysis with a regression model or a granger causality test. Some also extend to price movement prediction or trading strategy designs through deep learning models [[2]](https://www.sciencedirect.com/science/article/pii/S187775031100007X?via%3Dihub) [[8]](https://www.mdpi.com/1099-4300/21/6/589). The studies differ in sentiment analysis approaches when "computationally" evaluate how positive, negative or neutral a piece of text is. 
One main approach is lexicon-based methods that use labeled lexical features to determine the polarization of the text piece. 
Examples include Valence Aware Dictionary and Entiment Reasoner [[6]](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2517025), Loughran and McDonald financial corpus [[9]](https://onlinelibrary.wiley.com/doi/abs/10.1111/j.1540-6261.2010.01625.x), and Harvard IV-4 psychological corpus. Another approach is supervised learning, which trained the classifiers through existing annotated data to label the tweets. 1-4 days is observed to be the most effective predictive period for Tweets in the financial market [[7]](https://econpapers.repec.org/article/eeeintfin/v_3a65_3ay_3a2020_3ai_3ac_3as104244312030072x.htm).

Existing literature in sentiment analysis intended for price prediction without informing investment strategies. We move forward by incorporating newsreader algorithms to other tech indicators that generate buy and sell signals. 

![Sentiment Analysis: The Algorithm](https://github.com/SciEcon/SRS2021/blob/main/fig/fig2_3.png)
*Figure 1: Sentiment analysis: the algorithm. Following the general pipeline described in Figure 2. The algorithm starts from the left with the inputs (pink), we get our data sources from Yahoo Finance API, Alpha Vantage API, and snscrape API [[10]](https://pypi.org/project/yfinance/) [[11]](https://www.alphavantage.co/documentation/) [[12]](https://github.com/JustAnotherArchivist/snscrape). The raw input variables will be historical closing prices and tweets online comments with specific hashtags. Once the historical data, tweets, and the subset of assets to trade are determined, we perform our analysis (blue) which is the natural language processing [[13]](https://ojs.aaai.org/index.php/ICWSM/article/view/14550) and the exponential moving average calculation. Then we propose a sentiment trading condition to produce buy and sell signals (green). Lastly, we will evaluate the performance by using ROI and Sharpe Ratio.*

Figure 1 shows the pipeline for Sentiment Analysis Case Study. We collect historical prices from Yahoo Finance API  and tweets text by snscrape API. Then we calculate the sentiment category by VADER [[13]](https://ojs.aaai.org/index.php/ICWSM/article/view/14550), a natural language processing tool that combines a lexicon-based approach and grammatical rules to quantify sentiment polarity. We generated buy and sell signals based on two inferences: 1) whether the current price deviates significantly from the average? 2) whether there is a significant positive or negative sentiment? If the price is significantly lower than its EMA and the sentiment is in the positive range, we infer an underestimation of stock value and emotion to drive the market price high soon. Thus, the investor should buy. On the other hand, if the price is significantly higher than its EMA and the sentiment is in the negative range, we infer an overestimation of the stock value and emotion to drive the market price low soon. Thus the investor should sell. We keep other aspects of the case study as consistent with previous ones as possible. 

## Data

We collected historical stock prices and cryptocurrency prices from Yahoo Finance API [[10]](https://pypi.org/project/yfinance/) and Alpha Vantage API [[11]](https://www.alphavantage.co/documentation/) separately. Tweets were obtained from Twitter through Snscrape API [[12]](https://github.com/JustAnotherArchivist/snscrape). Snscrape API outweighs Twitter API in terms of comprehensiveness of queries because Twitter API has an upper limit of 180 queries per 15 minutes. Table 1 shows the sentiment analysis raw variables:

| **Variable Name**  | **Frequency** | **Unit** | 
| :----------------: | :-----------: | :------: |
| Date  | daily  | YYYY-MM-DD |
| Tweets|- | - |
|Stock Price | daily | USD |
|Crypto Price | daily | USD|

*Table 1: Sentiment Analysis: Raw Variables. Data Source: Snscrape API, Yahoo Finance API, Alpha Vantage API. This table shows the raw data that we retrieved from the APIs. The price of stock and crypto asset corresponds to the close price of the given asset at a given date.*

Valence Aware Dictionary and Entiment Reasoner (VADER) is a lexicon-based sentiment analysis tool developed by Hutto and Gilbert [[13]](https://ojs.aaai.org/index.php/ICWSM/article/view/14550). VADER’s lexicon has a rating for each word, illustrating the sentiment polarity (positive/negative) as well as sentiment intensity scaling from -4 to 4. For example, the word “sucks” has a rating of -1.5, while the word “great” has a rating of 3.1. Developers asked people from Amazon Mechanical Turk to manually rate each word. When one applies VADER to rate one sentence, the sentence is split into words, and the words which have been presented in the lexicon are summed up together. “Today is a good day and the weather is nice” has two words, “good” and “great ”, and has ratings of 1.9 and 1.8 respectively. The compound sentiment metric $P_{comp}$ is the sum of all the ratings that have been standardized to a scaling from -1 to 1. We categorized the sentiment based on $P_{comp}$ metric by mean and standard deviation with a multiple of 0.2.

The exponential moving average (EMA) is a technical chart indicator that tracks the price of an investment (like a stock or commodity) over time. The EMA is a type of weighted moving average (WMA) that gives more weighting or importance to recent price data.

Table 2 shows the sentiment analysis calculated variables: 

| **ID**  | **Frequency** | **Unit** | **Description** |
| :----------------: | :-----------: | :------: | --------------------------- |
|$P_{comp}$ | per tweet | - | A normalized compound score that sums every lexicon rating and takes values from -1 to 1 |
|$EMA_{t}$ <br /> (10-day) | daily | USD | Exponential moving average of adjusted closing price, where $EMA_{0} = P_{0}$ and $EMA_{t} = (1-\alpha)EMA_{t-1}+P_{t}, \alpha = 2/(s+1)$. For span $s \geq 1, s:$ decay in terms of span $P_{t}$ : day t closing price |
|Raw Trading Position | daily | USD | $P_t-EMA_{t}$|
|Sentiment Category | daily | Negative, Positive, Neutral | Negative: $P_{comp}<\bar P_{comp}-0.2\sigma_{P_{comp}}$ <br /> Positive: $P_{comp}>\bar P_{comp}+0.2\sigma_{P_{comp}}$ <br /> Neutral: $P_{comp} \geq \bar P_{comp}-0.2\sigma_{P_{comp}}$ or $P_{comp} \leq \bar P_{comp}+0.2\sigma_{P_{comp}}$|
|Trading Positions | daily | - |1 represents buy, and -1 represents sell |

*Table 2: Sentiment Analysis: Calculated Variables. This table shows a detailed description of the calculated variables.*

The initial capital is 100,000 USD. The transaction fee is 0.1\%. We sell the assets when $P_t - EMA_t> \sigma_{P-EMA}$  \& sentiment=negative, and we buy the assets when $P_t-EMA_t<-\sigma_{P-EMA}$ \& sentiment=positive. 

At the beginning of the trading period, there is no transaction if no buy or sell signal exists. At the end of the trading period, we sell all the shares. We make a comparison with the buy and hold strategy (invest all cash on the first trading day, and sell all the shares on the last trading day).

# Result
We choose one typical cryptocurrency, Bitcoin (BTC), to discover whether traders could make use of the sentiment analysis strategies to get a certain amount of profits.

Figure 2 is a visualization of how buy and sell strategy is defined when applying the Sentiment Analysis to perform the backtesting on BTC. The line in pink shows the evolution of the price of BTC for the period retrieved. The line in blue shows the standard deviation of the difference of closing price and exponential moving average. The pink and blue dots represent positive and negative sentiment category, respectively. According to Figure 2, when the difference of adjusted closing price and exponential moving average is larger than its standard deviation, and the sentiment is negative, it would generate a selling signal, represented by a downward red arrow in the graph. When the difference of adjusted closing price and exponential moving average is smaller than its standard deviation, and the sentiment is positive, it would generate a buying signal, represented by an upward green arrow in the graph.


![Buy-and-sell Signal](https://github.com/SciEcon/SRS2021/blob/main/fig/fig3_3_a.png)
*Figure 2: Buy-and-sell Signal: Sentiment Analysis*

Figure 3 shows how portfolio would change in the time series after applying the sentiment analysis strategy to claim to buy or sell the BTC during the backtesting period. We plotted the current amount of cash in red, the value of the holdings in green, and the sum of both cash and holdings in blue (total). The overall trend of total value is increasing in the graph.

![Portfolio Time Series](https://github.com/SciEcon/SRS2021/blob/main/fig/fig3_3_b.png)
*Figure 3: Portfolio Time Series: Sentiment Analysis*

Figure 4 displays a comparison of the ROI when trading BTC using buy-and-hold strategy (in blue) and the sentiment strategy (in pink). The figure depicts that, with sentiment analysis algorithm, the ROI given this backtesting period is 54.57\%, performing twice as much as the simple buy and hold strategy, which produces the result of ROI of 27.00\%. 

![ROI](https://github.com/SciEcon/SRS2021/blob/main/fig/fig3_3_c.png)
*Figure 4: Gross ROI: Sentiment Analysis vs Buy-And-Hold: Sentiment strategy ROI: 54.57\%, Buy & hold strategy ROI: 27.00\%*

Figure 5 displays a comparison of the Sharpe Ratio when trading BTC using buy-and-hold strategy (in blue) and the sentiment strategy (in pink). The figure depicts that, the Sharpe Ratio of the sentiment analysis algorithm reaches 1.24, showing that this strategy has a relatively higher ability to deal with financial risks, compared to the Sharpe Ratio of simple buy and sell strategy, 0.69.

![Sharpe Ratio](https://github.com/SciEcon/SRS2021/blob/main/fig/fig3_3_d.png)
*Figure 5: Sharpe Ratio: Sentiment Analysis vs buy-and-hold: Sentiment strategy Sharpe Ratio: 1.24, Buy & hold strategy Sharpe Ratio: 0.69*

# Discussion
Figures below show the generated buy-and-sell signals using the sentiment analysis strategy, the portfolio evolution, the ROI, and the Sharpe Ratio for Ether (ETH) and Apple (AAPL) stock.

![AAPL Buy-and-sell Signal](https://github.com/SciEcon/SRS2021/blob/main/fig/fig_5_3_a.png)
*Figure 6: AAPL Buy-and-sell Signal: Sentiment Analysis*

![AAPL Portfolio Time Series](https://github.com/SciEcon/SRS2021/blob/main/fig/fig_5_3_b.png)
*Figure 7: AAPL Portfolio Time Series: Sentiment Analysis*

![AAPL Gross ROI](https://github.com/SciEcon/SRS2021/blob/main/fig/fig_5_3_c.png)
*Figure 8: AAPL Gross ROI: Sentiment Analysis vs Buy-And-Hold: Sentiment strategy ROI: 16.32\%, Buy & hold strategy ROI: -3.40\%*

![AAPL Sharpe Ratio](https://github.com/SciEcon/SRS2021/blob/main/fig/fig_5_3_d.png)
*Figure 9: AAPL Sentiment strategy Sharpe Ratio: 1.07, Buy & hold strategy Sharpe Ratio: -0.09*

![ETH Buy-and-sell Signal](https://github.com/SciEcon/SRS2021/blob/main/fig/fig_5_3_e.png)
*Figure 10: ETH Buy-and-sell Signal: Sentiment Analysis*

![ETH Portfolio Time Series](https://github.com/SciEcon/SRS2021/blob/main/fig/fig_5_3_f.png)
*Figure 11: ETH Portfolio Time Series: Sentiment Analysis*

![ETH Gross ROI](https://github.com/SciEcon/SRS2021/blob/main/fig/fig_5_3_g.png)
*Figure 12: ETH Gross ROI: Sentiment Analysis vs Buy-And-Hold: Sentiment strategy ROI: 98.79\%, Buy & hold strategy ROI: 271.25\%*

![ETH Sharpe Ratio](https://github.com/SciEcon/SRS2021/blob/main/fig/fig_5_3_h.png)
*Figure 13: ETH Sentiment strategy Sharpe Ratio: 1.50, Buy & hold strategy Sharpe Ratio: 1.95*
