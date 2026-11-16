## Dataset A: UFC Historical Fight Database (`ufc_fights`)

| | |
|---|---|
| Rows × Cols | 8,736 × 15 |
| One row | One UFC fight/bout |
| Years covered | 1994–2026 |
| Geography | Global |
| License | CC0 1.0 Universal (via TidyTuesday) |

### 1. Motivation
- **Creation:** TidyTuesday (a weekly social data project on GitHub) curates datasets for community exploration. This subset was compiled by Benjamin Smith (curator) via the `fightr` R package, which aggregates UFCStats, Kaggle, and the Octagon API, to allow analysis of fight outcomes, physical advantages, and betting odds.
- **Funded by:** TidyTuesday is a volunteer-driven community project.

### 2. Composition
- **One row represents:** A single UFC fight, including the two fighters, event details, and outcome.
- **Rows:** 8,736. **Columns:** 15.
- **Census?** It is a census of recorded UFC fights available in the source aggregators up to the collection date.

### 3. Collection process
- **Gathering method:** Automated scraping and API aggregation. The `fightr` package compiles data from UFCStats, Kaggle datasets, and the Octagon API.
- **Time frame:** Historical records from UFC inception (1993) through the TidyTuesday release date (July 2026). Data covers fights from **1994–2026**.
- **Consent:** The data is about public sporting events and publicly available athlete profiles. No direct consent was required because the data is public record.

### 4. Preprocessing
- **Publisher cleaning:** The `fightr` package standardizes fighter names, formats dates, and normalizes weight class strings. TidyTuesday provides the data as a clean CSV.
- **Raw data:** The raw CSV is in the TidyTuesday GitHub repository.

### 5. Uses
- **Already used for:** TidyTuesday participant projects (exploratory data analysis, visualization). Uses include analysis of physical advantages and betting prediction models.
- **Should not be used for:** Medical diagnosis of fighter injuries.

### 6. Distribution
- **Published:** TidyTuesday GitHub Repository (`rfordatascience/tidytuesday`) in CSV format.
- **License:** CC0 1.0 Universal (Public Domain). No restrictions on reuse.

### 7. Maintenance
- **Maintained by:** Jon Harmon (Owner of repo)
- **Updated?** The TidyTuesday GitHub repo is updated weekly. However, this UFC data is from July 2026 and has been the same since. For this dataset, updates would require a new `fightr` package release or an expanded UFC dataset.

## Dataset B: UFC Stats Athlete Profiles (`ufcstats_data`)

| | |
|---|---|
| Rows × Cols | 4,504 × 18 |
| One row = | One UFC fighter's career profile |
| Years covered | Fighters active 1993–2026 |
| Geography | Global roster |
| Missing data | `height`, `weight`, `reach`, `dob`: `"NA"` placeholder strings; `stance`: `"NA"` in some rows |
| License | CC0 1.0 Universal (via TidyTuesday) |

### 1. Motivation
- **Creation:** Companion athlete-level file to `ufc_fights`, released for the same TidyTuesday week so users can join fighter attributes to bout outcomes. Created and compiled by Benjamin Smith (curator) via the `fightr` package.
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
- **Raw data:** The raw CSV is in the TidyTuesday GitHub repository.

### 5. Uses
- **Already used for:** Analyses linking reach/height advantages to win rates and striking/takedown accuracy to divisional ranking.
- **Should not be used for:** Betting recommendations; comparing eras directly, inferring health or injury status.

### 6. Distribution
- **Published:** TidyTuesday GitHub Repository (`rfordatascience/tidytuesday`) in CSV format.
- **License:** CC0 1.0 Universal (Public Domain). No restrictions on reuse.

### 7. Maintenance
- **Maintained by:** Jon Harmon (Owner of repo)
- **Updated?** The TidyTuesday GitHub repo is updated weekly. However, this UFC data is from July 2026 and has been the same since. For this dataset, updates would require a new `fightr` package release or an expanded UFC dataset.


## Part 2 — Scope

**RQ1: Do taller fighters, or fighters with longer reach or a reach advantage, win more often?**
*   **Target Population:** All professional MMA fighters who have competed in any professional promotion.
*   **Access Frame:** UFCStats.com athlete profiles for fighters who have competed in the UFC.
*   **Sample:** 4,504 UFC fighters with available profile data (Dataset B).
*   **Missing from Data:** Fighters who competed in other promotions (Bellator, ONE, etc.) but never in the UFC. Also UFC fighters who never had a UFCStats profile created.
*   **Limitation:** Results apply only to the UFC roster. The UFC has specific recruitment biases, so correlations may not hold for the whole MMA industry.

