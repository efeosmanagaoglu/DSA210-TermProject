# DSA 210 Project  
## Evolution of Three-Point Shooting in the NBA  

### Does the increase in three-point shooting reflect a structural change in NBA playing style over time?

---

## Overview

This project investigates the long-term evolution of three-point shooting in the NBA and examines whether the increase in three-point usage reflects a broader structural change in playing style.

Over the past decades, the NBA has increasingly emphasized perimeter shooting, especially the three-point shot. This project analyzes how three-point shooting has evolved over time and whether this shift is associated with other game characteristics such as scoring patterns and pace.

The analysis is conducted at the league level to capture structural changes in basketball strategy.

---

## Terminology

- **3PA (Three-Point Attempts):** Number of three-point shots attempted per game  
- **3PM (Three-Point Made):** Number of three-point shots made per game  
- **3P%:** Shooting accuracy, calculated as `3PM / 3PA`  
- **ThreePointShare:** Percentage of total points scored from three-point shots  
- **PTS_per_game:** Average points scored per game  
- **Pace:** Estimated number of possessions per game  
- **Season:** NBA season (e.g. `1996–97`)  

---

## Motivation

The NBA has undergone a major stylistic transformation with increasing reliance on three-point shooting. This project aims to determine whether this change is gradual or represents a fundamental structural shift in how the game is played.

### Why this dataset?

Three-point shooting is one of the most visible and measurable changes in modern basketball. Unlike subjective metrics, three-point statistics (attempts, makes, accuracy) are precisely recorded and publicly available. By combining shooting data from Kaggle with pace and scoring data from Basketball Reference, we can examine not just the three-point trend in isolation, but how it relates to broader changes in game tempo and scoring — giving us a more complete picture of the NBA's stylistic evolution.

---

## Research Question

How has three-point shooting evolved in the NBA over time, and does its increase reflect a structural change in overall playing style?

---

## Hypotheses

- **H₀ (Null Hypothesis):**  
  There is no significant difference between early and modern NBA seasons in terms of three-point shooting.

- **H₁ (ThreePointShare):**  
  Three-point scoring share has significantly increased in modern NBA seasons.

- **H₂ (3PA):**  
  Three-point attempts have significantly increased in modern NBA seasons.

- **H₃ (Correlation):**  
  There is a positive relationship between three-point attempts and points per game.

---

## Data Sources

### Primary Dataset (Kaggle)
NBA Three-Point Shooting Data (1996–2020)

Includes:
- 3PM  
- 3PA  
- 3P%  
- ThreePointShare  

### Secondary Dataset (Basketball Reference)
NBA League Averages (Per Game)

Collected as CSV files from:
https://www.basketball-reference.com/

Includes:
- Points per game (PTS)  
- Pace  

---

## Data Preparation

The two raw datasets were combined using the following Python script:

```python
import pandas as pd

# Load raw datasets
df_3pt = pd.read_csv("DATA/raw/NBA_3Point_Shooting_Data.csv")
df_extra = pd.read_csv("DATA/raw/nba_additional_stats_raw.csv")

# Clean column names
df_3pt.columns = df_3pt.columns.str.strip()
df_extra.columns = df_extra.columns.str.strip()

# Standardize season format
df_extra["Season"] = df_extra["Season"].astype(str).str.strip()

# Select relevant columns
df_3pt = df_3pt[["Season", "3PM", "3PA", "3P_percent", "ThreePointShare"]]
df_extra = df_extra[["Season", "PTS_per_game", "Pace"]]

# Merge on Season
df_final = pd.merge(df_3pt, df_extra, on="Season", how="inner")

# Sort and save
df_final = df_final.sort_values(by="Season").reset_index(drop=True)
df_final.to_csv("DATA/processed/final_dataset.csv", index=False)
```

- Final dataset contains **24 seasons** (1996–2020) and **7 features**
- No missing values after merge

---

## Exploratory Data Analysis (EDA)

The EDA includes:

- Time series analysis of:
  - 3PA
  - 3P%
  - ThreePointShare
  - PTS per game
  - Pace

- Correlation analysis:
  - Heatmap visualization
  - Identification of strong relationships

