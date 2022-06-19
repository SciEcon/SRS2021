# Methodology
## Algorithm

Public mood is another valuable indicator to predict the change in market value of financial assets. 
Moreover, the advances in computational algorithms, coined Sentiment Analysis or Emotion AI, make public mood quantifiable. 
Teclock \cite{tetlock_2007}first proposes a newsreader algorithm that utilizes the information in news, tweets, blogs, and surveys to predict stock price. 
Previous research applied a variety of methods in Natural Language Processing (NLP) to quantify sentiments, 
which significantly improves the prediction of stock prices \cite{bollen_mao_zeng_2011,luss_d_aspremont_2012}.

A majority of studies have examined Twitter’s predictive power on stock market value 
such as Dow Jones Industrial Average (DJIA) and S\&P 500 \cite{bollen_mao_zeng_2011, makrehchi_shah_liao_2013,zhang_fuehres_gloor_2011,sprenger_sandner_tumasjan_welpe_2014, kraaijeveld_smedt_2020}. 
These works follow a general event study framework including sentiment analysis with a regression model or a granger causality test. 
Some also extend to price movement prediction or trading strategy designs through deep learning models \cite{bollen_mao_zeng_2011,valencia_gomez-espinosa_valdes-aguirre_2019}. 
The studies differ in sentiment analysis approaches when "computationally" evaluate how positive, negative or neutral a piece of text is. 
One main approach is lexicon-based methods that use labeled lexical features to determine the polarization of the text piece. 
Examples include Valence Aware Dictionary and Entiment Reasoner \cite{sprenger_sandner_tumasjan_welpe_2014}, 
Loughran and McDonald financial corpus \cite{loughran_mcdonald_2011} and Harvard IV-4 psychological corpus. Another approach is supervised learning, 
which trained the classifiers through existing annotated data to label the tweets. 
1-4 days is observed to be the most effective predictive period for Tweets in the financial market \cite{kraaijeveld_smedt_2020}.
