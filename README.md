# Twitter_Sentiment_Analysis_of_Canadian_Political_Landscape_2019

The goal is to essentially use sentiment analysis on Twitter data to get insight into the 2019 Canadian elections.


## Introduction
Sentiment analysis is a technology of increasing importance in the modern society as it allows individuals and organizations to detect trends in public opinion by analyzing social media content. Keeping abreast of socio-political developments is especially important during periods of policy shifts such as election years, when both electoral candidates and companies can benefit from sentiment analysis by making appropriate changes to their campaigning and business strategies respectively.

**This project answers the question "WHAT PUBLIC OPINION ON TWITTER TELL US ABOUT THE CANADIAN POLITICAL LANDSCAPE IN 2019?**

## Outline of this project
1. Data Cleaning
2. Exploratory Data Analysis
3. Model Preparation
4. Model Implementation
5. Results


The Sentiment.csv file contains 130K+ labeled generic tweet texts. It had their sentiments already analyzed and recorded as: positive or negative. Each line is a single tweet, which may contain multiple sentences despite their brevity. The fields of each line are:

1. sentiment can be “positive” or “negative”
2. text the text of the tweet

The second data set, Canadian_elections_2019.csv, contains a list of tweets regarding the 2019 Canadian elections. The fields of each line are:

1. sentiment can be “positive” or “negative”
2. negative_reason reason for negative tweets. Left blank for positive tweets.
3. text the text of the tweet
Both datasets have been collected directly from the web.


### 1. Data Cleaning and Preparation

The steps taken to perform data cleaning are- 
1. All text in lowercase
2. Filter out all stopwords
3. Stemming the words
4. Removal of URL links and twitter handles
5. Removal of special characters

**Tokenizing** - tokenizing involves splitting sentences and words from the body of the text.

**Stop Words** - A stop word is a commonly used word (such as “the”, “a”, “an”, “in”). We would not want these words taking up space in our database, or taking up valuable processing time.

**Stemming**- It is the process of reducing words to their core root.

**Searching for individual political party related information and assigning names of the party to which the tweet refers.**

We will look for certain keywords in a tweet to classify the tweet with a political party.

1. Liberal : Keywords - 'justin|trudeau|justintrudeau|liberal|lpc'
2. Conservative : Keywords - 'andrew|scheer|andrewscheer|conservative|cpc'
3. NDP : Keywords - 'thejagmeetsingh|ndp|jagmeet|singh|democratic'
4. Mixed: If all or any two of the parties are mentioned
5. None: If neither of the keywords are present


### 2. Exploratory Data Analysis

* The following bar plot describes the number of reasons which were given to the tweets to be negative. 

<img src="https://github.com/Akshat2395/Twitter_Sentiment_Analysis_of_Canadian_Political_Landscape_2019/blob/main/images/neg_reason_count.png" width="1000" height="300">

We can see that most of the tweets written about the political parties (apart from 'others') were related to scandals made by the politicians followed by the lies they made by promising earlier and not fulfilling it later.


* Distribution of the political affiliations of the tweets

<img src="https://github.com/Akshat2395/Twitter_Sentiment_Analysis_of_Canadian_Political_Landscape_2019/blob/main/images/distribution_political_affiliations.png" width="1000" height="300">

From the above distribution of tweets, we can see that most of the tweets were related to the Conservative party followed by the Liberals. The maximum number of tweets were related to the elections but did not affiliate any of the political party. NDP had the least number of tweets which means that people were least interested with them.


* Distribution of negative and positive tweets about each political party

<img src="https://github.com/Akshat2395/Twitter_Sentiment_Analysis_of_Canadian_Political_Landscape_2019/blob/main/images/ditribution_neg_pos_political_parties.png" width="900" height="300">

The above pie chart describes the distribution of positive and negative tweets about each political party they represent. From the first pie chart, the conservatives had to bear the most as they received the maximum number of negative tweets followed by the Liberals. On the other hand, the Liberals and Conservatives were also favoured the most as they both received almost the same number of positive tweets.


### 3. Model Preparation

As ML models cannot understand english words, the inputs should be converted to a set of numbers which represent those english words/sentences. 
To do so, here we used TF and TF-IDF.
1. **TF (Term Frequency)** - 
Term frequency is the number of times a particular word appears in a document. Since every document is different in length, it is possible that a term would appear more often in longer documents than shorter ones. Thus, term frequency is often divided by the total number of terms in the document as a way of normalization.

2. **TF-IDF** - 
Tf-idf stands for term frequency-inverse document frequency, and the tf-idf weight is a statistical measure used to evaluate how important a word is to a document in a collection or corpus. The importance increases proportionally to the number of times a word appears in the document but is offset by the frequency of the word in the corpus.

3. **Word Embeddings** - 
A word embedding is a learned representation for text where words that have the same meaning have a similar representation. Word embeddings are in fact a class of techniques where individual words are represented as real-valued vectors in a predefined vector space. Each word is mapped to one vector and the vector values are learned in a way that resembles a neural network, and hence the technique is often lumped into the field of deep learning.

Word vectors are positioned in the vector space such that words that share common contexts in the corpus are located in close proximity to one another in the space.

4. **N-grams** - 
An N-gram model predicts the occurrence of a word based on the occurrence of its N – 1 previous words. It can also be defined as a contiguous sequence of N items from a given sample of text or speech. Here an item can be a character, a word or a sentence and N can be any integer. When N is 2, we call the sequence a bigram. Similarly, a sequence of 3 items is called a trigram, and so on.

### 4. Model Implementation

In this section, I have implemented various ML models to classify tweets. Hyperparameter tuning was also conducted using GridSearchCV. The models implemented and their performance is shown below.

<img src="https://github.com/Akshat2395/Twitter_Sentiment_Analysis_of_Canadian_Political_Landscape_2019/blob/main/images/accuracy_algorithms.png" alt="Gender of Respondents" width="700" height="400">

From the above bar chart, we can see that the Logistic regression and SVC model have the highest accuracy on the test set for both word frequency (TF) and TF-IDF as features. Hence I went with the features provided by TF-IDF and implement Logistic regression on the Canadian Elections data set.

Moreover, the reasons of the tweets to be negative were grouped together to predict their sentiments.

### 5. Result

* **How each party is viewed in the public eye based on the sentiment value?**

<img src="https://github.com/Akshat2395/Twitter_Sentiment_Analysis_of_Canadian_Political_Landscape_2019/blob/main/images/distribution_neg_tweets.png" alt="Gender of Respondents" width="900" height="400">

This is substantiated from the above graph that most of the negative tweets of the Conservative party are categorized as 'Scandal' and 'Tell Lies' whereas most of the negative tweets for the rest of the parties are in 'Others' category.

This shows that the public associated the Conservative party with deceit, scandalous and lies in their tweets. The same can be said for Liberal party but it is not to the same extent as that of the Conservative party.


* **Provide a few reasons why your model may fail to predict the correct negative reasons.**

Count of grouped reasons - 

Climate Problem     41
Economy             63
Healthcare          54
Manipulative       214
Others             364
Scandalous         270

It can be inferred that the count of reasons is disproportionate. Half of the reasons have very less samples as compared to the rest. Hence the data is skewed which means our model has very few tweets of 'Climate Problem', 'Economy' and 'Healthcare' to model on. Therefore, as we got few samples per class to build our model, we obtain a low accuracy in our model.

* There is no improvement in accuracies from word embeddings except for Decision Trees where we see an improvement in accuracy of around 6%.

* Using Uni and Tri-grams (ngram_range=(1,3)), we observed that the accuracies of all the models have increased by a significant amount.
