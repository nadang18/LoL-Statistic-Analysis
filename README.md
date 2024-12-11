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
In this section of our research project, we wil aim to analyze and assess the relationship between the number of epic jungle monster objectives secured and their likelyhood of winning a game. Below are our statistics for this permutation test to assess such relationship:

- **Null Hypothesis H<sub>(0)</sub>**: There is no relationship between the number of epic objectives a team secures and their likelihood of winning. The number of epic objectives is unrelated to the game result; observed differences are due to random chance.
- **Alternative Hypothesis H<sub>(1)</sub>**: Teams that secure more epic objectives (dragons, barons, etc.) are more likely to win the game.
- **Test Statistic**: Differences in mean

Running our permutaiton test at a significant level of 5%, we get the following result:
<iframe
  src="assets/fig7.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
With a p-value of 0.0, which is less than our 0.05 threshold, we reject the null hypothesis. Furthermore, we receive an observed statitic of 2.66, thus our data suggests that team that secure more epic objectives (dragons,barons,heralds) are more liekly to win the game.

---

# Framing a Prediction Problem
Since our hypothesis test explored the relationship between epic jungle monsters secured and results of the game, it would make sense for us now to establish a basic prediction model to predict the result of a game given the number of dragons, heralds, and barons secured. To do so, we derive the following dataframe with relevant columns to our prediction:

| teamname          | side   |   gamelength |   kills |   deaths |   assists |   dragons |   heralds |   barons |   firsttower |   visionscore |   earnedgold |   totalgold |   result |
|:------------------|:-------|-------------:|--------:|---------:|----------:|----------:|----------:|---------:|-------------:|--------------:|-------------:|------------:|---------:|
| BoostGate Esports | Blue   |         1446 |      20 |        7 |        47 |         2 |         1 |        1 |            1 |           186 |        36396 |       52523 |        1 |
| Dark Passage      | Red    |         1446 |       7 |       20 |        14 |         1 |         0 |        0 |            0 |           141 |        23655 |       39782 |        0 |
| unknown team      | Blue   |         2122 |      31 |       20 |        60 |         2 |         0 |        1 |            0 |           251 |        49333 |       72355 |        1 |
| unknown team      | Red    |         2122 |      20 |       31 |        23 |         3 |         1 |        1 |            1 |           251 |        43943 |       66965 |        0 |
| unknown team      | Blue   |         2099 |      24 |        8 |        54 |         2 |         1 |        1 |            0 |           261 |        45438 |       68226 |        1 |

Given that we are predicting the result of a game, either win(1) or lost (0), this is considered a classification problem. This means that we will either have to employ our model of decision tree or random forest to build our model. To test how effective our prediction models are we will use accuracy score, along side with f1-score to ensure that our model accurately predict results without any instances of false positive or false negative biases.

With these information in mind, we will first see how well a basic model of a decision tree can do.

---

# Baseline Model
For our baseline model, we will simply implement a decision tree to predict the result of the game on three feature columns: **dragons**, **heralds**, **barons**. Furthermore, to introduce some nuance to our model, we will split the data into a training and a testing set to ensure that we are not underfitting or overfitting our prediction.

We will implement the use of scikit-learn to instantiate a pipeline where we will standardize our three feature columns. This is due to the fact that games can vary in length, thus longer games can lead to higher amounts of epic jungle monster objectives captured.

After running our basic model, we received a **training score** accuracy of 85.72% and a **testinng score** accuracy of 85.46%. This seems relatively good for a basic model, but these accuracy score is not all as we still need to test for the precision, recall, and f1-score to ensure no biases in false positive or false negative cases. Runing those cases, we receive a **precision score** of 81.75%, **recall score** of 91.70%, and a **f1-score** of 86.34%. Considering a basic model, our test shows that the model is relatively decent in predicting the result of match given those three features. This further highlight the importance of securing jungle objectives in a game as they can contribute to much of the gameplay that can truly push for a victory!

---

# Final Model
Although our basic model perform relatively decent, there is still room for improvement as we seek to add more feature columns as well as enhance our decision tree to a random forest classifier. Below we decided to add four more column features we believe directly affect gameplay and potentially the result of the game:

In our final model, we will include 3 more features that directly affect the amount of jungle objectives security:

- **side**: as we have found out in our *bivariate analysis*, depending on which side your team is playing on can affect the amount of heralds and dragons captured

- **kills**: this column is self-explanatory as each kill gives your team a higher number advantage when a fight breaks on when contesting these objectives
  
- **visionscore**: this mark allows team to have more awareness on current activities of the game, namely enemy team's action which allows team to stop enemy from capturing objectives
 
- **earnedgold**: gives us a hollistic view on how well each team is doing as the higher the stronger your team will be with purchases of items that allows you to further contest objectives and in return, gain even more gold.

Furthermore, we will also modify our classifer from a simple decision trea to a random forest classifier to gain better results in terms of accuracy. Furthermore, we will also employ the use of GridSearchCV to find the most optimal hyperparameter as to avoid overfitting. Here we test hyperparameter on three distinct critiria:

- **n_estimator**: the amount of trees we will have in our random forest, ranging from 2 to 100 with step size of 2

- **max_depth**: the depth that each tree will split into, ranging from 2 to 200 with step size of 20

- **criterion**: the criterion in which we determine our model, either gini or entropy

As for transforming our columns, we will binarize the side column as the column contains binary value of *red* or *blue* side. The reamining columns we will standardize as well due to reasoning that longer game can potentially increase the value for all those columns. Preprocessing our data using a column transformer, we now pass it through a pipeline using a random forest classifer. To ensure we are selecting the best hyperparameters, we will run it all through GridSearchCV to predict the data at the best hyperparameters. 

With all said and done, we now run for prediction results and observe that it contains a **training score** accuracy of 100% and a **testing score** accuracy of 88.51%. Similarly, our **precision score** gives us 87.38%, **recall score** of 90.10% and ultimately a **f1-score** of 88.70%. Although we did not significantly improve as our basic model already performs decently well, we still managed to show improvement overall. This implication can be relevant as with some extra steps, we were able to increase our model odds of correctly predicting a game result!

---

# Fairness Analysis
In any data science research project, it is important to question the fairness of one's analysis, testing whether the test applies equally for the different groups we are testing. Aggregating the dataframe shows us an interesting piece of information:

- Total Victories for Blue Side: 4375
- Total Victories for Red Side: 3916

With blue side observing more total victories than red side, could our model be bias towards blue side, in that the outcome disparity between each side lead our model to be unbias. To test it out, we employ the use of fairness analysis.

In our fairness analysis, we picked out two distinct group that our prediction model dealt with when predicting outcome of a game. However, there exist a noticeable difference in wins for blue side over the red side, as we found out in our bivariate analysis, thus we we employ the use of f1-score to balance precision and recall for this test due to the imbalance between distribution of win/lost on each side. Even then our goal is to test the model fairness for both side so we will use a permutation test on f1-score to evaluate our model fairness.

Hypotheses:
- Null Hypothesis (H₀): The model's precision is the same for teams on the Blue side and the Red side. Any observed differences are due to random chance.

- Alternative Hypothesis (Hₐ): The model's precision is different for teams on the Blue side compared to the Red side.

Running the permutation test gives us the following results:
<iframe
  src="assets/fig8.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
With a p value of 0.64, which is greater than the significant threshold of 0.05, we fail to reject the null hypothesis. This implies that our prediction model carries fair f1-score level for both side, meaning there is balance bewteen precision and recall of the model whether you are playing for blue or red side of the game.

