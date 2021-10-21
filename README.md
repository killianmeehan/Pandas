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

Converted Budget and Gross to float. Left at one decimal place but canchange it two under pandas.options if necessary. Personally I would prefer to leave as an integer as it looks neater and makes more sense. 

Ratings were checked to see the distribution. It would be interesting to see the different standard deviations of each genre separately- intuitively one might expect some genres to have a wider spread of ratings than others.
The default bin value is 10 (i.e. number of samples) so this was increased for more accurate visualisation. In retrospect, another graph type could have been deployed to greater effect.

Next movies with more than 7 in Rating & greater than 50 million Gross were shown. This, as with most questions following, was solved using the .loc method as it is easy to use and quite flexible. Other methods, which work only on the index or on numericals, were noted, e.g. .query.

The next question built on the last, asking for Parental guidance as MPAA Rating also. It was not necessary to use any string methods for this, merely a simple equivalency (==).

For the question, "count of Animation movies with more than 7 in Rating", it was requested to use the count() function. This works but has the undesireable outcome of printing the results of all columns. It was not determined how to prevent this in an elegant fashion. Using len() should be possible.

In-line graphs were generated for several questions out of curiosity. For example, when asked to show the list of top 5 movies based on Budget. A graph in descending order of budget was deemed an effective way of visualing this information. .head() was used as an easy variant for the top 5, instead of the .nlargest(5,'Budget') method.
The in-line graph generator was used instead of matplotlib.

.loc and .nlargest was used for the next questions with multiple filtering requirements as it was very easy to customise. 

The phrasing of one question, "how many Genres are present in the dataframe? (use the function value_counts() which applies to Series, not Dataframe)" restricted the applied methodologies. Converting to a series was trivial, however, the result format using value_counts() breaks down the count by each genre. This solution was provided, with an alternative solution giving the count of unique genres in the dataframe also being provided using the len() and .unique() functions. 

The output using value_counts was used to determine most and least frequent MPAA Ratings. The split was given in ranked percentages which clearly illustrate the highest and lowest frequency occurences. Usin groupby() and .size() would give actual number of occurrences instead of relative frequency.

The penultimate question, most and least expensive Genre, was an interesting challenge.
The suggestion was to take an average of all Budget measures grouped by Genre using the groupBy() method.
This was done, taking advantage of groupby as requested. With only one key, this was not complex. This was not used as the index as it would cause axis issues when trying to sort by budget. .mean() was used on the budget to get the mean budget per genre. .sort_values was used in descending order to show the top budget genres first.

The last question was approached in the same way. However, the result was unsatisfying and merits further thought. "Which Genre is favored the most by the people?" is open to interpretation. As answered, this merely took rating into account. However, weighting should ideally be applied based on the total number of ratings received also. 