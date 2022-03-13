This folder includes all the data related to pairs trading. The files are divided into two different groups of data, namely preprocessing and trading data.

## Preprocessing data
The file names follow the following format
<code>
"preprocessing_pairs_DATA_CRITERIA.csv"
</code>
  
  Where:
  
  DATA can be from the S&P500 or DigitalCurrencies available in AlphaVantage
  
  CRITERIA can be either sarmento [1] or gatev [2] or neither (in such a case "S&P500-and-" becomes just "S&P500")

## Trading data
The filenames follow the following format 
 <code>"pairs_DATA_SPREAD_CRITERIA_AGG.csv"</code>
  
  Where:
  
  DATA can be from the S&P500 or DigitalCurrencies available in AlphaVantage
  
  SPREAD can be either n-spread (Normal Spread) or s-spread (Simple Spread) as defined in the article
  
  CRITERIA can be either sarmento [1] or gatev [2] or neither (in such a case "S&P-and-" becomes just "S&P")
  
  AGG tells if the information is aggregated or not, if it's aggregated that means the data collected corresponds to the whole portfolio, if it is not included then the data is seggregated by pairs.


## References
  
  [1] Sarmento, S. M., & Horta, N. (2020). Enhancing a Pairs Trading strategy with the application of Machine Learning. Expert Systems with Applications, 158, 113490. https://doi.org/10.1016/j.eswa.2020.113490
  
  [2] Gatev, E., Goetzmann, W. N., & Rouwenhorst, K. G. (2006). Pairs Trading: Performance of a Relative-Value Arbitrage Rule. Review of Financial Studies, 19(3), 797–827. https://doi.org/10.1093/rfs/hhj020
