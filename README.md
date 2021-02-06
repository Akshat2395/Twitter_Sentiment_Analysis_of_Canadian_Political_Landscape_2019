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


### 1. Data cleaning and preparation

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

The above bar plot describes the number of reasons which were given to the tweets to be negative. 

<img src="https://github.com/Akshat2395/Data-Scientist-Salary-Prediction/blob/main/images/Gender_distribution_wrt_job_profile.png" alt="Gender of Respondents" width="300" height="300">

We can see that most of the tweets written about the political parties (apart from 'others') were related to scandals made by the politicians followed by the lies they made by promising earlier and not fulfilling it later.
