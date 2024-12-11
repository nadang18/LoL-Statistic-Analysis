# League of Legends Results Analysis
League of Legends results analysis is a comprehensive data science project aimed at studying and predicting the relationship between winning and losing odds of a game based on varying factors of the game. The project employs data analysis, inference, and the conclusion of such analysis. Throughout this project, we will aim to assess data frame value missingness, conduct hypothesis testing, and build a prediction model all while evaluating its fairness it. This project employ the uses of Python, along with many modules such as panda, numpy, plotly, scikitlearn, etc.
by: Nathan Dang


# Introduction
League of Legends is a free-to-play MOBA game released in 2009 and published by Riot Games. As of 2024, the game has reached around 180 million active players monthly. With such popularity, the game has multiple different professional tournaments globally where team compete for monetary rewards. This dataset, obtained via download at [oracleselixir]([https://www.example.com](https://oracleselixir.com/tools/downloads)), contains around 1000 recorded professional games from 2024. 

The game centers around a 5v5 MOBA combat system where teams will try to destroy the enemy team's turrets, and eventually nexus (the ultimate end goal of the game). Throughout the game, teams may fight and contest different objectives such as jungle monsters. It is important to note that some jungle monsters may grant permanent and or temporary boosts in team strength that can truly turn the tide of a game; we will denote these monsters as epic jungle monsters. In our research project, we will look to analyze the relationship between victory and loss depending on the amount of epic jungle monsters captured and later on, building a prediction model to predict a team game's result depending on the amount of jungle monsters they have captured.

By using our data analysis technique, we can potentially identify underlying patterns through games and identify potential factors that greatly affect results of a game. Using this information to improve game balance and mechanics to ensure that each and every game feels fair and satisfying to the player base.


## Introduction to Data
The Dataset contains multiple columns denoting game statistics and values, as well as results, however, some games are denoted as incomplete as they are still being recorded through the seasons, thus we will drop those rows of incomplete games. Each row in the dataset would correspond to a specific match. As you may notice, row values can seem identical at a glance, that is due to the fact that League of Legends is a team game, and each five rows marks each player from a team of a professional game, with the sixth row from that being the overall value of the team. For our research, we will filter the data to only contain rows that are representative of a team as we are analyzing the result of a game. Then we will proceed to keep columns that are relevant to our research and drop any columns that may contain redundant information.

- **gameid**: our index for a unique id of each competitive match
- **teamname**: the name of the team competing in the match
- **gamelength**: the length of the game in seconds
- **side**: which side of the map the team plays on, either red or blue
- **result**: the outcome of the game where 1 denotes victory and 0 is lost
- **kills**: the total amount of kills the team achieve on the enemy team
- **deaths**: the total amount of deaths the team accumulated
- **assists**: the total amount of help to secure a kill
- **firstdragon**: value of 1 or 0 on whether a team captured the first dragon spawn
- **dragons**: the total number of dragons a team captured 
- **heralds**: the total number of heraldss a team captured
- **barons**: the total number of barons a team captured
- **visionscore**: the total amount of time a team established vision, spotting an enemy team
- **totalgold**: the total amount of gold earned by a team


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


