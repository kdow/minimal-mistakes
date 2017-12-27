---
title: WeRateDogs Data Wrangling Project
categories:
- python
- data wrangling
date: 2017-12-29
---

## Introduction
This project was part of the data wrangling section of the Udacity Data Analyst Nanodegree program and is primarily focused on wrangling data from the [WeRateDogs](https://twitter.com/dog_rates) Twitter account using Python, documented in a Jupyter Notebook. To view the Notebook and data, please see my [GitHub repository](https://github.com/kdow/WeRateDogs).

The WeRateDogs Twitter account rates dogs with humorous commentary. The rating denominator is usually 10, however, the numerators are usually greater than 10. This aspect was not cleaned as it is part of the humor and popularity of WeRateDogs.

## Project Details
For this project, we only wanted original ratings (no retweets) that have images. Not all of the original tweets in the dataset are dog ratings and some are retweets.

Fully assessing and cleaning the entire dataset would require exceptional effort so only a subset of its issues (eight quality issues and two tidiness issues at minimum) needed to be assessed and cleaned.

The tasks for this project were:
- Data wrangling, which consisted of:
  - Gathering data
  - Assessing data
  - Cleaning data
- Storing, analyzing, and visualizing the wrangled data
- Reporting on my data analyses and visualizations

## The Data
WeRateDogs provided their Twitter archive (which included tweets through August 1, 2017) of basic tweet data (tweet ID, timestamp, text, etc.) for use with this project. The "enhanced" csv file provided by Udacity also contains columns which were extracted programatically: the rating numerator, rating denominator, dog's name, and dog stages (doggo, floofer, pupper, and puppo). These columns needed to be assessed and cleaned as the extraction process wasn't perfect.

The provided Twitter archive lacked some useful information: retweet count and favorite count. I used the tweet IDs to query the Twitter API for each tweet's JSON data using Python's Tweepy library and stored each tweet's entire set of JSON data in a txt file. I then read the txt file line by line into a pandas DataFrame only including the desired variables; retweet count and favorite count.

Udacity also provided a link to image_predictions.tsv which I downloaded programatically using the Requests library.

## Analysis
My analysis revolved around the trend in popularity over time of the account, based off of the number of retweets and favorites, and analysis of the rating scores over time. In my analysis, I recognized a trend in the favorites and retweets over time. This trend increased, presumably as the account became more popular. In the chart below, we see an upward trend for both retweets and favorites. There is a more noticeable increase in the number of favorites when compared to retweets as well as several large outliers in favorites for extremely popular tweets.

<p align="center">
<img src="/assets/images/WeRateDogs/retweets_favorites.png" alt="Retweets and favorites over time" style="width: 85%"/>
</p>

The dog ratings are usually a number out of 10, however, there are a fair amount of ratings that use a scale other than 10. In order to normalize the ratings, I created a ratio of the rating numerator divided by the denominator. When this is plotted, we see a few extreme outliers:

<p align="center">
<img src="/assets/images/WeRateDogs/ratio.png" alt="Rating ratio over time" style="width: 85%"/>
</p>

If we take a look at those two tweets, we can see that the ratings were done for comedic effect:

<p align="center">
<img src="/assets/images/WeRateDogs/tweet1.png" alt="America tweet" style="width: 85%"/>
</p>

<p align="center">
<img src="/assets/images/WeRateDogs/tweet2.png" alt="Snoop Dogg tweet" style="width: 85%"/>
</p>

If we limit our view of the y axis to ignore the outliers and view the bulk of the data, we can get a better idea of the rating ratio trend:

<p align="center">
<img src="/assets/images/WeRateDogs/ratio_zoom.png" alt="Rating ratio over time zoom" style="width: 85%"/>
</p>

In this plot we can see that a few dogs received zero scores, or scores close to zero. We can also see that lower scores are given in general earlier in the dataset. Over time, the scores trended towards higher than a 1:1 ratio with far fewer outliers below 1.
