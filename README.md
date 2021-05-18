# The Correlation Between Stock Market Prices And Reddit Investors Sentiment

### Does the sentiment of investors active on reddit influence stock market prices?



# Contents:
- [Introduction](#Introduction)
- [Goals, Method and Approach](#Goals-Method-and-Approach)
- [Insights](#Insights-into-the-data)
   - [Yearly analysis](#Insights-into-the-data)
   - [In-depth analysis of one week](#Insights-into-the-data)
- [Trading strategy](#Model-application)
- [Last Words](#Last-words)
***


## Introduction
This case study was inspired by event happening in the financial markets in january 2021. The long story can be read here: [click](https://theprint.in/theprint-essential/the-gamestop-story-how-a-group-of-investors-on-reddit-gave-wall-street-a-wild-week/595181/)
In short: A investor called Keith Gill had an interesting observation regarding the shares of the company GameStop Inc. 

He was under the impression, that the stock was more often sold than shares exist in the free market. 
##### You probably wonder how something can be sold more often than it exists? Allow me to explain:
This is possible through a mechanism called short-selling.
Short-selling a stock means, that the the selling entity is borrowing the stock and selling it.
The enitity hopes for lower prices, so that the shares can be bought back for a discount. The difference between the borrowed price and the price where the shares where bought back, is the return or loss of the short seller.

![Picture](https://github.com/Caparisun/reddit_stocks/blob/main/pictures/short_selling.png)

Keith argued, that if lot's of people would start buying up the available shares, the short sellers would be forced to buy shares as well to cut their losses. 
He did this mostly via Reddit, a social media platform where people engage with communities via topics rather then their personal network. You can imagine it as a large forum that collects multiple forums in it, and therefore people interested in numerous things are actively exchanging ideas and memes there.
On Reddit he was posting long articles about the mechanics of how this so called "Short Squeeze" would be working, and screenshots of his trading positions.
It took over a year, but towards the end of December 2020, people started acting on his advice and bought GameStop share.

Within a timeframe of only 4 weeks, the price for GameStop shares increased twenty-fold. Many people made a life-changing amount of money, but there is also another side to this trade: 
Many people lost a lot of money.
And then there is another third category of people, who believe they missed a once-in-a-lifetime opportunity to get rich quickly.

All these dynamics lead to an tenfold increase of active user on Reddit's most active community for investors and traders - the community has the suiting name 'Wallstreetbets'.
#### These users are, to this day, hunting for the next GameStop and exchanging loads of trading ideas.

But none of these users have asked themselves important questions:
Is there a change of this happening again, or was this a one time phenomenon?
Is there actually a correlation between what user talk about and price movements?
Can you actually build a winning trading strategy around the sentiment of Reddit users?

In this casestudy, I am going to try to answer these question to the best of my abilities.
I used the following process to get and process the necessary data:

## Goals, Method and Approach

### Weekly in-depth analysis
I scraped 2.000 comments and posts on each trading day of calendar week 19 2021.
Using natural language processing, I then searched for stock tickers in each post or comment, and if a ticker was mentioned, I calculated the sentiment of the comment. This gives me a number that I can use to score the mood of the users.
I then created a table that shows the frequency of a tickers mentions and the average mood for that ticker.
Using Tableau, i tried to spot patterns in the sum of mentions, mood and price movements.

![Picture](https://github.com/Caparisun/reddit_stocks/blob/main/pictures/_Flussdiagramm.jpeg)