**RQ2: Are strikers or grapplers more successful — is striking accuracy or takedown accuracy more strongly tied to winning?**
*   **Target Population:** All UFC fighters throughout the sport's history.
*   **Access Frame:** UFCStats.com profiles joined with `ufc_athletes.csv` for fighting style classification.
*   **Sample:** 2,924 fighters who matched between `ufcstats_data.csv` and `ufc_athletes.csv` (65% of 4,504), filtered to those with ≥5 career bouts.
*   **Missing from Data:** Fighters whose names did not match between sources; fighters retired before their stats were scraped; fighters whose early-career stats are incomplete or missing.
*   **Limitation:** Career win rate is biased toward fighters who stayed in the UFC long enough to accumulate wins (survivorship bias). Requiring at least 5 bouts mitigates but does not eliminate this bias.

**RQ3: How has the baseline frequency of distance decisions vs. early knockout finishes evolved over the sport's developmental eras?**
*   **Target Population:** All UFC fights from 1993 to 2026.
*   **Access Frame:** The `ufc_fights` dataset.
*   **Sample:** 8,736 UFC fights.
*   **Missing from Data:** Scheduled fights that did not take place, early-era fights (1993–1994) where referee reporting was less standardized.
*   **Limitation:** The dataset only includes completed bouts. It cannot speak to how often fights are cancelled. Early-era data may underreport certain finish types due to less record-keeping and different rules.


## Part 3 — Codebook

## Dataset A: `ufc_fights` (raw columns)

| name | type | units | meaning | range / allowed values | missing coded as | source |
|---|---|---|---|---|---|---|
| `fight_url` | str | — | UFCStats.com page URL for the bout | unique URLs | none | raw |
| `event_name` | str | — | Name of the UFC event | free text | none | raw |
| `date` | datetime | date | Date the event took place | 1994-03-11 to 2026-06-27 | none | raw; parsed via `pl.str.strptime()` in `eda.ipynb` |
| `location` | str | — | Host city + state/country | free text | none | raw |
| `f1_name` | str | — | First listed fighter's name | matches UFCStats spelling | none | raw |
| `f1_result` | str | — | Outcome for fighter 1 | `"W"`, `"L"` | none (incomplete bouts removed upstream) | raw |
| `f2_name` | str | — | Second listed fighter's name | matches UFCStats spelling | none | raw |
| `f2_result` | str | — | Outcome for fighter 2 | `"W"`, `"L"` | none | raw |
| `weight_class` | str | — | Bout category | 123 values, e.g. `"Lightweight Bout"`, `"UFC Lightweight Title Bout"` | none | raw |
| `method` | str | — | How the fight ended | 10 values: Decision (Unanimous/Split/Majority), KO/TKO, Submission, TKO - Doctor's Stoppage, DQ, Overturned, Could Not Continue, Other | none | raw |
| `round` | int | round # | Round in which the fight ended | 1–5 | none | raw |
| `time` | str | min/sec | Elapsed time in final round at stoppage | e.g. `"5M 0S"`, `"38S"` | none | raw |
| `time_format` | str | rounds | Scheduled fight length | e.g. `"3 Rnd (5-5-5)"`, `"5 Rnd (5-5-5-5-5)"` | none | raw |
| `referee` | str | — | Referee name | free text | none | raw |
| `judging_details` | str | — | Scorecard or stoppage description | free text (e.g. `"Punches to Head On Ground"`) | none detected in raw CSV | raw |

## Dataset B: `ufcstats_data` (raw columns)

