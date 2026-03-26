# DSA 210 Project: Evolution of Three-Point Shooting in the NBA

## Does the increase in three-point shooting reflect a structural change in NBA playing style over time?

---

## Overview

This project investigates the long-term evolution of three-point shooting in the NBA and examines whether the increase in three-point usage reflects a broader structural change in playing style.

Over the past decades, the NBA has increasingly emphasized perimeter shooting, especially the three-point shot. This project aims to analyze how three-point shooting has evolved over time and whether this shift is associated with other game characteristics such as scoring patterns and pace.

Rather than focusing on individual players, the analysis is conducted at the league level to better understand the overall transformation of basketball strategy.

---

## Terminology

- **3PA (Three-Point Attempts):** Number of three-point shots attempted per game  
- **3PM (Three-Point Made):** Number of three-point shots made per game  
- **3P%:** Three-point shooting accuracy, calculated as `3PM / 3PA`  
- **3P Share in Total Points:** Percentage of total points scored from three-point shots  
- **Pace:** Estimated number of possessions per game, indicating game speed  
- **Season:** A single NBA season (e.g. `1996–97`)  

---

## Motivation

The NBA has undergone a major stylistic transformation over time, with a growing emphasis on three-point shooting. As a basketball follower, I am interested in understanding whether this change is simply gradual or whether it reflects a deeper structural shift in the way the game is played.

This project aims to explore the rise of three-point shooting and examine whether its increasing importance is associated with broader changes in the game, such as higher scoring and changes in pace.

---

## Research Question

**How has three-point shooting evolved in the NBA over time, and does its increase reflect a structural change in overall playing style?**

---

## Hypotheses

- **H₀ (Null Hypothesis):**  
  There is no significant change in three-point shooting trends over time in the NBA.

- **H₁ (Alternative Hypothesis):**  
  Three-point shooting, in terms of attempts and contribution to total scoring, has significantly increased over time in the NBA.

- **H₂:**  
  The share of three-point shots in total scoring has increased significantly over time.

- **H₃:**  
  There is a positive relationship between three-point attempts and total points scored per game.

---

## Data Sources

### 1. Primary Dataset (Kaggle)
**NBA 3-Point Shooting Data (1996–2020)**

This dataset contains season-level averages for:
- `3PM`
- `3PA`
- `3P%`
- `3-point share in total points`

### 2. Secondary Dataset (NBA Official Website - Scraped)
Additional season-level statistics will be collected from the NBA official website, such as:
- Points per game
- Pace
- Additional shooting-related metrics

---

## Data Preparation

The Kaggle dataset provides structured data on three-point shooting statistics across NBA seasons and serves as the main source for analyzing long-term trends in attempts, efficiency, and scoring contribution.

To enrich the analysis, additional season-level data will be scraped from the NBA official website. These variables, such as pace and total scoring, will help evaluate how three-point shooting relates to broader game dynamics.

After collection, the datasets will be:
- cleaned
- standardized
- merged by season
- organized into a time-series structure

The final dataset is expected to contain approximately **25–30 seasons** with multiple statistical features for each season.

---

## Analysis Plan

The project will include:

- **Time-series analysis** of `3PA`, `3P%`, and three-point scoring share
- **Trend visualizations** across seasons
- **Hypothesis testing** to evaluate whether changes are statistically significant
- **Correlation and regression analysis** between three-point shooting and scoring-related variables

---

## Expected Outcome

This project is expected to show that three-point shooting has become increasingly central to NBA offense and that this increase is associated with broader changes in the structure and tempo of the game.

---
