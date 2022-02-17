This folder includes all the data related to pairs trading. The files are divided into two different groups of data, namely preprocessing and trading data.

## Preprocessing data
The file names follow the following format
"preprocessing_pairs_S&P500-and-<cryptocurrency name>_<selection criteria>.csv"
  Where:
  cryptocurrency name can be BTC (bitcoin) or ETC (ethereum)
  selection criteria can be either sarmento [1] or gatev [2] or neither (in such a case "S&P500-and-<>" becomes just "S&P500")

## Trading data
The filenames follow the following format
"pairs_S&P-and-<cryptocurrency name>_<spread name>_<selection criteria>.csv"
  Where:
  cryptocurrency name can be BTC (bitcoin) or ETC (ethereum)
  spread name can be either n-spread ($S_{normal}$) or s-spread ($S_{simple}$)
  selection criteria can be either sarmento [1] or gatev [2] or neither (in such a case "S&P500-and-<>" becomes just "S&P500")
  
Normal spread
$$
    S_{\text{normal}} = \sum_{t \in F} \left(\frac{P^A_t}{P^A_0} - \frac{P^B_t}{P^B_0}\right)
$$
  
Simple spread
$$
    S_{\text{simple}} = \sum_{t\in F}\left(P^A_t - P^B_t\right)
$$
