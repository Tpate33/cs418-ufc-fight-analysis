## PRIMARY DATASETS

**ufcstats_data.csv** - This dataset contains 4,504 rows and 19 columns. These data track athletes career metrics which include their W/L/D, height weight and stance which are important factors. The data for each profiles numerical data were all within strings which is something we must convert into integers or floats for further exploration. We also derived a `win_rate` column (wins / (wins + losses + draws) x 100) since the source file only has raw W/L/D counts.

**ufc_fights.csv** - This dataset contains 8,736 rows and 16 columns and the data here documents the results for matches. The data for these match results were sorted by the dates they took place and those dates were formatted as ("YYYY-MM-DD").

## SECONDARY DATASET USED IN EDA

**ufc_athletes.csv** - This dataset contains 3,145 rows and 43 columns and is the only one of our files with a `fighting_style` field, so it is joined to `ufcstats_data.csv` on fighter name to analyze style. The join matched 2,924 of 4,504 fighters (65%); the unmatched 35% are cases where ufcstats.com and ufc.com spell or format the same fighter's name differently. We kept the exact-match join rather than fuzzy matching to avoid incorrectly pairing different fighters, and we report the style results as applying to that 65% subset.

## ANOMALIES

There are strings of "NA" in the data which wouldn't show up as NA when looking at the data since it wouldn't be caught if we ran a null_count. This affects categories such as height, reach and stance. To fix this we must check for "NA's" and then convert them into a proper NA so that we can track them with a null_count.

There are also some parts of the data where when given a percentage they include a "%" which would turn these numbers into strings which would cause issues when we need to sort or average data if needed. Mostly found in "ufcstats_data.csv" which can be fixed with simple stripping of these strings and then converting them into desired number types.

Another issue is with our dates which are in the format of ("YYYY-MM-DD") which wouldn't exactly sort correctly as text. To fix this we parse out the year and use that to group fights chronologically.

The `fighting_style` column in `ufc_athletes.csv` is free-text scraped from UFC profile pages, so the same discipline appears under several labels ("Wrestler" vs "Wrestling", "Boxer" vs "Boxing", "Brazilian Jiu-Jitsu" vs "Jiu-Jitsu"). This is a problem with the source data, not with our parsing. Left alone it produces a bar chart where near-identical styles sit at slightly different heights, which invites over-reading a difference that is just label noise. We therefore collapse the 19 raw labels into 12 families before analyzing.

## DISTRIBUTIONS

**Career Wins** - This data is right-skewed, this could be caused by veterans which create outliers with some athletes with up to 253 wins while the median wins is about 11 where the data is centered tightly.

**Physical Reach** - This data is symmetric, normally distributed which is centered around 72 inches. Note that reach is the sparsest physical field, so this distribution reflects only the fighters whose profiles list it.

**Takedown Average** - This data is heavily right-skewed, there is a load of 0's. Some of these zeros are genuine (fighters who never shoot), but because the column has zero nulls, some are likely the scraper writing 0 where a profile had no data. We flag this rather than claiming strikers avoid wrestling.

**Striking Accuracy** - This data is symmetric, there is high and low groups which make it follow a normal bell curve with the peak being around 41%.


## Relationships

**Striking Accuracy vs Win Rate** - This scatter plot compares a fighter's striking accuracy with their overall career win rate. There seems to be a weak positive relationship, where fighters with higher striking accuracy sometimes have higher win rates, but there is still a lot of variation. This means striking accuracy alone does not explain a fighter's success very well.

**Takedown Accuracy vs Win Rate** - This scatter plot compares takedown accuracy with overall career win rate. There does not seem to be a strong relationship between the two variables. Fighters with similar takedown accuracy can have very different win rates, which suggests that takedown accuracy by itself is not a strong indicator of overall success.

