# cs418-ufc-fight-analysis
Names: Taufeeq Patel, Christian Pimentel, Uzair Azizuddin, Firas Al Halaq

## Research Questions
The project will investigate UFC fight outcomes and the factors associated with winning.

Our current research questions are:

1. What fighter and fight characteristics are associated with winning UFC fights?
2. How are striking and grappling statistics associated with fight outcomes?
3. How have UFC fight characteristics and outcomes changed over time?

## Primary Datasets
### 1. UFC Fights Dataset
**File:** `ufc_fights.csv`  
**Source:** TidyTuesday UFC Athletes and Fight Data  
**Link:** https://github.com/rfordatascience/tidytuesday/blob/main/data/2026/2026-07-07/ufc_fights.csv
This dataset contains historical UFC fight information. Each row represents one UFC fight.

The dataset contains:

- 8,736 rows
- 15 columns

Relevant variables include:

- fighter names
- fight results
- event date
- location
- weight class
- method of victory
- round
- fight time
- referee

This dataset will allow us to analyze fight outcomes, methods of victory, weight classes, and changes in UFC fights over time.

### 2. UFC Stats Dataset
**File:** `ufcstats_data.csv`
**Source:** TidyTuesday UFC Athletes and Fight Data
**Link:** https://github.com/rfordatascience/tidytuesday/blob/main/data/2026/2026-07-07/ufcstats_data.csv
This dataset contains the names of all UFC fighters that have fought since the beginning of UFC. It shows their stats such as wins, losses, height, etc.

The dataset contains:

- 4,504 rows
- 18 columns

Variables:

- wins
- losses
- draws
- height
- weight
- stance
- td_acc
- sub_avg

This dataset will allow us to see multiple stats of all UFC fighters and it can help determine their fighting styles.

## Secondary Datasets

### 1. Ultimate UFC Dataset
**File:** `ufc-master.csv`
**Source:** Kaggle
**Link:** https://www.kaggle.com/datasets/mdabbert/ultimate-ufc-dataset?resource=download&select=ufc-master.csv
This dataset contains all the fights ranging from 2010 - current with the fighter names, their odds, their rankings, and many other goodies.  

There are:
- 118 columns

Relevant Variables:
- R_fighter
- B_fighter
- R_odds
- B_odds
- R_ev
- B_ev


We can use this dataset to see trends in fighting odds vs results, find trends that can help with betting on a fighter, and also train a ML model to predict the result of a fight.

### 2. UFC Fighter Stats
**File:** [ufc_athletes.csv](data/ufc_athletes.csv)
**Source:** TidyTuesday UFC Athletes and Fight Data
**Link:** https://github.com/rfordatascience/tidytuesday/blob/main/data/2026/2026-07-07/ufc_athletes.csv
This dataset can be joined with 'ufcstats_data.csv' since it doesn't have data such as 
fighting style, gym, place of birth, UFC Debut date, KO/TKO wins, submission win, and decision wins.

The Data Contains:
- 43 Columns
- 3146 Rows

Relevant Variables
- weight_class
- place_of_birth
- age
- height
- weight
- octagon_debut
- fighting_style
- average_fight_time


## Exploratory Analysis
-----------------------------------------
Our exploratory data science phase evaluated 4,504 unique UFC athletes alongside 8,736 historical matches to uncover hidden tactical and physical success signals.

### Core Dataset Metadata
* **Primary Athletes Database (`ufcstats_data.csv`):** 4,504 Rows | 19 Columns
* **Historical Match Database (`ufc_fights.csv`):** 8,736 Rows | 16 Columns

### Cleaned System Anomalies
All mixed physical text tags (`155 lbs.`, `42%`) and literal string `"NA"` characters were filtered out via regular expressions, normalized into uniform numeric systems, and safely logged without row-loss deletion.

### Revised Project Research Framework
1. What baseline physical attributes and dynamic stance metrics correlate with higher career win ratios across distinct eras?
2. How do strike-delivery volumes vs. offensive grappling paces split out long-term veteran paths from short-duration prospect profiles?
3. How has the baseline frequency of distance decisions vs. early knockout finishes evolved chronologically over the sport's developmental eras?

* **Why they changed:** The data profiling phase exposed that legacy physical traits (such as reach values before 2005) suffer from an intense 43% null deficiency rate. We adjusted our research questions to focus on high-fidelity features (Stance, Volume Output, and Match Chronology) to eliminate any historical entry bias in our future predictive models.

## Data Documentation

Full documentation in [`DATASHEET.md`](DATASHEET.md).

| Dataset | Source | License |
| --- | --- | --- |
| [UFC Fights](https://github.com/rfordatascience/tidytuesday/blob/main/data/2026/2026-07-07/ufc_fights.csv) | TidyTuesday (rfordatascience/tidytuesday) | CC0 1.0 Universal |
| [UFC Stats](https://github.com/rfordatascience/tidytuesday/blob/main/data/2026/2026-07-07/ufcstats_data.csv) | TidyTuesday (rfordatascience/tidytuesday) | CC0 1.0 Universal |

**Biggest limitation:** The data only covers fighters in the UFC, so results reflect elite MMA fighters, it cannot be generalized to all of the sport. It also lacks demographic fields (age, gender, nationality), limiting any representation analysis. However, the datasheets can be combined with other data which could makeup for some limitations.