- Scatter plot:
  - 3PA vs Points Per Game
  - Includes regression line

### Key Findings

- **3PA doubled** from 16.8 (1996-97) to 34.1 (2019-20) attempts per game, with sharp acceleration after 2014-15
- **ThreePointShare** grew from ~14% to ~33% — one-third of all points now come from three-pointers
- **3P% remained stable** at ~35%, meaning the increase in volume did not reduce accuracy
- **PTS per game** rose from ~95 to ~112; **Pace** increased from ~90 to ~100 possessions per game
- **Strongest correlations:** 3PA vs PTS (r = 0.95), 3PA vs Pace (r = 0.93), 3PA vs ThreePointShare (r ≈ 1.00)

---

## Hypothesis Testing

### Method

- Dataset split into two eras:
  - **Early era (1996–2008):** 12 seasons
  - **Modern era (2008–2020):** 12 seasons

- **Welch's independent two-sample t-test** was used because:
  - We are comparing means of two independent groups
  - Welch's variant does not assume equal variances, making it more robust for our small sample sizes (n=12 per group)

---

### Results

#### Test 1: ThreePointShare (Early vs Modern)
| Metric | Value |
|--------|-------|
| Early era mean | 16.60% |
| Modern era mean | 24.07% |
| t-statistic | -4.8472 |
| p-value | 0.000273 |
| Cohen's d | 1.98 (very large) |

**Interpretation:** The modern era has a 7.47 percentage point higher three-point scoring share. With p = 0.000273 (far below 0.05), we reject H₀. The large Cohen's d (1.98) confirms this is a practically meaningful difference, not just a statistical artifact.

#### Test 2: 3PA (Early vs Modern)
| Metric | Value |
|--------|-------|
| Early era mean | 15.10 |
| Modern era mean | 23.56 |
| t-statistic | -4.9296 |
| p-value | 0.000286 |
| Cohen's d | 2.01 (very large) |

**Interpretation:** Modern teams attempt 8.46 more three-pointers per game — a 56% increase. With p = 0.000286, we reject H₀. Cohen's d of 2.01 indicates an extremely large effect size.

#### Correlation Analysis
- 3PA vs PTS_per_game: **r = 0.95** (very strong positive)
- Three-point shooting volume is strongly associated with overall scoring

---

## Conclusion

The results show that the increase in three-point shooting is not random but represents a statistically significant structural change in NBA playing style (p < 0.001 for both tests, Cohen's d > 1.9).

Modern NBA offenses rely heavily on three-point shooting: the three-point share of scoring rose from 16.6% to 24.1%, and attempts increased by 56%. This shift is strongly associated with increased scoring (r = 0.95) and faster gameplay (r = 0.93), while three-point accuracy remained stable at ~35% — suggesting a deliberate strategic transformation rather than random variation.

---

## Project Structure

```
├── DATA/
│   ├── raw/
│   │   ├── NBA 3-Point Shooting Data (1996-2020).xlsx
│   │   └── nba_additional_stats_raw.csv
│   └── processed/
│       └── final_dataset.csv
├── EDA.ipynb
├── Hypothesis_Testing.ipynb
├── Proposal Report.pdf
├── requirements.txt
└── README.md
```


---

## Limitations

- The dataset covers only league-wide averages, not individual team or player data, which limits the granularity of the analysis.
- The sample size is relatively small (24 seasons), which may reduce the statistical power of some tests.
- Correlation between 3PA and scoring does not imply causation; other confounding factors (rule changes, player development) are not controlled for.
- The era split at the midpoint (2008) is somewhat arbitrary and may not align with the actual structural breakpoint.

---

## Future Work

- Add advanced metrics (e.g., offensive rating)
- Apply machine learning models
- Detect structural breakpoints more formally

---

## How to Reproduce

1. Clone the repository:
   ```bash
   git clone https://github.com/efeosmanagaoglu/DSA210-TermProject.git
   cd DSA210-TermProject
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Run the notebooks in order:
   - `EDA.ipynb` — Exploratory Data Analysis
   - `Hypothesis_Testing.ipynb` — Statistical hypothesis tests

---

## Author

Efe Osmanağaoğlu - 33979