| name | type | units | meaning | range / allowed values | missing coded as | source |
|---|---|---|---|---|---|---|
| `name` | str | — | Fighter name as listed on UFCStats | matches `f1_name`/`f2_name` join key | none | raw |
| `wins` | int | bouts | Career wins | 0–~100+ | none | raw |
| `losses` | int | bouts | Career losses | 0–~100+ | none | raw |
| `draws` | int | bouts | Career draws | 0–few | none | raw |
| `nc` | int | bouts | No-contest results | 0–few | none | raw |
| `height` | str → float | inches | Fighter height | formatted `"5' 11\""`; converted to numeric | literal string `"NA"` | raw; parsed in `eda.ipynb` |
| `weight` | str → float | pounds | Listed weight class weight | formatted `"155 lbs."`; converted to numeric | literal string `"NA"` | raw; parsed in `eda.ipynb` |
| `reach` | str → float | inches | Arm reach | formatted `"70\""`; converted to numeric | literal string `"NA"` | raw; parsed in `eda.ipynb` |
| `stance` | str | — | Fighting stance | `"Orthodox"`, `"Southpaw"`, `"Switch"`, `"Open Stance"`, `"Sideways"` | literal string `"NA"` | raw |
| `dob` | str → datetime | date | Date of birth | formatted `"Jul 13, 1978"`; parsed to date | literal string `"NA"` | raw; parsed in `eda.ipynb` |
| `s_lp_m` | float | strikes/min | Significant strikes landed per minute | ~0–10 | none | raw |
| `str_acc` | str → float | % | Significant striking accuracy | formatted `"77%"`; stripped to 0–100 | literal string `"NA"` if present | raw; `%` stripped in `eda.ipynb` |
| `s_ap_m` | float | strikes/min | Significant strikes absorbed per minute | ~0–10 | none | raw |
| `str_def` | str → float | % | Significant strike defense | formatted `"66%"`; stripped to 0–100 | `"NA"` if present | raw; `%` stripped in `eda.ipynb` |
| `td_avg` | float | takedowns/15 min | Average takedowns landed | 0–~15 | none | raw |
| `td_acc` | str → float | % | Takedown accuracy | formatted `"33%"`; stripped to 0–100 | `"NA"` if present | raw; `%` stripped in `eda.ipynb` |
| `td_def` | str → float | % | Takedown defense | formatted `"77%"`; stripped to 0–100 | `"NA"` if present | raw; `%` stripped in `eda.ipynb` |
| `sub_avg` | float | attempts/15 min | Average submission attempts | 0–~10 | none | raw |

## Derived columns (created in `eda.ipynb`)

| name | type | units | meaning | range / allowed values | missing coded as | source |
|---|---|---|---|---|---|---|
| `win_rate` | float | % | Career win rate: `wins / (wins + losses + draws) × 100`, rounded to 1 dp | 0.0–100.0 | `NaN` when a fighter has 0 recorded bouts | derived: `wins / (wins + losses + draws)` in `eda.ipynb` |
| `fight_year` | int | year | Year extracted from `date` for chronological grouping | 1994–2026 | none | derived: `.dt.year()` in `eda.ipynb` |
| `style_family` | str | category | Collapsed fighting style family (12 categories) | `"Boxing"`, `"BJJ"`, `"Wrestling"`, `"Grappling"`, `"Striking"`, `"MMA"`, `"Karate"`, `"Kickboxer"`, `"Muay Thai"`, `"Taekwondo"`, `"Sambo"`, `"Freestyle"` | `null` if `fighting_style` is null | derived: `STYLE_MAP` applied to `fighting_style` in `eda.ipynb` |
| `total_bouts` | int | bouts | Total career bouts (wins + losses + draws) | 0–~300 | none | derived: sum of W/L/D in `eda.ipynb` |

**Planned derived columns (for future modeling):**

| name | type | units | meaning | range / allowed values | missing coded as | source |
|---|---|---|---|---|---|---|
| `career_length` | int | years | Years between first and last fight | 0–~25 | n/a | planned: derived from `ufc_fights` dates per fighter |
| `era` | str | category | Developmental era label | e.g. `1994–2004`, `2005–2015`, `2016–2026` | none | planned: binned by `fight_year` |
| `finish_type` | str | category | Simplified outcome class | `"Decision"`, `"KO/TKO"`, `"Submission"`, `"Other"` | none | planned: recoded from `method` |
| `early_finish` | int (bool) | 0/1 | Fight ended before final scheduled round | 0 or 1 | none | planned: compares `round` vs `time_format` |
| `striking_vs_grappling` | float | ratio | Strike volume relative to grappling

## Part 4 — Recipe

