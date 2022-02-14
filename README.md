# WebScraping
web scraping project to determine the possible effects social media sentiment has on an NFT collections performance.

This project started in the python program titled "openSea crawling_final (1).ipynb" I used the the openseas api to collect summary statistics 
for the top 30 largest NFT collections in terms of overall cost of each piece in a collection. Some of the statistics include total volume traded, floor price, 
trading volume over the last 30 days, the 30 day percentage price change, and the number of sales over the last 30 days. The output for each collection was in 
json format but was all combined and restructured in excel.

The next step was to extract sentiment data about each NFT collection. I used the snscrape package to collect tweets about each collection in which the tweets
were posted 28-32 days prior to collecting the summary statistics of each NFT collection.I collected about 400 tweets for all 30 NFT collections and stored 
that data in pandas data frames.

After that I used the vader sentiment analyzer package to calculate the sentiment every tweet of each collection. I appended the compound polarity score for 
every tweet in each NFT collections data frame. I then calculated the average compound polarity score for each NFT collection. I also used measurement commonly
used sentiment analysis for stocks which is the bull-bear ratio. I calculated this by counting the number of tweets that had a positive score and the number of 
tweets that had a negative compound polarity score. Any tweet that had a neutral score was omitted for the calculation. The count of postive tweets is the numerator
and the negative tweets was the denominator. I repeated this calculation process for each NFT collections tweets. After getting this 2 statistics I then appended it
to the dataset that had the summary statistics for each collection.

Now that I had a proper dataset to use for analysis I switched over to R to run linear regressions on the data. These linear regressions are shown in the program labeled
"webAnalyticsFinalModelsR.Rmd." You can see that I first ran a regression with the 30 day percentage price change of each NFT collection as the dependent variable
and the average compound polarity score of each NFT collection as the independent variable. The results were statistically insignificant. I then ran another 
linear regression with the 30 day percentage price change as the dependent variable and the bull bear ratio I calculated which I labelled "sentiment_ratio."
These results were also statistically insignificant.

I went back into the python program to further examine the data to try and derive meaningful interpretations of all this data. I used matplotlib to visualize 
the regression line of this data. A couple of outliers seemed to possibly be the cause of these insignifcant results. I used a box and whisker plot to see if
any of the NFT collections fall outside the minimum and maximum inter quartile range and can be deemed statistical outliers. There were a couple of collections
that did fall outside. I then removed these collections from the dataset and re ran the regressions in R.

The outputted results using the same variables for the linear regressions on the data with the outliers removed certainly made the results more accurate with a 
much higher R-squared. But the values of the coeffecients were still statistically insignicant at even a 80% confidence level. I then pivotted to looking at other 
performance measurement indicators that I had collected from Opensea. I choose to look at the possible effects twitter sentiment may have on the trading volume for
an NFT collection over the 30 days upon collection of the statistics as well as the number of sales an NFT collection had over the last 30 days. I ran a regression
using the thirty day volume has the dependent variable and the sentiment ratio as the independent variable. These results proved to be statistically signficant. 
I then ran a regression with thirty day sales as the dependent variable and the average compound polarity score as the independent variable. This model also yielded
statistically significant results.

Further explanation, interpretation, and importance of these results can be found in the "Research Paper" file. 





