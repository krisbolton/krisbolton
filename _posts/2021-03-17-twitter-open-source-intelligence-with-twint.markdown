---
layout: post
title: Twitter Open Source Intelligence with TWINT
description: TWINT provides a termainal or code interface to Twitter in which you can search tweets, replies and more over specific time periods and easily export the intelligence...
date:   2021-03-19 19:41:00 +0000
tags:   [OSINT, TWINT]
---

<style>p { text-align: justify; }</style>

<a href="https://github.com/twintproject/twint" target="_blank">TWINT</a>, short for Twitter Intelligence, is an open source Twitter OSINT tool writtein in Python, created by Franesco Poldi. TWINT provides a termainal or code interface to Twitter in which you can search tweets, replies, favourites, followers, following, retweets and more over specific time periods and easily export the intelligence to CSV, JSON and an ElasticSearch-based intergration.

In this post we'll work through a basic workflow in a <a href="https://jupyter.org/" target="_blank">Jupyter Notebook</a> using TWINT and <a href="https://pandas.pydata.org/" target="_blank">Pandas</a>, a python data science library.

## Setup

If you have never used any of the technologies I mentioned, start here. If you already have Jupyter Notebooks skip to  step.

**Step 0**: Download and install <a href="https://www.anaconda.com/products/individual#Downloads/" target="_blank">Anaconda. Anaconda is a data science platform which includes Jupyter Notebooks. Installers are availalbe for Windows, MacOS and Linux. `pip3 install jupyter` is a fast terminal-based method for Mac and Linux.  
**Step 1**: Install TWINT.`pip3 install twint` for Mac and Linux is possible, however, installing in-notebook provides a more consistent approach for using TWINT with Jupyter across Windows, Mac and Linux. 
    
However, feel free to `pip3 install twint` install via terminal on Mac or Linux so you can use the `twint` command in-terminal, as well as in-notebook. If you do this, it isn't necessary to type the following part of this step.
    
In the first cell of a notebook, type:
    
```python
import sys
!{sys.executable} -m pip install twint
```

**Step 2**: We need to import twint and pandas for use in the notebook. The code below this allows us to use multiple cells, rather than wait for cells to finish. You will still need to wait for cells which depend on previous cells of course.


```python
import twint
import pandas as pd

# Allows the running of multiple event loops in Jupyter Notebooks.
# Fixes: "RuntimeError: This event loop is already running"
import nest_asyncio

nest_asyncio.apply()
```

## Basic TWINT Usage

Now that we're all set up, we can gather some Twitter intelligence.

There are two ways to use TWINT, in the terminal and within python code. We will not be discussing the use of TWINT via the terminal, only its use within python scripts.

The simplest usable TWINT script used to scrape tweets from a users timeline is as follows:

```python
c = twint.Config()

c.Username = 'jack'
c.Limit = 10

twint.run.Search(c)
```

We utlise the TWINT `Config()` method, which allows us to use various functions such as `Username`, `Limit` and many others. The `Limit` function allows us to limit the number of tweets returned. The output will be the tweet ID, datetime, username and tweet.

If you have issues at this stage, for example the error `CRITICAL:root:twint.run:Twint:Feed:noDataExpecting value [...]`, try uninstalling twint `pip3 uninstall twint` and reinstall with via the following: `pip3 install --user --upgrade git+https://github.com/twintproject/twint.git@origin/master#egg=twint`.

## A Useful Workflow

The above is the essance of TWINT, returning Twitter information directly (either in-terminal or in-notebook). This isn't particulalry useful or readable at the moment. Pandas can change that!

```python
c = twint.Config()

c.Username = 'jack'
c.Since = '2021-02-01 00:00:00'
c.Until = '2021-03-17 00:00:00'
c.Pandas = True

twint.run.Search(c)
```

Above, we target tweets by user `jack` (the founder of Twitter) from Febuary 17st 2021 to the date of this post, March 17th 2021 and utilise the Pandas module of TWINT (pandas is a seperate data science library, this is just a flag to store in data so we can use the functions ahead).