1. **Load files** from `ufc_fights.csv`, `ufcstats_data.csv`, `ufc-master.csv`, and `ufc_athletes.csv`. Cell 1–4 in `data_acquisition.ipynb` (`pl.read_csv` calls).
2. **Load files** from `ufc_fights.csv`, `ufcstats_data.csv`, and `ufc_athletes.csv`. Cell 1 in `eda.ipynb` (`pl.read_csv` calls).
3. **Fix placeholder missing values** in `ufcstats_data`: literal string `"NA"` → true nulls across all string columns. Cell 1 in `eda.ipynb`.
4. **Parse numeric fields**: strip `%` from `str_acc`, `str_def`, `td_acc`, `td_def` and cast to float; strip `" lbs."` from `weight`; strip `'"'` from `reach`. Rows dropped: 0. Cell 1 in `eda.ipynb`.
5. **Derive `win_rate`**: `wins / (wins + losses + draws) × 100`, rounded to 1 dp; set to 0 when total fights = 0. Cell 1 in `eda.ipynb`.
6. **Parse dates** in `ufc_fights`: `date` string → Date type, extract `fight_year`. Rows dropped: 0. Cell 1 in `eda.ipynb`.
7. **Aggregate timeline table**: group fights by `fight_year`, compute total fights and % decided by decision. Result: 33 rows (1994–2026). Cell 1 in `eda.ipynb`.
8. **Join fighter profiles to fighting styles** — inner join `ufcstats_data` to `ufc_athletes.csv` on `name`, then collapse the 19 raw `fighting_style` labels into 12 families via `STYLE_MAP`. Filter to fighters with ≥5 career bouts and styles with ≥10 fighters. Matched 2,924 of 4,504 fighters (65%); unmatched due to name-format differences between ufcstats.com and ufc.com. Rows dropped by join: 1,580. Cell 2-4.
9. **EDA plots** — four histograms (wins, reach, takedown avg, striking accuracy), scatter plots (str/takedown accuracy vs win rate), timeline plot (decision % over years), and bar chart (avg win rate by style family). Cells 5-9.

## Part 5 — Access and Reuse

### Dataset A: UFC Historical Fight Database (`ufc_fights`)

| FAIR principle | Item | Details |
|---|---|---|
| **Findable** | Source | https://github.com/rfordatascience/tidytuesday/tree/main/data/2026/2026-07-07 |
|  | Direct download URL | https://raw.githubusercontent.com/rfordatascience/tidytuesday/main/data/2026/2026-07-07/ufc_fights.csv |
|  | Version / access date | TidyTuesday release dated 2026-07-07 |
| **Accessible** | Access | Open access through GitHub; no authentication required |
| **Interoperable** | File format | CSV |
| **Reusable** | License | CC0 1.0 Universal |
|  | Processed data reuse | Processed data may be reused if the group releases it under the same or another compatible open license |

### Dataset B: UFC Stats Athlete Profiles (`ufcstats_data`)

| FAIR principle | Item | Details |
|---|---|---|
| **Findable** | Source | https://github.com/rfordatascience/tidytuesday/tree/main/data/2026/2026-07-07 |
|  | Direct download URL | https://raw.githubusercontent.com/rfordatascience/tidytuesday/main/data/2026/2026-07-07/ufcstats_data.csv |
|  | Version / access date | TidyTuesday release dated 2026-07-07 |
| **Accessible** | Access | Open access through GitHub; no authentication required |
| **Interoperable** | File format | CSV |
| **Reusable** | License | CC0 1.0 Universal |
|  | Processed data reuse | Processed data may be reused if the group releases it under the same or another compatible open license |


## Part 6 — People in the Data

### Who is represented

- `ufc_fights.csv` represents professional UFC fighters and includes referee names associated with recorded UFC bouts.
- `ufcstats_data.csv` represents professional UFC fighters with UFCStats profile information.
- The data describes public fight results and publicly available athlete statistics.

### Representation and potential misrepresentation

- The data only includes fighters who reached the UFC, so it does not represent all professional MMA fighters.
- Fighters from other promotions, amateur fighters, and athletes without UFCStats profiles are missing.
- Women are underrepresented because women's divisions were introduced later and there are fewer women's weight classes.
- The dataset does not include race, ethnicity, nationality, gender identity, or socioeconomic information. Date of birth is available for most fighters in `ufcstats_data.csv`, so age can be derived; `ufc_athletes.csv` lists age directly and `ufc-master.csv` records fighter age at the time of each bout.

### Ethical considerations

Although the datasets are publicly available and released under CC0, they describe real people's careers and performance. Analyses should stay within what the recorded UFC statistics support. The data should not be used to make unsupported claims about a fighter's health, intelligence, character, or overall ability outside the measured performance statistics. Researchers should also avoid sensationalizing losses, injuries, or poor performance when presenting results.
