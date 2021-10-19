# Pandas

*Learning to use Pandas and working with a data set previously visualised with RapidMiner.*

Completed initial data cleanup.

We can see an interesting result from the duplicate check:

MovieID | Title | MPAA Rating | Budget | Gross | Release Date | Genre | Runtime | Rating | Rating Count
------------ | ------------- | ------------ | ------------- | ------------ | ------------- | ------------ | ------------- | ------------ | -------------
99 | Jurassic Park III | PG-13 | 93000000.0 | 3.688000e+08 | 2001-07-16 | Thriller | 92.0 | 8.9 | 1690474.0
250 | Jurassic Park III | PG-13 | 93000000.0 | 3.687808e+08 | 2001-07-18 | Adventure | 92.0 | 5.9 | 280110.0

Other movies were clearly the result of re-releases (very different dates, run times, budgets, gross etc) but this appears to be referring to the same movie. The minor discrepancy in gross aside, the biggest difference is the rating and rating count. Comparing with IMDb, the 5.9 rating would appear to be more accurate. However, the 8.9 rating is also taken from 6 times more ratings. The difference in [release dates](https://www.imdb.com/title/tt0163025/releaseinfo) shows that the Premiere in the USA was on July 16th, with the general release occurring on July 18th. All other movies in the dataset refer to USA release dates. 

There are 107 rows where the rating (and rating count) are not present. This will be taken into account when performing data analysis. Missing data is contiguous.

One row full of NaNs was identified and removed.

The genres were checked to ensure that there were no spelling inconsisties which would create multiple spurious categories.
Converted Budget and Gross to float. Left at one decimal place but canchange it two under pandas.options if necessary. Personally I would prefer to eave as an integer as it looks neater and makes more sense. 


