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
This dataset contains the names of all UFC fighters that have fought since the beginning of UFC. It shows their stats such as wins, losses, height, etc. Each row is one fighter's career totals.

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
- str_acc
- td_acc
- sub_avg

This dataset will allow us to compare fighter physical attributes and career accuracy stats against fight outcomes.

## Secondary Datasets

### 1. Ultimate UFC Dataset
**File:** `ufc-master.csv`
**Source:** Kaggle
**Link:** https://www.kaggle.com/datasets/mdabbert/ultimate-ufc-dataset?resource=download&select=ufc-master.csv
This dataset contains all the fights ranging from 2010 - current with the fighter names, their odds, their rankings, and many other goodies. Each row is one fight, with red-corner columns prefixed `R_` and blue-corner columns prefixed `B_`.

The dataset contains:

- 7,177 rows
- 118 columns

Relevant variables include:

- fighter names
- winner
- betting odds
- expected value
- weight class
- title bout flag
- pre-fight career stats (striking accuracy, takedown average, age, reach)

We can use this dataset to see trends in fighting odds vs results, find trends that can help with betting on a fighter, and also train a ML model to predict the result of a fight. Unlike the other files, the stats here are snapshots taken before each fight, which matters when we try to predict outcomes.

### 2. UFC Fighter Stats
**File:** [ufc_athletes.csv](data/ufc_athletes.csv)
**Source:** TidyTuesday UFC Athletes and Fight Data
**Link:** https://github.com/rfordatascience/tidytuesday/blob/main/data/2026/2026-07-07/ufc_athletes.csv
This dataset can be joined with `ufcstats_data.csv` since it has data such as fighting style, gym, place of birth, UFC debut date, KO/TKO wins, submission wins, and decision wins. Each row is one active fighter profile.

The dataset contains:

- 3,145 rows
- 43 columns

Relevant variables include:

- weight_class
- place_of_birth
- age
- height
- weight
- octagon_debut
- fighting_style
- trains_at
- average_fight_time

This dataset will allow us to see multiple stats of all UFC fighters and it can help determine their fighting styles.