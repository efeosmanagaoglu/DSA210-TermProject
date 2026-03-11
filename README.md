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

- Data from Kaggle and Basketball Reference were combined
- Cleaned and standardized column names
- Merged using the `Season` column
- Final dataset contains:
  - 24 seasons
  - 7 features

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

- 3PA increases significantly over time  
- Sharp acceleration after ~2015  
- ThreePointShare steadily increases  
- Points per game and pace also increase  
- Strong positive correlation between 3PA and scoring  

---

## Hypothesis Testing

### Method

- Dataset split into two eras:
  - Early era (1996–2008)
  - Modern era (2008–2020)

- Independent two-sample t-test applied:
  - `ThreePointShare`
  - `3PA`

---

### Results

#### Test 1: ThreePointShare
- p-value < 0.001  
- Significant increase in modern era  
- H₀ rejected  

#### Test 2: 3PA
- p-value < 0.001  
- Significant increase in attempts  
- H₀ rejected  

#### Correlation Analysis
- Correlation (3PA vs PTS): ~0.95  
- Strong positive relationship  

---

## Conclusion

The results show that the increase in three-point shooting is not random but represents a statistically significant structural change in NBA playing style.

Modern NBA offenses rely heavily on three-point shooting, which is strongly associated with increased scoring and faster gameplay.

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