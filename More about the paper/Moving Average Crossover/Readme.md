# Appendix

## Additional Assets' performances by Simple Moving Average Crossover Strategies
The figures below show the generated buy-and-sell signals using the Simple Moving Average strategy, the portfolio evolution, the ROI, and the Sharpe Ratio for Bitcoin cryptocurrency (BTC), Apple (AAPL), and Tesla (TSLA) stock.

![Buy-and-Sell Signal: BTC moving average crossover](https://github.com/SciEcon/SRS2021/blob/main/fig/fig_5_1_aa.png)
*Figure 1: Buy-and-Sell Signal: BTC moving average crossover*

![Portfolio time series: BTC moving average crossover](https://github.com/SciEcon/SRS2021/blob/main/fig/fig_5_1_ab.png)
*Figure 2: Portfolio time series: BTC moving average crossover*

![Gross ROI: BTC moving average crossover](https://github.com/SciEcon/SRS2021/blob/main/fig/fig_5_1_ac.png)
*Figure 3: Gross ROI: BTC moving average crossover vs buy-and-hold*

![Sharpe Ratio: BTC moving average crossover](https://github.com/SciEcon/SRS2021/blob/main/fig/fig_5_1_ad.png)
*Figure 4: Sharpe Ratio: BTC moving average crossover vs buy-and-hold*

![Buy-and-Sell Signal: AAPL moving average crossover](https://github.com/SciEcon/SRS2021/blob/main/fig/fig_5_1_ba.png)
*Figure 5: Buy-and-Sell Signal: AAPL moving average crossover*

![Portfolio time series: AAPL moving average crossover](https://github.com/SciEcon/SRS2021/blob/main/fig/fig_5_1_bb.png)
*Figure 6: Portfolio time series: AAPL moving average crossover*

![Gross ROI: AAPL moving average crossover](https://github.com/SciEcon/SRS2021/blob/main/fig/fig_5_1_bc.png)
*Figure 7: Gross ROI: AAPL moving average crossover vs buy-and-hold*

![Sharpe Ratio: AAPL moving average crossover](https://github.com/SciEcon/SRS2021/blob/main/fig/fig_5_1_bd.png)
*Figure 8: Sharpe Ratio: AAPL moving average crossover vs buy-and-hold*

![Buy-and-Sell Signal: TSLA moving average crossover](https://github.com/SciEcon/SRS2021/blob/main/fig/fig_5_1_ca.png)
*Figure 9: Buy-and-Sell Signal: TSLA moving average crossover*

![Portfolio time series: TSLA moving average crossover](https://github.com/SciEcon/SRS2021/blob/main/fig/fig_5_1_cb.png)
*Figure 10: Portfolio time series: TSLA moving average crossover*

![Gross ROI: TSLA moving average crossover](https://github.com/SciEcon/SRS2021/blob/main/fig/fig_5_1_cc.png)
*Figure 11: Gross ROI: TSLA moving average crossover vs buy-and-hold*

![Sharpe Ratio: TSLA moving average crossover](https://github.com/SciEcon/SRS2021/blob/main/fig/fig_5_1_cd.png)
*Figure 12: Sharpe Ratio: TSLA moving average crossover vs buy-and-hold*

## Exponential Moving Average (EMA)

At the same time, some existing literature claims that SMA fails to consider the issue of recency [[1]](https://www.jstor.org/stable/pdf/1913829.pdf) [[2]](https://par.nsf.gov/servlets/purl/10186768). Exponential Moving Average, defined in Equation \ref{eq:3} is an  alternative indicator that puts more weights on recent prices [[3]](https://www.cambridge.org/core/journals/journal-of-applied-probability/article/abs/an-exponential-movingaverage-sequence-and-point-process-ema1/7CFB5DE9313286DAB7C6EF3D40D62129) [[4]](https://ieeexplore.ieee.org/document/6252962). We also take ETH as an exemplified cryptocurrency for analysis.

$EMA_{t}^{n} = \frac{2}{n+1} (p_t - EMA_{t}^{n-1}) + EMA_{t}^{n-1} \quad t \geq 2$

Figure 13 is a visualization of how buy and sell strategy is defined when applying the Exponential Moving Average Strategy to perform the backtesting on ETH. Similar to previous analysis, it is easy to understand that when the Short-window Moving Average (SWMA) crosses above the Long-window Moving Average (LWMA), it would generate a buy signal. On the contrary, it would produce a sell signal. The signal is specifically drawn on the closing price line.

![Buy-and-Sell Signal: exponential moving average crossover](https://github.com/SciEcon/SRS2021/blob/main/fig/fig_3_1_e.png)
*Figure 13: Buy-and-Sell Signal: exponential moving average crossover*

Figure 14 shows how portfolio would change in the time series after applying the exponential moving average crossover strategy to claim to buy or sell the ETH during the backtesting period. From Figure 14, it is obvious to discover that over the two-year backtesting periods, the total revenue is increasing. From Figure 15, ROI given this backtesting period is $856.60\%$, performing much better than the simple buy and hold strategy, which produces the result of ROI $22.55 \%$. From Figure 16, Sharpe Ratio given this backtesting period is $1.00$, showing that this strategy has a relatively higher ability to deal with financial risks, which produces the result of Sharpe Ratio $2.83$.

![Portfolio time series: exponential moving average crossover](https://github.com/SciEcon/SRS2021/blob/main/fig/fig_3_1_f.png)
*Figure 14: Portfolio time series: exponential moving average crossover*

![Gross ROI: exponential moving average crossover vs buy-and-hold](https://github.com/SciEcon/SRS2021/blob/main/fig/fig_3_1_g.png)
*Figure 15: Gross ROI: exponential moving average crossover vs buy-and-hold*

![SSharpe Ratio: exponential moving average crossover vs buy-and-hold](https://github.com/SciEcon/SRS2021/blob/main/fig/fig_3_1_h.png)
*Figure 16: Sharpe Ratio: exponential moving average crossover vs buy-and-hold*

## Simple Moving Average with LSTM

As several machine learning algorithms are developed these days, we find that Recurrent Neural Network (RNN) might be a good training model to compensate for the disadvantages of moving average crossover strategy, for it could distinguish between recent and relatively old data when doing the training. Sang and Massimo (2019) integrate Long-short-term Memory Neural Network (LSTM), a classic modification from Recurrent Neural Network (RNN) in Data Science, with SMA [[5]](https://www.sciencedirect.com/science/article/pii/S2405918818300539). The reason to apply LSTM is that it could update the current state with information in the past and compute the gradient using truncated Backpropagation Through Time (BPTT). There is an advantage of Truncated BPTT over full BPTT when the length of the input sequential data is large as the former is able to effectively prevent gradient vanishing problems.

An LSTM unit involves four gates: Input Gate $i_t$, Output Gate $o_t$, Forget Gate $f_t$, and Stage Update Gate $c_t$, and they are connected in such a way that

$f_t = \sigma_f(W_{fx}x_t + W_{fh}h_{t-1} + B_f)$

$i_t = \sigma_i(W_{ix}x_t + W_{ih}h_{t-1}+b_i)$ 

$o_t = \sigma_o(W_{ox}x_t + W_{oh}h_{t-1}+b_o)$

$c_t = f_{t}c_{t-1} + i_t \text{tanh}(W_{cx}x_t + W_{ch}h_{t-1} + b_c)$

$h_t = o_t \text{tanh}(c_t)$

where $x_t$ refers to Input Tensor, $h_t$ refers to Output Tensor, $W$ refers to Weights, and $b$ refers to Biases functions.

Figure 17 is a visualization of how buy and sell strategy is defined when applying the Moving Average Strategy after getting the predicted prices from the LSTM model to perform the backtesting on ETH. Figure 18 shows how portfolio would change in the time series after applying the crossover strategy to claim to buy or sell the ETH during the backtesting period. From Figure 19, it is obvious to discover that over the two-year backtesting periods, the total revenue is decreasing, and ROI given this backtesting period is $-39.88$\%, performing much better than the simple buy and hold strategy, which produces the result of ROI $0.01$\%. Figure 20 shows that Sharpe Ratio given this backtesting period is $-1.00$, showing that this strategy has a relatively weaker ability to deal with financial risks, which produces the result of Sharpe Ratio $0.36$.

![Buy-and-Sell Signal: BTC moving average crossover](https://github.com/SciEcon/SRS2021/blob/main/fig/fig_5_1_a.png)
*Figure 17: Buy-and-Sell Signal: moving average crossover with LSTM*

![Portfolio time series: BTC moving average crossover](https://github.com/SciEcon/SRS2021/blob/main/fig/fig_5_1_b.png)
*Figure 18: Portfolio time series: moving average crossover with LSTM*

![Gross ROI: BTC moving average crossover](https://github.com/SciEcon/SRS2021/blob/main/fig/fig_5_1_c.png)
*Figure 19: Gross ROI: moving average crossover with LSTM vs buy-and-hold*

![Sharpe Ratio: BTC moving average crossover](https://github.com/SciEcon/SRS2021/blob/main/fig/fig_5_1_d.png)
*Figure 20: Sharpe Ratio: moving average crossover with LSTM vs buy-and-hold*

