# DSA 210 Project Proposal  
## Evolution of Three-Point Shooting in the NBA  

### Motivation  
Over the past decades, the NBA has undergone a significant transformation, with an increasing emphasis on three-point shooting. As a basketball follower, I am interested in understanding whether this change is gradual or represents a structural shift in how the game is played.

---

### Research Question  
How has three-point shooting evolved in the NBA over time, and does its increase reflect a structural change in overall playing style?

---

### Data Sources  

**Primary Dataset (Kaggle):**  
NBA Three-Point Shooting Data (1996–2020)  
- Covers approximately 24 NBA seasons  
- Features include:  
  - 3PA (Three-Point Attempts)  
  - 3PM (Three-Point Made)  
  - 3P% (Accuracy)  
  - Three-point share in total points  

**Secondary Dataset (NBA Official Website - Web Scraping):**  
Additional season-level statistics will be collected using Python (requests, pandas):  
- Points per game  
- Pace (possessions per game)  
- Additional scoring metrics  

**Data Enrichment:**  
The secondary dataset will be merged with the primary dataset by season to enrich the analysis. This allows the project to examine how three-point shooting relates to broader game dynamics such as scoring and pace.

---

### Data Characteristics  

- Unit of analysis: NBA season  
- Estimated size: ~25–30 seasons  
- Features: ~6–8 numerical variables per season  
- Data type: Time-series dataset  

---

### Data Collection & Preparation  

The Kaggle dataset will be directly imported, while additional data will be collected via web scraping from official NBA sources.  

The datasets will then be:  
- cleaned and standardized  
- merged by season  
- structured as a time-series dataset for analysis  

---

### Analysis Plan  

The project will include:  
- Time-series analysis of three-point shooting trends (3PA, 3P%, scoring share)  
- Visualization of long-term trends  
- Hypothesis testing to evaluate statistical significance of changes  
- Correlation and linear regression analysis between three-point shooting and scoring metrics  

Additionally, different time periods (e.g., pre-2010 vs post-2015) will be compared to identify potential structural changes in playing style.
