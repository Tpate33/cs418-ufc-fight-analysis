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

**Striking Accuracy vs Win Rate** - This scatter plot compares a fighter's striking accuracy with their overall career win rate. There seems to be a weak positive relationship, where fighters with higher striking accuracy sometimes have higher win rates, but there is still a lot of variation. This means striking accuracy alone does not explain a fighter's success very well.

**Takedown Accuracy vs Win Rate** - This scatter plot compares takedown accuracy with overall career win rate. There does not seem to be a strong relationship between the two variables. Fighters with similar takedown accuracy can have very different win rates, which suggests that takedown accuracy by itself is not a strong indicator of overall success.

**Fighting Style vs Average Win Rate** - This plot uses our secondary dataset `ufc_athletes.csv` joined with `ufcstats_data.csv` by fighter name. We compared the average career win rate across fighting styles. Wrestlers had one of the highest average win rates, but most fighting styles were still fairly close together. We only included styles that had at least 10 fighters so very small groups would not affect the results too much.


## So What?

**Striking Accuracy vs Win Rate** - Striking accuracy may have some relationship with fighter success, but the large amount of variation shows that other factors also play a major role in winning.

**Takedown Accuracy vs Win Rate** - Takedown accuracy alone does not seem to have a strong relationship with win rate. This suggests that just being accurate with takedowns is not enough to explain whether a fighter will be successful.

**Fighting Style vs Average Win Rate** - Fighting style may have some relationship with success because wrestlers had a higher average win rate than several other styles. However, the differences between most styles were not very large, so fighting style alone probably cannot explain fight outcomes.


## What Next?

**Striking Accuracy vs Win Rate** - We could next see whether striking accuracy has a stronger relationship with winning when fighters are separated by weight class or when it is combined with other striking statistics.

**Takedown Accuracy vs Win Rate** - We could compare takedown accuracy with takedown volume or takedown average to see if fighters who attempt and land more takedowns have different results.

**Fighting Style vs Average Win Rate** - We could compare fighting styles within individual weight classes or combine style with striking and grappling statistics to see whether certain styles perform better in certain situations.
