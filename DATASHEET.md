## Dataset A: UFC Historical Fight Database (`ufc_fights`)

| | |
|---|---|
| Rows × Cols | 8,736 × 15 |
| One row | One UFC fight/bout |
| Years covered | 1994–2026 |
| Geography | Global |
| License | CC0 1.0 Universal (via TidyTuesday) |

### 1. Motivation
- **Creation:** TidyTuesday (a weekly social data project on github) curates datasets for community exploration. This subset was compiled by Benjamin Smith (curator) via the `fightr` R package, which aggregates UFCStats, Kaggle, and the Octagon API, to allow analysis of fight outcomes, physical advantages, and betting odds.
- **Funded by:** TidyTuesday is a volunteer-driven community project.

### 2. Composition
- **One row represents:** A single UFC fight, including the two fighters, event details, and outcome.
- **Rows:** 8,736. **Columns:** 15.
- **Census?** It is a census of recorded UFC fights available in the source aggregators up to the collection date..

### 3. Collection process
- **Gathering method:** Automated scraping and API aggregation. The `fightr` package compiles data from UFCStats, Kaggle datasets, and the Octagon API.
- **Time frame:** Historical records from UFC inception (1993) through the TidyTuesday release date (July 2026). Data covers fights from **1994–2026**.
- **Consent:** The data is about public sporting events and publicly available athlete profiles. No direct consent was required because the data is public record.

### 4. Preprocessing
- **Publisher cleaning:** The `fightr` package standardizes fighter names, formats dates, and normalizes weight class strings. TidyTuesday provides the data as a clean CSV.
- **Raw data** The raw CSV is in the TidyTuesday GitHub repository.

### 5. Uses
- **Already used for:** TidyTuesday participant projects (exploratory data analysis, visualization). Uses include analysis of physical advantages and betting prediction models.
- **Should not be used for:** Medical diagnosis of fighter injuries.

### 6. Distribution
- **Published:** TidyTuesday GitHub Repository (`rfordatascience/tidytuesday`) in CSV format.
- **License:** CC0 1.0 Universal (Public Domain). No restrictions on reuse.

### 7. Maintenance
- **Maintained by:** Jon Harmon (Owner of repo)
- **Updated?** The TidyTuesday GitHub repo is updated weekly. However, this ufc data is from July 2026 and has been the same since. For this dataset, updates would require a new `fightr` package release or an expanded UFC dataset.

## Dataset B: UFC Stats Athlete Profiles (`ufcstats_data`)

| | |
|---|---|
| Rows × Cols | 4,504 × 18 |
| One row = | One UFC fighter's career profile |
| Years covered | Fighters active 1993–2026 |
| Geography | Global roster|
| Missing data | `height`, `weight`, `reach`, `dob`: `"NA"` placeholder strings; `stance`: `"NA"` in some rows |
| License | CC0 1.0 Universal (via TidyTuesday) |

### 1. Motivation
- **Creation:** Companion athlete-level file to `ufc_fights`, released for the same TidyTuesday week so users can join fighter attributes to bout outcomes. Created and compiled by Benjamin Smith(curator) via the `fightr` package.
- **Funded by:** Volunteer-driven community project.

### 2. Composition
- **One row represents:** One individual UFC fighter, with career totals and performance averages.
- **Rows / Columns:** 4,504 × 18.
- **Census?** Census of fighters with a UFCStats.com profile page as of the scrape date. Not a random sample.
- **What's missing:** The publisher uses the literal string `"NA"` (not a null/missing marker) to indicate unavailable data. Gaps are concentrated in physical attributes:
    - `height`, `weight`, `reach`, `dob`: `"NA"` for fighters whose measurements were never published on UFCStats
    - `stance`: `"NA"` in a subset of rows (stance was not always recorded historically).
    - All numeric career stats (`wins`, `losses`, `draws`, `nc`) are fully populated.
    - Performance metrics (`str_acc`, `td_acc`, etc.) are stored as percentage-formatted strings (e.g. `"77%"`) rather than numeric proportions.

### 3. Collection process
- **Gathering method:** Automated scraping and API aggregation. The `fightr` package compiles data from UFCStats, Kaggle datasets, and the Octagon API.
- **Time frame:** Career statistics accumulated from each fighter's debut through the July 2026 snapshot.
- **Consent:** The data is about public sporting events and publicly available athlete profiles. No direct consent was required because the data is public record.

### 4. Preprocessing
- **Publisher cleaning:** `fightr` standardizes names to match UFCStats listings and cleans column names via `janitor::clean_names()`. The publisher does **not** convert placeholder `"NA"` strings to true missing values, nor does it parse height/weight/reach into numerics. Accuracy fields are stored as formatted strings with `%` symbols.
- **Raw data** The raw CSV is in the TidyTuesday GitHub repository.

### 5. Uses
- **Already used for:** Analyses linking reach/height advantages to win rates and striking/takedown accuracy to divisional ranking.
- **Should not be used for:** Betting recommendations; comparing eras directly, inferring health or injury status.

### 6. Distribution
- **Published:** TidyTuesday GitHub Repository (`rfordatascience/tidytuesday`) in CSV format.
- **License:** CC0 1.0 Universal (Public Domain). No restrictions on reuse.

### 7. Maintenance
- **Maintained by:** Jon Harmon (Owner of repo)
- **Updated?** The TidyTuesday GitHub repo is updated weekly. However, this ufc data is from July 2026 and has been the same since. For this dataset, updates would require a new `fightr` package release or an expanded UFC dataset.



# Part 2 — Scope

**RQ1: What baseline physical attributes and dynamic stance metrics correlate with higher career win ratios across distinct eras?**
*   **Target Population:** All professional MMA fighters who have competed in any professional promotion.
*   **Access Frame:** UFCStats.com athlete profiles for fighters who have competed in the UFC.
*   **Sample:** 4,504 UFC fighters with available profile data (Dataset B).
*   **Missing from Data:** Fighters who competed in other promotions (Bellator, ONE, etc.) but never in the UFC. Also UFC fighters who never had a UFCStats profile created.
*   **Limitation:** Results apply only to the UFC roster. The UFC has specific recruitment biases, so correlations may not hold for the whole MMA industry.

**RQ2: How do strike-delivery volumes vs. offensive grappling paces split out long-term veteran paths from short-duration prospect profiles?**
*   **Target Population:** All UFC fighters throughout the sport's history.
*   **Access Frame:** UFCStats.com profiles of UFC fighters as of July 2026.
*   **Sample:** 4,504 UFC fighters.
*   **Missing from Data:** Fighters who retired before their stats were scraped; fighters whose early-career stats are incomplete or missing.
*   **Limitation:** The data is a snapshot. Fighters still active in 2026 are classified as "prospects" based on current tenure, even if they go on to have long careers. Short-duration is relative to the 2026 cutoff, not the fighter's actual career length.

**RQ3: How has the baseline frequency of distance decisions vs. early knockout finishes evolved chronologically over the sport's developmental eras?**
*   **Target Population:** All UFC fights from 1993 to 2026.
*   **Access Frame:** The `ufc_fights` dataset.
*   **Sample:** 8,736 UFC fights.
*   **Missing from Data:** Scheduled fights that did not take place, early-era fights (1993–1994) where referee reporting was less standardized.
*   **Limitation:** The dataset only includes completed bouts. It cannot speak to how often fights are cancelled. Early-era data may underreport certain finish types due to less record-keeping and different rules.
