# League of Legends Results Analysis
League of Legends results analysis is a comprehensive data science project aimed at studying and predicting the relationship between winning and losing odds of a game based on varying factors of the game. The project employs data analysis, inference, and the conclusion of such analysis.


# Introduction
In this data science research, we will ......

---

# Data Cleaning and Exploratory Data Analysis

## Data Cleaning
| teamname          |   gamelength | side   |   result |   kills |   deaths |   assists |   firstdragon |   dragons |   heralds |   barons |   golddiffat10 |   golddiffat15 |   golddiffat20 |   golddiffat25 |   epic_objectives |
|:------------------|-------------:|:-------|---------:|--------:|---------:|----------:|--------------:|----------:|----------:|---------:|---------------:|---------------:|---------------:|---------------:|------------------:|
| BoostGate Esports |         1446 | Blue   |        1 |      20 |        7 |        47 |             1 |         2 |         1 |        1 |           1364 |           2293 |           4248 |          12741 |                 4 |
| Dark Passage      |         1446 | Red    |        0 |       7 |       20 |        14 |             0 |         1 |         0 |        0 |          -1364 |          -2293 |          -4248 |         -12741 |                 1 |
| unknown team      |         2122 | Blue   |        1 |      31 |       20 |        60 |             0 |         2 |         0 |        1 |            -88 |            -75 |            777 |           1459 |                 3 |
| unknown team      |         2122 | Red    |        0 |      20 |       31 |        23 |             1 |         3 |         1 |        1 |             88 |             75 |           -777 |          -1459 |                 5 |
| unknown team      |         2099 | Blue   |        1 |      24 |        8 |        54 |             1 |         2 |         1 |        1 |          -2583 |           -561 |          -1528 |           1092 |                 4 |

## Univariate Analysis
<iframe
  src="assets/first_uni_dragons.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<iframe
  src="assets/first_uni_heralds.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<iframe
  src="assets/first_uni_barons.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<iframe
  src="assets/fig2.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

## Bivariate Analysis
<iframe
  src="assets/fig3.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<iframe
  src="assets/fig4.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

## Interesting Aggregates
<iframe src="assets/interest_agg.html" width="600" height="300" frameborder="0" style="border: none; transform: scale(1.5); transform-origin: top left;"></iframe>

Attached is our pivot table where we aggregated the average number of dragons, heralds, and barons captured per team side.

---

# Assessment of Missingness

---

# Hypothesis Testing

---

# Framing a Prediction Problem

---

# Baseline Model

---

# Final Model

---

# Fairness Analysis


