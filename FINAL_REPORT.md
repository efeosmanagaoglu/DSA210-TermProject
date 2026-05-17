# Final Report

## Evolution of Three-Point Shooting in the NBA

### Research Question

How has three-point shooting evolved in the NBA over time, and does its increase reflect a structural change in overall playing style?

## Motivation

The NBA has experienced one of the clearest strategic transformations in modern team sports. Over time, offensive systems have shifted away from mid-range-heavy play toward spacing, ball movement, and perimeter shooting. The three-point shot sits at the center of that transformation. In the 1990s, it was an important but still relatively limited part of a team’s offense; in the modern league, it has become one of the defining features of how teams create value on the court.

I chose this topic because it captures a visible basketball trend that can also be studied rigorously with data. The question is not only whether three-point attempts increased, but whether that increase reflects a deeper structural change in NBA playing style. If the three-point revolution is truly structural, it should appear in multiple ways:

- long-term upward trends in volume and scoring share
- strong relationships with scoring and pace
- statistically significant differences between earlier and modern eras
- season-level patterns that machine learning models can detect and use predictively

This project is therefore designed to move from description to inference and then to prediction. First, I describe how the game changed over time. Second, I test whether those changes are statistically meaningful. Third, I use machine learning to examine whether the statistical profile of a season is predictive of scoring and distinctive enough to identify a season’s era.

The overall project idea, topic selection, research direction, and general project structure were developed by the student. AI tools were used only in a supportive role during coding, visualization refinement, documentation editing, and consistency checks.

## Data Source

This project combines two public data sources:

1. A Kaggle dataset containing NBA three-point shooting statistics from the 1996-97 season through the 2019-20 season.
2. A Basketball Reference league-level dataset containing season averages such as points per game and pace.

The final processed dataset is stored in [DATA/processed/final_dataset.csv](/Users/efeosmanagaoglu/Desktop/GitHub/DSA210-TermProject/DATA/processed/final_dataset.csv:1) and contains 24 seasons and 7 core variables:

- `Season`
- `3PM`
- `3PA`
- `3P_percent`
- `ThreePointShare`
- `PTS_per_game`
- `Pace`

The raw datasets were cleaned and merged in order to build a single league-level dataset that could support both statistical testing and machine learning.

The preparation steps were:

1. Load the three-point shooting dataset from Excel and the supplementary season averages from CSV.
2. Strip column names and standardize season formatting.
3. Restrict the secondary dataset to the exact seasons covered by the three-point dataset.
4. Keep only the variables directly relevant to the research question.
5. Merge the datasets by season.
6. Sort the final dataset chronologically and export it as a processed CSV.

This approach keeps the project focused on a clearly defined question: whether long-run changes in three-point behavior are connected to broader changes in offensive style.

## Data Analysis

The project was carried out in three stages:

1. Exploratory Data Analysis
2. Hypothesis Testing
3. Machine Learning

### 1. Exploratory Data Analysis

EDA was conducted in [EDA.ipynb](/Users/efeosmanagaoglu/Desktop/GitHub/DSA210-TermProject/EDA.ipynb:1). This stage was used to understand the shape of the data before formal testing. The analysis focused on time-series plots and correlation patterns among three-point volume, three-point efficiency, scoring, and pace.

The main descriptive patterns were:

- Three-point attempts increased from 16.8 per game in 1996-97 to 34.1 per game in 2019-20.
- Three-point scoring share increased from roughly 14% to roughly 33%.
- Three-point percentage stayed near 35%, indicating that the growth in usage did not come with a major drop in efficiency.
- Points per game and pace both increased over time.

The strongest observed correlations were:

- `3PA` vs `PTS_per_game`: `r = 0.9551`
- `3PA` vs `Pace`: `r = 0.9522`
- `3PA` vs `ThreePointShare`: `r = 0.9910`

These findings matter because they show that the three-point trend is not isolated. The rise in `3PA` is occurring alongside faster pace and higher scoring, which supports the idea that the NBA has changed structurally rather than cosmetically.

