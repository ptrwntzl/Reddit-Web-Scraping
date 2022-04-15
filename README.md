# General Assembly Project 3: Web Scraping, Reddit Front Page

#### Peter Wentzel
---


## Problem Statement


Reddit is one of the most visited websites in the world, especially in the United States.  The message board attracts a wide audience and is therefore of interest for groups and businesses alike to spread information.  Reddit’s front page is populated with posts from sub sections of the message board called subreddits, when a post gets substantial social traction (comments and upvotes), it can make it to the front page for anyone visiting the main message board to see.  FiveThirtyEight is a journalism website that focuses on data and evidence to advance public knowledge.    Regarding their work, they value empirical evidence and transparency of findings so that their readers know that due diligence has been done.  They have expressed interest in how to create a Reddit post that will get high comment engagement from Reddit’s users.  By scraping information from the front page and performing data processing and modeling, the goal of this study is to provide more insight on the attributes of a high engagement post on the front page of Reddit.


## Executive Summary


The data gathered for this project was done via python and the Selenium testing environment.  Data was collected on average twice a day between the days of 23DEC2021 and 06JAN2022, with around ~1000 samples pulled per data gathering execution.  Thread title text, time up, the upvote margin count, the subreddit of the post, and the number of thread comments were the values gathered.  All this information was stored as .csv files and then combined for cleaning prior to analysis.  

While each pull of data contained on average 1000 samples, past a certain point in the data sets the posts were no longer resembling good front page examples.  At a minimum all sets were truncated at the 500th sample (except for one set that did not collect much data due to a collection error).  Between sets there were duplicates of posts due to the nature of the front page, where a high traction post may remain on the front page beyond 12 hours.  This combined with a few posts that were far older than the standard new post window or followed very similar/identical naming conventions (Reddit does love its meme’s), required some cleaning prior to traditional data cleaning.  Interesting caveat, giveaway threads are extremely effective at getting high levels of comment traction due to the nature of the thread (typically requiring a post in response to a question to enter!).  A way to sneak around the ‘promotional’ tagged posts that is also seen on the front page.

Analysis on the data showed that while the data set had a wide variety of data, modeling did not provide a substantial increase above the baseline.  A random forest classifier provided a 66% accuracy to classify a post having above or below the 200-comment count.  The baseline was ~50% when using the cleaned set median.  The subreddit dummy features proved to be the most useful, additional engineered features did not add any significant fidelity to the model.  Natural language processing of the data and data summaries did help provide more insight on successful reddit posts.  Namely, sentiment analysis showed that posts that skew positive or negative do have an increase in mean comment count.  While these were not the desired results, information was gained, and a useful model was built. 


## Recommendations for Future Work 


In-order to increase classification accuracy potentially more specific and new types of data will be needed.  Reddit’s ‘card’ format lends to significant number of videos and pictures being used in posts, some form of image processing (even if just to garner if text is present on the image and reading the text would be very effective or classifying if something is a ‘meme’) would be very effective at providing additional insight.  Since all posts originate from subreddits, and that a small portion of the subreddit’s in the sample list was responsible for almost half of the samples, a natural evolution of the model is to gather more specific subreddit data from high engagement communities to better understand post metrics and content.  Sampling posts more often could provide better information in relation to the time rate of upvotes and comments since the rate at which a post gains initial traction is highly correlated to its overall success.  When duplicates were suppressed in this model, potential post comment and upvote rates were lost, so more advanced preprocessing methods will need to be constructed.


## File Contents

scraper_to_file.ipynb:  This is the web scrapper, used to gather the initial data

Preprocess_data.ipynb:  This is the first cleaning of the data, prepares it for concating with other scraped data

Concat_automation.ipynb:  This program runs to both cut down the datasets but also combine for cleaning, EDA and Modeling

EDA_MODEL.ipynb:  Cleaning, EDA, Modeling Notebook.

Run order is then as follows:    scraper_to_file -> Preprocess_data -> Concat_automation (all the data sets) -> EDA_MODEL

## Data Dictionary


|Feature|Type|Dataset|Description|
|---|---|---|---|
|comment_count|float64|In cleaned .csv files|The thread comment count
|upvote_delta|float64|In cleaned .csv files|The upvote count difference for the thread
|timeup_list|float64|In cleaned .csv files|Time in hours that thread has been up (see intial cleaning for padding)
|subreddit|object|All .csv files|The subreddit associated with the thread
|thread_text|object|All .csv files|The thread title
|comment_count|object|In scrape .csv files|The thread comment count
|upvote_delta|object| scrape .csv files|The upvote count difference for the thread
|timeup_list|object|In scrape .csv files|Time in hours that thread has been up (see intial cleaning for padding)

## References

See cited sources sections in notebooks
