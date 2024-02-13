# Coronavirus Twitter Analysis

## Background

**Data**

Approximately 500 million tweets are sent everyday.
Of those tweets, about 2% are *geotagged*.
Only *geotagged* tweets are included in the dataset.
We will be using the dataset in the lambda server's `/data/Twitter dataset` folder which contains all geotagged 
tweets (1.1 billion tweets) that were sent in 2020. Each tweet is stored in a zip file for each day, with each zip file 
consisting of 24 text files, one for each hour of the day. Each text file hold tweets stored in JSON format.

We plan to use [MapReduce](https://en.wikipedia.org/wiki/MapReduce) to process these tweets to use to produce graph to visualie 
the frequency of certain languages, countries, and hashtags found in tweets.

## File Summaries 

The main files used in this project were `map.py`, `reduce.py`, `visualie.py`, and `alternative_reduce.py`

The `map.py` file processes the zip file for an indivual day and groups tweets by the usage of hashtags within languages and countries.
A zip file is created for each day and language and country with the tweets the contains the specified hashtag.

`reduce.py` groups the outputs from `map.py` and creates a file holding all the tweets by language, and a seperate file holding all the tweets by countries.

`visualie.py` creates a bar chart the visualies the frequency of a specified hashtag to the countries/languages. Where the countries/languages are on the x-axis, and the frequency of the hashtag is on the y axis.

`alternative_reduce.py` follows a structure similar to a combined version of `reduce.py` and `visualie.py`. This file will scan through all the data in the outputs folder created by `map.py` and will create a dataset to plot the frequency of multiple inputted hashtags along the year 2020 in a line char.

## Plots
### Plots made with <code>visualize.py</code>

We generate the following plots by running the following command:
```
$  ./src/visualize.py --input_path=<reduced.(lang/country)> --key='<hashtag>'
```

Ex. To plot the graph below we would run the following: 
```
$  ./src/visualize.py --input_path=reduced.lang --key='#coronavirus'
```

**Frequency of #coronavirus by language in 2020**
![language_coronavirus](https://github.com/JTan242/twitter_coronavirus/assets/132401824/ebfbd6eb-b5c7-475e-b930-56c046362fee)

**Frequency of #coronavirus by country in 2020**
![country_coronavirus](https://github.com/JTan242/twitter_coronavirus/assets/132401824/f3f192e6-3a51-4fde-b32b-793f86748758)

**Frequency of #코로나바이러스 by language in 2020**
![language_korean](https://github.com/JTan242/twitter_coronavirus/assets/132401824/da5d545f-ae36-4c0a-84d2-64ced73dd83d)

**Frequency of #코로나바이러스 by country in 2020**
![country_korean](https://github.com/JTan242/twitter_coronavirus/assets/132401824/f200911f-1760-41a8-9410-510c99c1e7e8)

### Plot made with <code>alternative_reduce.py</code>

To generate the line chart we run the following. Note that each hashtag is enclosed by a single quote and seperated by commas.
```
$  ./src/alternative_reduce.py --hashtags=" '<hashtag>', '<hashtag>', '<hashtag>', '<hashtag>'"
```
To produce the line chart below we can run the following command.
```
$  ./src/alternative_reduce.py --hashtags=" '#covid-19', '#coronavirus', '#corona', #virus', '#flu', '#sick', '#cough', '#sneeze', '#hospital', '#nurse'"
```
**Frequency of hashtags used in 2020**
![alternative_reduce_plot](https://github.com/JTan242/twitter_coronavirus/assets/132401824/f089cd9c-deba-4925-b2f3-8007a8fdfc76)