### 2. Hypothesis Testing

Hypothesis testing was conducted in [Hypothesis_Testing.ipynb](/Users/efeosmanagaoglu/Desktop/GitHub/DSA210-TermProject/Hypothesis_Testing.ipynb:1).

The 24 seasons were split into two equal eras:

- Early era: 1996-97 to 2007-08
- Modern era: 2008-09 to 2019-20

Welch's two-sample t-test was used because the project compares the means of two groups and does not assume equal variances. This is a reasonable choice here because the sample size is small and the two eras are being treated as distinct, non-overlapping periods.

#### Test 1: Three-Point Scoring Share

- Early mean: `16.6040`
- Modern mean: `24.0745`
- t-statistic: `-4.8472`
- p-value: `0.000273`
- Cohen's d: `1.9789`

This result shows that the modern NBA scores a much larger fraction of its points from three-pointers than the earlier NBA. The p-value is far below the usual 0.05 threshold, and the effect size is very large, so the difference is not only statistically significant but also practically meaningful.

#### Test 2: Three-Point Attempts

- Early mean: `15.1024`
- Modern mean: `23.5642`
- t-statistic: `-4.9296`
- p-value: `0.000286`
- Cohen's d: `2.0125`

This confirms that modern NBA teams attempt far more three-pointers per game than earlier teams. The difference is large in absolute terms, large in percentage terms, and accompanied by an extremely large Cohen's d value.

Taken together, the two tests support the same conclusion: the modern NBA differs from the earlier NBA not just in isolated shot counts, but in how much of its offense is built around the three-point line.

### 3. Machine Learning

Machine learning analysis was conducted in [ML_Methods.ipynb](/Users/efeosmanagaoglu/Desktop/GitHub/DSA210-TermProject/ML_Methods.ipynb:1).

Because the dataset contains only 24 observations, the machine learning section was intentionally designed around simple and interpretable models. This is an important methodological choice. On a very small dataset, overly complex models can easily overfit and create misleadingly strong apparent performance. For that reason, the project emphasizes:

- transparent model choices
- regularization where appropriate
- cross-validation rather than single-split evaluation
- interpretability over model complexity

#### Regression Task

Goal:

- Predict `PTS_per_game` using `3PA`, `3P_percent`, `ThreePointShare`, and `Pace`

Models:

- Linear Regression
- Ridge Regression
- Random Forest Regressor

Validation:

- Leave-One-Out Cross-Validation (LOOCV)

Results:

| Model | RMSE | MAE | R² |
|---|---:|---:|---:|
| Ridge Regression | 1.0671 | 0.9212 | 0.9539 |
| Random Forest Regressor | 1.4071 | 1.0927 | 0.9199 |
| Linear Regression | 1.5742 | 1.1111 | 0.8997 |

Ridge Regression performed best. This is an important result because it suggests two things at once. First, league scoring can be predicted quite accurately from the project’s core playing-style variables. Second, a regularized linear model outperforms both plain linear regression and the random forest benchmark, which is consistent with the small size and correlated structure of the dataset.

In practical terms, this means that the rise in scoring is strongly connected to the same strategic variables highlighted earlier in the EDA: pace, three-point volume, efficiency, and scoring share.

#### Classification Task

Goal:

- Classify seasons as `Early` or `Modern`

Features:

- `3PA`
- `3P_percent`
- `ThreePointShare`
- `Pace`
- `PTS_per_game`

Models:

- Logistic Regression
- Decision Tree Classifier
- Random Forest Classifier

Validation:

- Stratified 6-fold cross-validation

Results:

| Model | Accuracy | Precision | Recall | F1 |
|---|---:|---:|---:|---:|
| Decision Tree | 0.8750 | 0.9091 | 0.8333 | 0.8696 |
| Random Forest | 0.8750 | 0.9091 | 0.8333 | 0.8696 |
| Logistic Regression | 0.8333 | 0.9000 | 0.7500 | 0.8182 |