**Fighting Style vs Average Win Rate** - We compared average career win rate across fighting style families, collapsing similar labels (e.g., "Wrestler" and "Freestyle" -> "Wrestling"; "Boxer" and "Brawler" -> "Boxing") to reduce noise from inconsistent source data. We required at least 5 career bouts per fighter and at least 10 fighters per family. MMA led at 74.5%, Boxing trailed at 70.4%, and Wrestling sat at 73.1%, but the spread across all nine families was only about 4 percentage points, which is small relative to how much individual win rates vary. Fighting style family alone does not appear to strongly predict career win rate.


## So What?

**Striking Accuracy vs Win Rate** - Striking accuracy may have some relationship with fighter success, but the large amount of variation shows that other factors also play a major role in winning. One caveat: career striking accuracy is itself an aggregate of the same career we are scoring with win rate, so the two share information and the relationship cannot be read causally.

**Takedown Accuracy vs Win Rate** - Takedown accuracy alone does not seem to have a strong relationship with win rate. This suggests that just being accurate with takedowns is not enough to explain whether a fighter will be successful.

**Fighting Style vs Average Win Rate** - Once the duplicate labels are merged, the apparent wrestler advantage mostly disappears; the gap between the top and bottom style family is about 4 points. Combined with the weak striking and takedown relationships, the pattern across all three analyses is that no single career stat separates winners from losers on its own. That points toward modeling several attributes together, and against betting any single statistic as a signal.

**Implication for prediction** - If no single career stat cleanly separates winners from losers, the path to prediction is to model several attributes together at the fight level — comparing red vs. blue on reach, age, striking accuracy, takedown average, and stance matchup — rather than looking at career aggregates. The ufc-master.csv file provides pre-fight stat snapshots and betting odds, so we can also ask whether any of these stats add information beyond what the market already prices in.


## LIMITATIONS

- **Survivorship bias.** Career win rate is conditioned on keeping a UFC roster spot. Fighters who lose early get cut, so long careers are partly a consequence of winning rather than a neutral sample. We mitigate this by requiring at least 5 bouts, but it cannot be removed from career-level data.
- **Outcome leakage.** A fighter's career striking and takedown accuracy already include the fights whose result we are trying to explain. Avoiding this requires pre-fight snapshots, which only `ufc-master.csv` provides.
- **Join coverage.** Only 65% of fighters matched between `ufcstats_data.csv` and `ufc_athletes.csv`, so the style analysis covers a subset.
- **Sparse physical data.** Reach, height and stance are missing for a large share of older fighters, which limits era-over-era comparisons on those fields.
- **Demographics.** Age is available in `ufc_athletes.csv` and `ufc-master.csv`, but only for a subset of fighters and mainly for post-2010 bouts. Gender is available in `ufc-master.csv`. Nationality is not directly recorded but can be inferred from `place_of_birth` or event `location`/`country` with uncertainty.


## What Next?

**Striking Accuracy vs Win Rate** - We could next see whether striking accuracy has a stronger relationship with winning when fighters are separated by weight class or when it is combined with other striking statistics.

**Takedown Accuracy vs Win Rate** - We could compare takedown accuracy with takedown volume or takedown average to see if fighters who attempt and land more takedowns have different results.

**Fighting Style vs Average Win Rate** - Now that the raw labels are collapsed into families and short careers are filtered out, we could test whether style interacts with the technique stats, for example whether strikers with high takedown defense win more often than strikers without it.

**Move to a fight-level logistic regression** - Rather than predicting career win rate, predict the winner of each individual bout from differences between the two fighters, which sidesteps the survivorship bias in career aggregates. `ufc-master.csv` already supplies red-minus-blue difference columns plus pre-fight stat snapshots and betting odds, so the starting model is:

  red_wins ~ reach_dif + height_dif + age_dif + sig_str_acc_dif + avg_td_dif + C(weight_class) + C(stance_matchup)

with `family = binomial`. Note that `sig_str_dif` in the file is landed-strike volume, not accuracy, so an accuracy difference must be built from `R_avg_SIG_STR_pct - B_avg_SIG_STR_pct`. Adding the odds-implied win probability as a final predictor lets us test which stats, if any, remain significant after accounting for what the betting market already expects.