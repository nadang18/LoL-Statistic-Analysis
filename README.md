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
| Blue   |   2.05446 |   0.61031 |   0.73896 |
| Red    |   2.37520 |   0.38135 |   0.68902 |

> We can see that blue side has a higher average of herald captured compared to red side. Similarly, red side also has a higher average of dragons captured compared to blue side, but no where near as high as the differences in heralds. This begs the question that could blue side exhibit a higher win percentage due to their advantage of being able to capture the herald more easily than red side, which we have analyzed to be important as every epic jungle monster objective contributes to increasing win percentage?

---

# Assessment of Missingness

## NMAR (Not Missing at Random) Analysis
From our dataframe, we believe that columns of bans: **ban1**, **ban2**, **ban3**, **ban4**, **ban5** are best explained as being dependent on itself. In league of legends, banning is an optional mechanic in which a player can rid a character out of the character pool, thus making it impossible for anyone to play as that champion. Thus the missingness of the different ban columns are best explained as NMAR as a player may choose to not ban anyone, thus its missingness is dependent on itself.

## MAR (Missing at Random) Analysis
Other than our NMAR analysis, we will now try to examine other columns that contains missing values and see if we can attribute their missingness dependency upon other columns (proving if MAR holds).

First we analyze the missingness of the column **goldat25** and see if its missingness is dependent of other columns. To do so, we will perform a permutation test with a significant threshold of 5% and with the following test hypotheses:
- Null Hypothesis H<sub>(0)</sub>: The missingness of the goldat25 column is independent of the game length (MAR fails).
- Alternative Hypothesis H<sub>(1)</sub>: The missingness of the goldat25 column depends on the game length (MAR holds).
Below is our table of missingness where we will perform permutation on the **goldat25_nan** to test our hypothesis:

|   gamelength |   goldat25 | goldat25_nan   |
|-------------:|-----------:|:---------------|
|         1446 |      52523 | False          |
|         1446 |      39782 | False          |
|         2122 |      45691 | False          |
|         2122 |      44232 | False          |
|         2099 |      43051 | False          |

Performing our permutation test, we get the following result:
<iframe
  src="assets/fig5.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
> Here we observe a p-value of 0.0, which is less than the 0.05 threshold, thus we reject the null hypothesis.
Our test shows an **observed statistic** of 578.40, and from there we see almost no intances where our test displays such instances. Thus with a **p-value** of 0.0, which is less than our significant threshold, we reject the null hypothesis. This then suggests that the missingness of **goldat25** is not independent of game length, thus MAR holds.


Secondly, we will analyze the missingness of the **split** columna nd see if its missingnes is dependent of other columns. To do so, we will similarly conduct a permutation test with the following test hypotheses:
- Null Hypothesis H<sub>(0)</sub>: The missingness of split is independent of the side of map (MAR fails).
- Alternative Hypothesis H<sub>(1)</sub>: The missingness of split depends on the side of map (MAR holds).
Below is our table of missingness where we will perform permutation on the **split_nan** to test our hypothesis:

| side   | split   | split_nan   |
|:-------|:--------|:------------|
| Blue   | Winter  | False       |
| Red    | Winter  | False       |
| Blue   | Winter  | False       |
| Red    | Winter  | False       |
| Blue   | Winter  | False       |

Performing our permutation test, we get the following result:
<iframe
  src="assets/fig6.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
> Here we observe a p-value of 0.982, which is greater than the 0.05 threshold, thus we fail to reject the null hypothesis.
Our test shows us that our observed TVD is well within our range of generated TVD, meaning that the distribution between two group is not statistically significant. Thus with a **p-value** of 0.982, which is greater than our significant threhold, we fail to reject the null hypothesis. This then suggests that the missingness of **split** is independent of side, thus MAR fails.

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