The classification results show that seasons from the two eras can be distinguished reasonably well using only league-level playing-style metrics. This supports the central claim of the project: if a season can be identified as early or modern from its statistical profile alone, then the shift is not just narrative or visual, but measurable in the data.

The interpretive value of the logistic regression model is especially important. Its coefficients show that `3PA` and `ThreePointShare` are among the strongest indicators of the modern era, which aligns directly with both the EDA and the hypothesis testing results.

## Findings

The project provides consistent evidence that NBA three-point shooting reflects a structural change rather than random variation.

The main findings are:

- Three-point attempts more than doubled over the study period.
- The share of scoring coming from three-pointers rose dramatically.
- Three-point percentage remained relatively stable, meaning the change is driven more by shot selection and strategy than by major changes in accuracy.
- Higher three-point volume is strongly associated with both higher scoring and faster pace.
- Hypothesis tests show that differences between early and modern eras are statistically significant with very large effect sizes.
- Machine learning models can predict scoring well and can classify early vs modern seasons with reasonably strong performance.

Taken together, these results support the conclusion that the NBA has undergone a real strategic transformation centered on the three-point shot.

More specifically, the project shows that:

- teams are not merely taking a few more threes; they are reorganizing offense around the three-point line
- scoring has risen alongside this shift, not in contradiction to it
- pace has increased at the same time, suggesting a broader offensive modernization
- machine learning can recover these patterns well enough to both predict scoring and distinguish eras

The strongest overall interpretation is that modern NBA basketball is structurally different from the NBA of the late 1990s and early 2000s, and that the three-point shot is one of the clearest measurable markers of that difference.

## Limitations and Future Work

This project has several limitations:

- The dataset is small, with only 24 league-level observations.
- The analysis is conducted at the league level, not at the team or player level.
- Correlation does not imply causation.
- The early/modern split is imposed manually rather than estimated from a formal breakpoint model.
- The seasons are temporally ordered, which limits the independence assumptions behind some standard statistical and ML procedures.

Possible future extensions include:

- Adding advanced metrics such as offensive rating
- Moving from league-level to team-level analysis
- Testing formal structural break methods
- Expanding the machine learning section with richer historical features

## Project Deliverables and Repository Structure

The repository includes all code and documentation required to reproduce the project:

- [README.md](/Users/efeosmanagaoglu/Desktop/GitHub/DSA210-TermProject/README.md:1), which provides a concise project overview and reproduction steps
- [EDA.ipynb](/Users/efeosmanagaoglu/Desktop/GitHub/DSA210-TermProject/EDA.ipynb:1), which contains the exploratory analysis and visualizations
- [Hypothesis_Testing.ipynb](/Users/efeosmanagaoglu/Desktop/GitHub/DSA210-TermProject/Hypothesis_Testing.ipynb:1), which contains the formal statistical tests
- [ML_Methods.ipynb](/Users/efeosmanagaoglu/Desktop/GitHub/DSA210-TermProject/ML_Methods.ipynb:1), which contains the machine learning phase
- [requirements.txt](/Users/efeosmanagaoglu/Desktop/GitHub/DSA210-TermProject/requirements.txt:1), which lists the required Python packages
- [DATA/processed/final_dataset.csv](/Users/efeosmanagaoglu/Desktop/GitHub/DSA210-TermProject/DATA/processed/final_dataset.csv:1), which stores the final merged dataset used in the analysis

## AI Usage Disclosure

This project used AI assistance during development and documentation.

The overall project idea, topic selection, research direction, and general project structure were developed by the student.

AI tools were used mainly for supportive tasks such as:

- improving and organizing code
- helping generate or refine some code cells
- helping generate or refine some plots and visual outputs
- revising written explanations in the notebooks, README, and final report
- checking consistency between repository files before submission

All AI-supported code, figures, and text were reviewed, edited, and approved by the student before inclusion in the final submission.
