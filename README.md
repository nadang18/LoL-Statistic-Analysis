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
- **kills**: the total amount of kills the team achieves on the enemy team
- **deaths**: the total amount of deaths the team accumulated
- **assists**: the total amount of help to secure a kill
- **firstdragon**:the  value of 1 or 0 on whether a team captured the first dragon spawn
- **dragons**: the total number of dragons a team captured 
- **heralds**: the total number of heralds a team captured
- **barons**: the total number of barons a team captured
- **visionscore**: the total amount of time a team established vision, spotting an enemy team
- **totalgold**: the total amount of gold earned by a team


---

# Data Cleaning and Exploratory Data Analysis

## Data Cleaning
First, we will query to only keep rows denoting the value of a whole team rather than each individual player. Then we will filter to only keep rows with complete data. Afterward, we will keep columns presented in the introduction as they are relevant to our research. Below are certain changes we made on each column to be more coherent and practical with our research:
- **gameid**: Game Id column will be set as the index to avoid confusion with the original index
- **epic_objectives**: We add a new column containing the row sum of dragons, heralds, and barons captured by each team.

The remaining columns of our data remain unchanged as they are already filtered and cleaned out by the original download of the CSV.

| teamname          |   gamelength | side   |   result |   kills |   deaths |   assists |   firstdragon |   dragons |   heralds |   barons |   visionscore |   totalgold |   epic_objectives |
|:------------------|-------------:|:-------|---------:|--------:|---------:|----------:|--------------:|----------:|----------:|---------:|--------------:|------------:|------------------:|
| BoostGate Esports |         1446 | Blue   |        1 |      20 |        7 |        47 |             1 |         2 |         1 |        1 |           186 |       52523 |                 4 |
| Dark Passage      |         1446 | Red    |        0 |       7 |       20 |        14 |             0 |         1 |         0 |        0 |           141 |       39782 |                 1 |
| unknown team      |         2122 | Blue   |        1 |      31 |       20 |        60 |             0 |         2 |         0 |        1 |           251 |       72355 |                 3 |
| unknown team      |         2122 | Red    |        0 |      20 |       31 |        23 |             1 |         3 |         1 |        1 |           251 |       66965 |                 5 |
| unknown team      |         2099 | Blue   |        1 |      24 |        8 |        54 |             1 |         2 |         1 |        1 |           261 |       68226 |                 4 |


## Univariate Analysis
Below, we perform some univariate analysis, analysis that focuses on one column of our data. Our analysis mainly revolves around details regarding the distribution of each epic jungle monster objectives secured as we hope to analyze its relationship to game results later on.

<iframe
  src="assets/first_uni_dragons.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
> This plot shows the distribution of amount of dragons captured in total. The two columns with the highest distribution are 2 and 3, denoting that it is most common to capture around 2 to 3 dragons per game, highlighting the difficulty of such an objective.

<iframe
  src="assets/first_uni_heralds.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
> This plot shows the distribution of the amount of heralds captured in total. It is interesting to see that the distribution is either 0 or 1, suggesting that only 1 herald monster is spawned to be capturable throughout the course of the entire game.

<iframe
  src="assets/first_uni_barons.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
> This plot shows the distribution of barons captured in total. The decreasing distribution suggests that baron may be the hardest jungle monster to capture by far as most game team fails to capture any baron and the distribution massively decreases at the count of 2, suggesting that this objective is rare and may serve to be crucial for the game.

<iframe
  src="assets/fig2.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
> This box plot represents the statistics of all three epic jungle monsters and their number of captures. From here we can see that there exist at most 7 dragons in a normal duration of a game and 5 barons. This is followed by the median amount of captures for dragon being 2, baron as 1, and herald as 0.

## Bivariate Analysis
Following this, we will perform bivariate analysis, information capturing two columns of data. We will now try and explore an interesting relationship between winning percentage and other factors of the game.

<iframe
  src="assets/fig3.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
> Here we analyze the winning percentage of the game depending on what side of the map your team plays on. There exists a small difference between the red and blue sides where the  blue side exhibits more wins. Could this difference be due to random chance or are there underlying causes  that prove that one side is better? We will shortly explore a multitude of relationships in our research.

<iframe
  src="assets/fig4.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
> In this pie chart we can see that the team that secures the more amount of total epic jungle objectives has an increased winning percentage. This shows that capturing epic jungle monsters shows inherent benefits that greatly pushes the direction of the game.

## Interesting Aggregates
With such interesting information gathered from our graph, we will now perform a basic pivot table to explore the mulitple relationship between these values:
| side   |   dragons |   heralds |   barons |
|:-------|----------:|----------:|---------:|
| Blue   |   2.05446 |  0.610313 | 0.738963 |
| Red    |   2.3752  |  0.381355 | 0.689023 |

> We can see that blue side has a higher average of herald captured compared to red side. Similarly, red side also has a higher average of dragons captured compared to blue side, but no where near as high as the differences in heralds. This begs the question that could blue side exhibit a higher win percentage due to their advantage of being able to capture the herald more easily than red side, which we have analyzed to be important as every epic jungle monster objective contributes to increasing win percentage?

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


