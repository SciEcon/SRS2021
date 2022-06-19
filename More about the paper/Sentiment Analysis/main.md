# Methodology
## Algorithm

Public mood is another valuable indicator to predict the change in market value of financial assets. Moreover, the advances in computational algorithms, coined Sentiment Analysis or Emotion AI, make public mood quantifiable. Teclock [[1]](https://onlinelibrary.wiley.com/doi/10.1111/j.1540-6261.2007.01232.x) first proposes a newsreader algorithm that utilizes the information in news, tweets, blogs, and surveys to predict stock price. 
Previous research applied a variety of methods in Natural Language Processing (NLP) to quantify sentiments, which significantly improves the prediction of stock prices [[2]](https://www.sciencedirect.com/science/article/pii/S187775031100007X?via%3Dihub) [[3]](https://www.tandfonline.com/doi/full/10.1080/14697688.2012.672762).

A majority of studies have examined Twitter’s predictive power on stock market value such as Dow Jones Industrial Average (DJIA) and S\&P 500 [[2]](https://www.sciencedirect.com/science/article/pii/S187775031100007X?via%3Dihub) [[4]](https://www.researchgate.net/publication/261843641_Stock_Prediction_Using_Event-Based_Sentiment_Analysis) [[5]](https://www.sciencedirect.com/science/article/pii/S1877042811023895) [[6]](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2517025) [[7]](https://econpapers.repec.org/article/eeeintfin/v_3a65_3ay_3a2020_3ai_3ac_3as104244312030072x.htm). These works follow a general event study framework including sentiment analysis with a regression model or a granger causality test. Some also extend to price movement prediction or trading strategy designs through deep learning models [[2]](https://www.sciencedirect.com/science/article/pii/S187775031100007X?via%3Dihub) [[8]](https://www.mdpi.com/1099-4300/21/6/589). The studies differ in sentiment analysis approaches when "computationally" evaluate how positive, negative or neutral a piece of text is. 
One main approach is lexicon-based methods that use labeled lexical features to determine the polarization of the text piece. 
Examples include Valence Aware Dictionary and Entiment Reasoner [[6]](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2517025), Loughran and McDonald financial corpus [[9]](https://onlinelibrary.wiley.com/doi/abs/10.1111/j.1540-6261.2010.01625.x) and Harvard IV-4 psychological corpus. Another approach is supervised learning, which trained the classifiers through existing annotated data to label the tweets. 1-4 days is observed to be the most effective predictive period for Tweets in the financial market [[7]](https://econpapers.repec.org/article/eeeintfin/v_3a65_3ay_3a2020_3ai_3ac_3as104244312030072x.htm).

Existing literature in sentiment analysis intended for price prediction without informing investment strategies. We move forward by incorporating newsreader algorithms to other tech indicators that generate buy and sell signals. 

![Sentiment Analysis: The Algorithm](https://github.com/SciEcon/SRS2021/blob/main/fig/fig2_3.png)
*Figure 1: Sentiment analysis: the algorithm. Following the general pipeline described in Figure 2. The algorithm starts from the left with the inputs (pink), we get our data sources from Yahoo Finance API, Alpha Vantage API, and snscrape API [[10]](https://pypi.org/project/yfinance/) [[11]](https://www.alphavantage.co/documentation/) [[12]](https://github.com/JustAnotherArchivist/snscrape). The raw input variables will be historical closing prices and tweets online comments with specific hashtags. Once the historical data, tweets, and the subset of assets to trade are determined, we perform our analysis (blue) which is the natural language processing [[13]](https://ojs.aaai.org/index.php/ICWSM/article/view/14550) and the exponential moving average calculation. Then we propose a sentiment trading condition to produce buy and sell signals (green). Lastly, we will evaluate the performance by using ROI and Sharpe Ratio.*

Figure 1 shows the pipeline for Sentiment Analysis Case Study. We collect historical prices from Yahoo Finance API  and tweets text by snscrape API. Then we calculate the sentiment category by VADER [[13]](https://ojs.aaai.org/index.php/ICWSM/article/view/14550), a natural language processing tool that combines a lexicon-based approach and grammatical rules to quantify sentiment polarity. We generated buy and sell signals based on two inferences: 1) whether the current price deviates significantly from the average? 2) whether there is a significant positive or negative sentiment? If the price is significantly lower than its EMA and the sentiment is in the positive range, we infer an underestimation of stock value and emotion to drive the market price high soon. Thus, the investor should buy. On the other hand, if the price is significantly higher than its EMA and the sentiment is in the negative range, we infer an overestimation of the stock value and emotion to drive the market price low soon. Thus the investor should sell. We keep other aspects of the case study as consistent with previous ones as possible. 

## Data

We collected historical stock prices and cryptocurrency prices from Yahoo Finance API [[10]](https://pypi.org/project/yfinance/) and Alpha Vantage API [[11]](https://www.alphavantage.co/documentation/) separately. Tweets were obtained from Twitter through Snscrape API [[12]](https://github.com/JustAnotherArchivist/snscrape). Snscrape API outweighs Twitter API in terms of comprehensiveness of queries because Twitter API has an upper limit of 180 queries per 15 minutes. Table 1 shows the sentiment analysis raw variables: 

\begin{table}[ht]
\begin{tabular}{|c|c|c|}
\hline
Variable Name & Frequency & Unit \\ \hline
Date & daily & YYYY-MM-DD \\ \hline
Tweets & - & - \\ \hline
Stock Price & daily & USD \\ \hline
Crypto Price & daily & USD \\ \hline
\end{tabular}
\caption{Sentiment Analysis: Raw Variables\\
Data Source: Snscrape API, Yahoo Finance API, Alpha Vantage API. This table shows the raw data that we retrieved from the APIs. The price of stock and crypto asset corresponds to the close price of the given asset at a given date.}
\end{table}


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
|Sentiment Category | daily | Negative, Positive, Neutral | Negative: $P_{comp}<\bar P_{comp}-0.2\sigma_{P_{comp}}$ <br /> Positive: $P_{comp}>\bar P_{comp}+0.2\sigma_{P_{comp}}$ <br /> Neutral: $P_{comp} \geq \bar P_{comp}-0.2\sigma_{P_{comp}}$ <br /> $P_{comp} \leq \bar P_{comp}+0.2\sigma_{P_{comp}}$|
|Trading Positions | daily | - |1 represents buy, and -1 represents sell |

*Table 2: Sentiment Analysis: Calculated Variables. This table shows a detailed description of the calculated variables.*
