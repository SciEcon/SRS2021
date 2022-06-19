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

$EMA_{t}^{n} = \frac{2}{n+1} (p_t - EMA_{t}^{n-1}) + EMA_{t}^{n-1} \ t \geq 2$

