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
This dataset contains the names of all UFC fighters as well as their stats such as wins, losses, height, etc.

The dataset contains:

- 8,736 rows
- 15 columns

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


### 3. Ultimate UFC Dataset
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


## Secondary Datasets
### UFC Fighter Stats
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
