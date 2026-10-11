## PRIMARY DATASETS
**ufcstats_data.csv** -
This dataset contains 4,504 rows and 19 columns. These data track athletes career metrics which include their W/L/D, height, weight and stance
which are important factors. The data for each profiles numerical data were all withing strings which is something we must convert into integers
or floats for further exploration.

**ufc_fights.csv** - 
This dataset contains 8,736 rows and 16 columns and the data here documents the results for matches. The data for these match results were sorted
by the dates they took place and those dates were formatted as ("YYYY-MM-DD"). 


## ANOMALIES
There are strings of "NA" in the data which wouldn't show up as NA when looking at the data since it wouldn't be caught if we ran a null_count
this affeects categories such as height, reach and stance. To fix this we must check for "NA's" and then convert them into a proper NA so that 
we can track them with a null_count.
There are also some parts of the data where when given a percentage they include a "%" which would turn these numbers into strings which would cause
issues when we need to sort or average data if needed. Mostly found in "ufcstats_data.csv" which can be fixed with simple stripping of these strings
and then converting them into desired number types.
Another issue is with out dates which in the format of ("YYYY-MM-DD") which wouldn't exactly sort correctly. To fix this we could parse it into
year, month, date and then sort that way to get them into a chronological order.


## DISTRIBUTIONS
**Career Wins** - This data is right-skewed, this could be caused by veterans which create outliers  with some athletes with up to 253 wins while
the median wins is about 11 where the data is centered tightly

**Physical Reach** - This data is symmetric, normally distributed which is centered around 72 inches.

**Takedown Average** - This data is heavily right-skewed, there is a load of 0's which can lead to signs to assumptions that a lot of athletes
avoid offensive wrestling.

**Striking Accuracy** - This data is symmetric, there is high and low groups which make it follow a normal bell curve with the peak being around 
41%.


## Relationships
**Striking vs Grappling** - This scatter plot shows us that the more successful fighters are inclined to strike as the graph is more shifted towards
the right of the graph. Which can be used to infer that pace can dictate ones career longevity.

**Stance vs Career Win Rate** - This box plot shows us that the "Switch" hitters have a higher baseline and tighter IQR that traditional orthodox
fighters, this could be an indication that your stance could affect results.

**Evolution of Decision Finishes** - The time series uses our secondary dataset which allows us to see how overtime the decision matches were judged
which can be used to see what changes occurred to these decisions overtime.


## So What?
**Striking vs Grappling** - Style is important and can be a great indicator of ones career success and career longevity.

**Stance vs Career Win Rate** - Knowing which stance has been more successful can be useful for knowing who would win a fight

**Evolution of Decision Finishes** - Knowing how decision matches are judged overtime can show trends to see what wins fights and how to ensure
a victory if a match goes the full distance.


## What Next?
The next things we can applies to all of the previous plots we looked at so far. The next things we have to do is to look deeper rather than just
looking at all time averages, instead we will look into individual matches and get our own data out of these to make an even better educated guess
on what it takes to win a fight. The way we would do this is by using our dataset "ufc_fights.csv" so that we can see if from match to match how
ones stats could predict a future W/L odds.
