# Project Summary
We aimed to construct a long/short portfolio by leveraging sentiment analysis from various models, including GPT, BERT, and FinBERT. Given the suboptimal accuracy of most models, we opted to use a BERT model fined tuned on financial news. While training these models, we integrated the Yahoo Finance API to gather stock information for our specified tickers. Once sentiment analysis was obtained for the articles, we devised a strategy to buy or sell stocks based on sentiment and its corresponding score. Initially planning to utilize the AlphaLens package for backtesting and portfolio construction. We were able to use the alpha lens reloaded package. 

# Our Approach
## Data collection / PreProcessing
Gave ChatGPT entire dataset for all labeling. This resulted in a lack of variability in the labeled data

Provided ChatGPT with the entire dataset, tasking it to identify one event at a time before proceeding to the next. ChatGPT still fell short of reliability.

Implemented few-shot learning. Gave entire dataset to ChatGPT for event and impact identification separately. Next, tasked to distinguish causal and non-causal relationships among the articles. Finally, had to label relevant companies for each article.
This approach significantly increased the variability of data in the identified events.

# Models Used
## Finbert
* Finetuned version of bert-base-uncased on the dataset
* The training dataset consists of 4840 sentences from English language financial news categorised by sentiment. 
* The model has an accuracy of over 97% and a loss of .45
* We split the data based on the impact type of the article to get the probability of the sentiment of each article and check the accuracy of each impact type. 

## DistilBert Model Finetuned on Financial news
* Finetuned version of distilroberta-base
* On average DistilRoBERTa is twice as fast as Roberta-base.
* The training dataset consists of 4840 sentences from English language financial news categorised by sentiment. 
* The model Loss of 0.11 and an accuracy of over 98%
* We split the data based on the article to get a better idea on the sentiment and the sentiment probability for each

# Alphalens
## AlphaLens Reloaded Package
We found a kept up version of alphalens that we were able to work with. 
## Results 
We focused on the FinBert model for testing since it provided better results and ran alphalens on the different events. 
The default events provided the best return, with over 6%.

# Next Steps
* Construct a directed graph with event entities as nodes and causal links as directed edges, where the edge direction indicates the flow or order of causality. Assign weights to edges based on the confidence of the causal, with stronger connections having higher weights. 
* Construct a directed graph where events and companies are represented as two separate nodes, and the impact of events on companies is depicted as directed edges. Assign weights to the edges based on the confidence of the impact of the events. Stronger connections, indicating more significant impacts, will be assigned higher weights
* Analyze graph properties such as connected components to identify self-contained subgraphs of causally linked events.