You can also use pandas on any CSV files we have created using TWINT by importing the data into a <a href="https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html" target="_blank">dataframe</a>.

```python
df = twint.storage.panda.Tweeds_df
df
```

Here, we assign the data we collected and stored previously to a dataframe and print the contents. A dataframe is a two dimensional data structure with coloumns and rows, like a table. This allows us to tabulate data, making it much more readable.

This allows us to manipulate the data by focusing on indivudal columns and allows grouping etc. For example, we are dealing with one user so there's no need to see that information, and much of the other information is verbose. We may only care about the tweet content, and the datetime.

```python
df[['date', 'tweet']]
```

We have access to a great deal of tweet information. We can view information on what the dataframe contains with the `info()` function.

```python
df.info()
```

```text

<class 'pandas.core.frame.DataFrame'>
RangeIndex: 12 entries, 0 to 11
Data columns (total 33 columns):
 #   Column           Non-Null Count  Dtype 
---  ------           --------------  ----- 
 0   id               12 non-null     object
 1   conversation_id  12 non-null     object
 2   created_at       12 non-null     int64 
 3   date             12 non-null     object
 4   timezone         12 non-null     object
 5   place            12 non-null     object
 6   tweet            12 non-null     object
 7   hashtags         12 non-null     object
 8   cashtags         12 non-null     object
 9   user_id          12 non-null     int64 
 10  user_id_str      12 non-null     object
 11  username         12 non-null     object
 12  name             12 non-null     object
 13  day              12 non-null     int64 
 14  hour             12 non-null     object
 15  link             12 non-null     object
 16  retweet          12 non-null     bool  
 17  nlikes           12 non-null     int64 
 18  nreplies         12 non-null     int64 
 19  nretweets        12 non-null     int64 
 20  quote_url        12 non-null     object
 21  search           12 non-null     object
 22  near             12 non-null     object
 23  geo              12 non-null     object
 24  source           12 non-null     object
 25  user_rt_id       12 non-null     object
 26  user_rt          12 non-null     object
 27  retweet_id       12 non-null     object
 28  reply_to         12 non-null     object
 29  retweet_date     12 non-null     object
 30  translate        12 non-null     object
 31  trans_src        12 non-null     object
 32  trans_dest       12 non-null     object
dtypes: bool(1), int64(6), object(26)
memory usage: 3.1+ KB
```

We can manipulate any of these columns as we did above.

## Visualisations for Understanding

We can visualise the data we have gathered to gain a better understanding. We'll re-gather a larger dataset from jacks timeline so we have more data to deal wrangle insights from. 


```python
c = twint.Config()

c.Username = 'jack'
c.Since = '2021-01-01 00:00:00'
c.Until = '2021-03-17 00:00:00'
c.Pandas = True

twint.run.Search(c)
```

We have increased our search space by 1 month.

```python
df = twint.storage.panda.Tweeds_df
df
```

We reassign the collected tweets to the dataframe, as we have new data (we increased teh search space above).

We want to graph the number of tweets over the period using matplotlib.

```python
# Convert date colum into a list for the next step
dates_list = df['date'].to_list()
```

We convert the dataframes data column to a python list and assign it to the variable `data_list`.

```python
# Create a histogram of tweet frequency
# from https://stackoverflow.com/questions/44929555/how-to-properly-create-a-histogram-displaying-the-frequency-of-the-tweets-for-e

dates = []
for t in dates_list:
    # extract the date part of the datetime
    date_str = t.split(' ')[0]
    # extract the time from the date
    year,month,day = [int(i) for i in date_str.split('-')]
    # create a date object
    d = date(year, month, day)
    # sort
    dates.append(d)
    
# sort dates
dates.sort()

# find the first and last date
min_date = dates[0]
max_date = dates[-1]

# compute num days
length = (max_date - min_date).days + 1

# plot histogram
plt.figure(figsize=(12,8))
plt.hist(dates)
plt.show()
```

Above we create a histogram of tweets over the period, the tweet frequency. For the data we gathered on jack this produces the following:

