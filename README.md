#DSA 210 Project: Evolution of Three-Point Shooting in the NBA
Does the increase in three-point shooting reflect a structural change in NBA playing style over time?
Terminology

3PA (Three-Point Attempts): Number of three-point shots attempted per game.

3PM (Three-Point Made): Number of three-point shots made per game.

3P%: Three-point shooting accuracy (3PM / 3PA).

3P Share in Total Points: Percentage of total points scored from three-point shots.

Pace: Estimated number of possessions per game, indicating game speed.

Season: A single NBA season (e.g., 1996–97).

Motivation

Over the past decades, the NBA has undergone a significant transformation in playing style, with an increasing emphasis on three-point shooting. As a basketball follower, I am interested in understanding whether this change is gradual or represents a structural shift in how the game is played.

This project aims to analyze how three-point shooting has evolved over time and whether its increasing usage is associated with broader changes in the game, such as scoring patterns and pace. Rather than focusing on individual players, the analysis will examine league-wide trends to capture the overall evolution of basketball strategy.

Hypothesis

Null Hypothesis (H₀):
There is no significant change in three-point shooting trends over time in the NBA.

Alternative Hypothesis (H₁):
Three-point shooting (in terms of attempts and contribution to total scoring) has significantly increased over time in the NBA.

Sub Hypothesis (H₂):
The share of three-point shots in total scoring has increased significantly over time.

Sub Hypothesis (H₃):
There is a positive relationship between three-point attempts and total points scored per game.

Data Sources

Primary Dataset (Kaggle):
NBA 3-Point Shooting Data (1996–2020)

Contains season-level averages for:
3PM
3PA
3P%
3-point share in total points

Secondary Dataset (NBA Official Website - Scraped):

Season-level team or league statistics such as:
Points per game
Pace
Additional shooting metrics
Data Preparation

The Kaggle dataset provides structured data on three-point shooting statistics across NBA seasons. This dataset will be used as the main source for analyzing trends in three-point attempts, efficiency, and scoring contribution.

To enrich the analysis, additional data will be collected by scraping the NBA official website. This includes variables such as pace and total scoring, which will allow for examining how three-point shooting relates to overall game dynamics.

The datasets will be cleaned, merged by season, and organized into a time-series format. The final dataset is expected to include approximately 25–30 seasons, with multiple statistical features per season.

Analysis Plan (Short)
Time-series analysis of 3PA, 3P%, and 3P scoring share
Visualization of trends over time
Hypothesis testing (trend significance)
Correlation/regression analysis between 3-point shooting and scoring
