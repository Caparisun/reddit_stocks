![Picture](https://github.com/Caparisun/reddit_stocks/blob/main/pictures/title.jpg)
# The Correlation of Reddit Users Sentiment and Stock Prices
### Does the sentiment of investors that are active on Reddit influence stock market prices?
A Data Science Case Study

# Contents:
- [Introduction](#Introduction)
- [Method and Approach](#Method-and-Approach)
- [Insights](#Insights)
   - [In-depth analysis of one week](#week-data)
   - [Yearly analysis](#yearly-study)
- [Trading strategy](#Trading-Strategy)
- [Last Words](#Last-words)


## Introduction
This case study was inspired by an event happening in the financial markets in January 2021. The long story can be read here: [click](https://theprint.in/theprint-essential/the-gamestop-story-how-a-group-of-investors-on-reddit-gave-wall-street-a-wild-week/595181/)

In short: A investor called Keith Gill had an interesting observation regarding the shares of the company GameStop Inc. 
He was under the impression, that the stock was more often sold than shares exist in the free market. 
#### You probably wonder how something can be sold more often than it exists? Allow me to explain:
This is possible through a mechanism called short-selling.
Short-selling a stock means, that the selling entity is borrowing the stock and selling it.
The entity hopes for lower prices so that the shares can be bought back for a discount. The difference between the borrowed price and the price where the shares were bought back, is the return or loss of the short seller.

![Picture](https://github.com/Caparisun/reddit_stocks/blob/main/pictures/short_selling.png)

Keith argued, that if lots of people would start buying up the available shares, the short sellers would be forced to buy shares as well to cut their losses. 
He did this mostly via Reddit, a social media platform where people engage with communities via topics rather than their personal network. You can imagine it as a large forum that collects multiple forums in it, and therefore people interested in numerous things are actively exchanging ideas and memes there.
On Reddit, he was posting long articles about the mechanics of how this so-called "Short Squeeze" would be working, and screenshots of his trading positions.
It took over a year, but towards the end of December 2020, people started acting on his advice and bought GameStop share.

Within a timeframe of only 4 weeks, the price for GameStop shares increased twenty-fold. Many people made a life-changing amount of money, but there is also another side to this trade: 
Many people lost a lot of money.
And then there is another third category of people, who believe they missed a once-in-a-lifetime opportunity to get rich quickly.

All these dynamics lead to a tenfold increase of active users on Reddit's most active community for investors and traders - the community has the suiting name 'Wallstreetbets'.
#### These users are, to this day, hunting for the next GameStop and exchanging loads of trading ideas.

But none of these users have asked themselves important questions:
Is there a chance of this happening again, or was this a one-time phenomenon?
Is there actually a correlation between what users talk about and price movements?
Can you actually build a winning trading strategy around the sentiment of Reddit users?

In this case study, I am going to try to answer these questions to the best of my abilities.
I used the following process to get and process the necessary data:

## Method and Approach

#### Week-long in-depth analysis
This part focuses more on individual stocks rather than the overall market sentiment.

I scraped 2.000 comments and posts on each trading day of calendar week 19 2021.
Using natural language processing, I then searched for stock tickers in each post or comment, and if a ticker was mentioned, I calculated the sentiment of the comment. This gives me a number that I can use to score the mood of the users.
I then created a table that shows the frequency of ticker mentions and the average mood for that ticker.
Using Tableau, I tried to spot patterns in the sum of mentions, mood, and price movements.

![Picture](https://github.com/Caparisun/reddit_stocks/blob/main/pictures/_Flussdiagramm%20.jpeg)


#### Three-year overall analysis
This part focuses on the overall market sentiment.
I scraped three years of comment history from the most engaged with, daily appearing post on 'Wallstreetbets', called the daily discussion thread.
Using this data I was able to create a daily overall market sentiment score.
This score was then plotted against an index price and I investigated if there is a relationship that can be used for trading profitably and generate more returns than just investing in a passive index fund.

## Insights

### Week Data
The in-depth study over the course of the week has yielded the following observations:

- Stocks, that have high expected volatility get talked more often about. 
- An often appearing example of this is a companies earnings call, where quarterly revenue and profit numbers are publicly communicated.
- Stocks often surge or decline rapidly after such an earning release.
- In anticipation of these events, Reddit users talk more often about it.
- If a stock declines against the expectations, the sentiment declines as well.
- The correlation seems to be the other way round: Events in financial markets are shaping the topics the users are talking about.

A detailed overview of the daily data can be found in a Tableau story [here](https://public.tableau.com/profile/thamo.koeper#!/vizhome/Scraping_reddit/Story1?publish=yes)

### Yearly Study

The sentiment score calculated was initially very noisy and did not lead to any meaningful insights. I used a Fourier transform to smoothen the score a lot, which allowed me to spot trends in the data.
Below you can see the score before and after transformation.

![Picture](https://github.com/Caparisun/reddit_stocks/blob/main/pictures/smoothing.gif)


There are some seasonal patterns appearing in the sentiment, for example, can the highest sentiment scores be observed towards the end of the year, and a regular drop in sentiment appears over the late summer months.
![Picture](https://github.com/Caparisun/reddit_stocks/blob/main/pictures/sentiment_per_month.png)

The returns of the markets and the sentiment appear to be only correlated when the returns are close to extreme levels, but besides that, there appears no correlation to returns:
![Picture](https://github.com/Caparisun/reddit_stocks/blob/main/pictures/return_setiment.png)

#### The most interesting pattern is the following:
The index price appears to be lagging behind the sentiment of Reddit users a bit. 
This means, that the mood of market participants changes before price does.

![Picture](https://github.com/Caparisun/reddit_stocks/blob/main/pictures/price_sent_pattern.png)

I tried to exploit this with a trading strategy, that I will explain below.


## Trading Strategy

The trading strategy tries to foresee changes in sentiment and enters a buy position if the algorithm notices this.
I achieved this by calculating two rolling averages of the sentiment, one of them is using the mean of the last 5 days, the other one the mean of the last 10 days.
A buying position is entered whenever the faster-moving average crosses the slower-moving average.
The position is being closed when the long-term sentiment average catches up to the fast average. 
100% of the capital is used for every trade, to compound wins quicker.

This strategy is *not* using short selling to leverage a negative change in sentiment.

![Picture](https://github.com/Caparisun/reddit_stocks/blob/main/pictures/sentiment_averages.png)

The algorithm works as followed: 
When the blue line crosses the orange line, the algorithm buys. 
The algorithm sells the position as soon as the blue average touches the orange one.

I tested this strategy backward for the last three years and compared it to just putting money into an index fund.
The algorithm returned fascinating results:

![Picture](https://github.com/Caparisun/reddit_stocks/blob/main/pictures/benchmark_trading_strategy.png)

Over the course of the last three years, 14 trades were made with the algorithm.
14/14 trades were profitable, and over three years the algorithm returned ~80%. A lot more than the index, and also a lot more than the average hedge fund.

## Last words

Short summary:
Reddit does not move the market, it appears that events in the markets are moving reddits emotions.
*But* there seems to be some hidden advantage in the emotions that Reddit users transport via the social media platform.
This advantage can be used to increase one's understanding of current market sentiment and help in anticipating future price movements.
However, the data does not indicate that accurately predicting movements based on the sentiment and frequency of mentions is possible.

Although the algorithm yields impressive results, I personally doubt it will work in a forward-tested environment.
This has to do with the way the sentiment was smoothed, the Fourier transform I used will very likely lead to a so-called ["leakage effect"](https://en.wikipedia.org/wiki/Leakage_effect). The leakage effect will make the Fourier transformed values less accurate. This lack of accuracy increases towards the end of the data. 

Nevertheless, the next step for this project is to connect the data to a simple trading bot and see if the bot can perform in a paper trading environment for a forward test.