<div style="text-align:center;"><img src="/images/posts/2021/jack-tweet-frequency.jpg" alt="A histogram showing the freqnecy of tweets by jack over a 2 and a half month period." style="width:350px; padding-bottom: 10px;"/></div>

<p style="text-align: center; font-style: italic;">A histogram showing the freqnecy of tweets by jack.</p>

## Extract Unique Hashtags

We want to find the individual hashtags a user has used during the collection period.

```python
# Extract unique hashtags
# Get hashtag list
hashtag_list = df['hashtags'].to_list()

# Remove empty elements
filtered_list = list(filter(None, hashtag_list))

# Find unique entries (will be slow with *very* large lists)
unique_hashtags = []
for value in filtered_list:
    if value not in unique_hashtags:
        unique_hashtags.append(value)

# In this case, we only have one unique hashtag
print(unique_hashtags)
```

Above we create a list containing the hashtags from the associated column in the data. We filter out empty entires, there will be many of these unless a user is a prolific hashtag user on every tweet. Finally, we loop through each entry to find unique hashtags to remove duplicates. We end printing this unique hashtag list.

In this case there is only one output, "#bitcoin".

## Word Cloud

We want to create a word cloud to visualise the possible topics a user is discussing during the captured period. The word cloud package serves this purpose.

```python
tweets = df['tweet'].to_list()

words = ''
stopwords = set(STOPWORDS)

# Iterate through tweets
for value in tweets:
    # Convert to string
    value = str(value)
    # Tokenize
    tokens = value.split()
    # Convert each to lowercase
    for i in range(len(tokens)):
        tokens[i] = tokens[i].lower()
        
    # Add to word
    words += " ".join(tokens)+" "

# Word cloud setup
wordcloud = WordCloud(width = 800, height = 800,
                     background_color = 'white',
                     stopwords = stopwords,
                     min_font_size = 10).generate(words)

# Plot
plt.figure(figsize=(8,8))
plt.imshow(wordcloud)
plt.axis("off")
plt.show()
```

Above, we create a list of the tweets from the associated column. We iterate through each tweet, turning the values to strings, tokenizing these strings and converting them to lowercase. Once each word has been cleansed in this way, they are added to the words variable which will be used to generate a word cloud using the `WordCloud()` function. Finally, we plot the word cloud using matplotlib.

<div style="text-align:center;"><img src="/images/posts/2021/jack-tweets-word-cloud.jpg" alt="A word cloud composed of tweets from jack during Feb - Mar 2021.." style="width:350px; padding-bottom: 10px;"/></div>

<p style="text-align: center; font-style: italic;">A word cloud composed of tweets from jack during Feb - Mar 2021.</p>

## Further Analysis and Improvements

This is only a small set of what is possible with Python, pandas, matplotlib and TWINT of course. There are also a number of things we can do to improve on what we have done here. For example, the word cloud does not remove hyperlinks or emojis, on large datasets this unnecessary analysis would add up.

## References

<ol>    

<li>Matplotlib (2021) <i>Matplotlib</i><a href="https://matplotlib.org/" target="_blank">https://matplotlib.org</a>.</li>

<li>Pandas (2021) <i>Pandas</i><a href="https://pandas.pydata.org/" target="_blank">https://pandas.pydata.org</a>.</li>

<li>Pandas (2021) <i>Pandas.DataFrame</i><a href="https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html" target="_blank">https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html</a>.</li>

<li>Twitter (2021) <i>Profile: Jack</i><a href="https://twitter.com/jack" target="_blank">https://twitter.com/jack</a>.</li>

<li>Wikipedia (2021) <i>Jack Dorsey</i><a href="https://en.wikipedia.org/wiki/Jack_Dorsey" target="_blank">https://en.wikipedia.org/wiki/Jack_Dorsey</a>.</li>

<li>Wordcloud (2021) <i>WordCloud for Python documentation</i><a href="https://amueller.github.io/word_cloud/" target="_blank">https://amueller.github.io/word_cloud/</a>.</li>

</ol>