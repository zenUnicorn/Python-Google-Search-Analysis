# Python-Google-Search-Analysis
Pytrends API
Pytrends is an unofficial Google Trends API called pytrendsoffers several ways to retrieve information from popular searches from Google Trends. With the aid of the python module, you may speed up the process of automating data retrieval. It is useful to examine and compile a list of the top Google search results for a given topic broken down by geographical location and language.

### Installing pytrends
We must first install this API on our computer before using it.

```python
pip install pytrends
```

### Importing libraries and connecting to Google

Pandas must first be imported in order to generate a dataframe. The function TrendReq from the pytrends.request the library must be imported in order to connect to Google and request the Google trending topics. We will load matplotlib as well, in order to visualize  the data.

```python
import pandas as pd
import matplotlib.pyplot as plt
from pytrends.request import TrendReq
```
### Creating an object out of TrendReq

```python
pytrends = TrendReq(hl='en-US', tz=360)
```
`hl` represents the hosting language for accessing Google Trends, we set it to English. 
`tz` represents timezone, we use the US time zone (represented in minutes), which is 360.

### Building payload
To create a list of terms for Google Trends searches, use the build_payload function from pytrends. Additionally, you may define the category and timeframe for data collection.

```python
keyword_list = ["Data science"] # you can also add a list of keywords
pytrends.build_payload(keyword_list, cat=0, timeframe='today 12-m')
```
### Daily search trends

Let's now look at the top daily search trends globally. The trending_searches() function will be used for this. Simply enter no parameters if you wish to search globally.

```python
# Google Trends data
df = pytrends.trending_searches(pn='nigeria')
df.head(10)
```
### Interest by region

Let's look at some of the most often used regional terms around the globe. 

```python
pytrends.build_payload(kw_list=["Data science"])
df = pytrends.interest_by_region()
df.sort_values(by=["Data science"], ascending=False)
```
Let's check for another term "web development".

```python
pytrends.build_payload(kw_list=['Games'])
df = pytrends.interest_by_region()
df.head(10)
```

### Historical hourly interest

We will use the get_historical_intereset() function to retrieve hourly data for the time period we specify in order to obtain a keyword's hourly interest.

```python
pytrends.get_historical_interest(keyword_list, year_start=2022, 
                                 month_start=5, day_start=1,
                                 hour_start=0, year_end=2022, 
                                 month_end=9, day_end=30,        hour_end=0, cat=0, sleep=0)
```

### Interest over time

```python
pytrends = TrendReq(hl='en-US', tz=360)
pytrends.build_payload(kw_list=['Programming'])
pytrends = pytrends.interest_over_time()
fig, ax = plt.subplots(figsize=(10, 5))
pytrends['Programming'].plot()
plt.style.use('fivethirtyeight')
plt.title('Total Google Searches for Programming', fontweight='bold')
plt.xlabel('Year')
plt.ylabel('Total Count')
plt.show()
```

### Top charts
We can obtain the most popular searches each year using this technique. So let's look at the most popular search terms in 2020.

```python
# Get Top Charts
df = pytrends.top_charts(2020, hl='en-US', tz=300, geo='GLOBAL')
df.head()
```

### Related queries

```python
pytrends.build_payload(kw_list=['Blockchain'])

related_queries = pytrends.related_queries()
related_queries.values()
```

### Keyword Suggestions
Google Trends may provide you with a list of suggested keywords that are related to your primary keyword. 

```python
#Google Keyword Suggestions
keywords = pytrends.suggestions(keyword='Tesla')
df = pd.DataFrame(keywords)
df.drop(columns= 'mid')
 ```
 
 I will update this repository once I publish an article about this project.
 
 Happy coding!
 
 
 
 
 
 
 
 
