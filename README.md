# Project Summary
This project aims to utilize NLP techniques to discern the presence of various events within articles. These events encompass Defaults, Mergers and Acquisitions, Revenue discussions, Margin/profitability discussions, and Industry competition. Upon identifying an event, sentiment analysis is conducted accordingly. Notably, an article may encompass multiple events simultaneously. In addition to event identification and sentiment labeling, the project endeavors to distinguish between causal and non-causal events within the articles, as well as to label relevant companies discussed therein. This was our foundational truth. Following this data labeling process using ChatGPT, we employed FinBERT and DistilRoberta models, both fine-tuned on financial news, to detect events and assess their sentiment. Subsequently, the outcomes of both models were integrated into AlphaLens to formulate portfolios for each event. Given the superior performance of the FinBERT model within AlphaLens, our focus shifted towards leveraging its data for portfolio construction.

# Our Approach
## Data Labelling
Initially, the entire dataset was entrusted to ChatGPT for labeling purposes. However, this approach yielded a lack of variability in the labeled data, undermining the reliability of the outcomes. In response, a modified strategy was implemented, wherein ChatGPT was provided with the complete dataset but was directed to identify one event at a time before progressing to the next. Despite this adjustment, ChatGPT's performance remained suboptimal. Subsequently, a few-shot learning approach, which is a method used to make predictions with a limited number of labeling samples, was adopted to enhance ChatGPT's proficiency. After that, the entire dataset was again presented to ChatGPT, this time for the identification of events and their impacts separately. Furthermore, ChatGPT was tasked with discerning between causal and non-causal relationships among the articles, followed by labeling the relevant companies discussed in each article. By segmenting the tasks and providing comprehensive guidance, this methodology notably augmented the variability of data in the identified events, thereby enhancing the overall effectiveness of the process. This was the dataset used for modeling. 

# Models Used
## Finbert
* Finetuned version of bert-base-uncased on the dataset
* The training dataset consists of 4840 sentences from English language financial news categorized by sentiment. 
* The model has an accuracy of over 97% and a loss of .45
* We split the data based on the impact type of the article to get the probability of the sentiment of each article and check the accuracy of each impact type. 

## DistilBert Model Finetuned on Financial news
* Finetuned version of distilroberta-base
* On average DistilRoBERTa is twice as fast as Roberta-base.
* The training dataset consists of 4840 sentences from English language financial news categorized by sentiment. 
* The model Loss of 0.11 and an accuracy of over 98%
* We split the data based on the article to get a better idea of the sentiment and the sentiment probability for each

# Alphalens
## AlphaLens Reloaded Package
The team discovered an updated version of AlphaLens that we could utilize. This version can be found here: https://github.com/stefan-jansen/alphalens-reloaded

## Results 
The tea, focused on using the results from the FinBert model for testing since it provided better results. Alphalens was run on the different events. 
The default events provided the best return, with over 6%.

# Next Steps
Moving forward, the following steps are planned: To begin, we will construct a directed graph incorporating event entities as nodes and causal links as directed edges. The direction of the edge will signify the flow or order of causality between events. We will assign weights to these edges based on the confidence level of the causality, with stronger connections receiving higher weights. Additionally, another directed graph will be constructed where events and companies are depicted as separate nodes, with the impact of events on companies represented by directed edges. Similar to the previous step, weights will be assigned to these edges according to the confidence level of the impact of events. Stronger connections, indicating more substantial impacts, will be assigned higher weights. Furthermore, we will conduct an analysis of graph properties such as connected components to identify self-contained subgraphs of causally linked events. This analysis will provide insights into the interrelatedness and significance of various events within the dataset.

