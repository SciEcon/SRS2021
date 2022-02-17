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
  
  spread name can be either n-spread (Normal Spread) or s-spread (Simple Spread) as defined in the article
  
  selection criteria can be either sarmento [1] or gatev [2] or neither (in such a case "S&P500-and-<>" becomes just "S&P500")
