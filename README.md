# Project 3 – Competitive League of Legends Match Analysis 📊

# Introduction
Our dataset consists of information on competitive matches from the tier one league of Legends. The dataset includes relevant columns such as 'league', 'champion', and 'result'. The dataset provides insights into the performance of different champions in competitive matches.The question of our analysis is: "If someone plays Jinx in a competitive League of Legends game in a major region, are they more likely to win?"

Readers of our website should care about this dataset and the question for several reasons, one of them being that Jinx is a popular champion in League of Legends known for her strong late-game damage potential. Our analysis aims to shed light on the effectiveness of Jinx in competitive play specifically in major regions. This information can be useful for professional players, teams, and fans who closely follow the competitive scene and want to gain insights into champion performance trends.

The dataset contains a certain number of rows, but the exact number is not provided in the question. However, the relevant columns for our question are:
1. 'league': Indicates the league in which the competitive match took place.
2. 'champion': Specifies the champion played by a player in the match.
3. 'result': Denotes the outcome of the match, indicating whether the player won or lost.

# Cleaning and EDA
### Data Cleaning
In order to clean the data, we took these following steps: 
1. Remove the summary rows: In this data set, every twelve rows corresponds to one game: ten for each player in the game, and then two for the summary in each team. These rows are not needed for our analysis, so they were filtered and removed from our dataset. 
2. Filter by relevant leagues: In our analysis, we were mainly only intereseted in major leagues, that being the LCK, LEC, LPL, and LCS. Therefore, any games that were not played in those major regions were filtered out and removed from our dataset. 
3. Select relevent columns: After filtering out our data, we only need the columns that are relevant to our query. Therefore, only 'result' and 'champion' are required. 
Our table is as follows: 

| champion   |   result |
|:-----------|---------:|
| Gwen       |        1 |
| Jarvan IV  |        1 |
| Syndra     |        1 |
| Jinx       |        1 |
| Nautilus   |        1 |

### Univariate Analysis

<iframe src="assets/univariate.html" width=800 height=600 frameBorder=0></iframe>

The histogram plot displays the frequency distribution of champions in the dataset, showing the popularity of each champion in competitive matches. It reveals that certain champions are more popular than others, indicating that they are played more frequently. However, no specific trends or patterns are apparent from the histogram, suggesting that champion popularity does not follow a distinct pattern in this dataset.
### Bivariate Analysis

<iframe src="assets/bivariate.html" width=800 height=600 frameBorder=0></iframe>

The scatterplot above visualizes the relationship between the "champion" and "winrate" columns. Each point represents a specific champion and its corresponding winrate.

### Interesting Aggregates


| champion   |   result |   Number of Games |   winrate |
|:-----------|---------:|------------------:|----------:|
| Aatrox     |       52 |               120 |  0.433333 |
| Ahri       |      234 |               461 |  0.507592 |
| Akali      |       97 |               197 |  0.492386 |
| Akshan     |        9 |                18 |  0.5      |
| Alistar    |       56 |               124 |  0.451613 |

Our winrate column is aggregated with the champion, in order to find the amount of games played. This is significant, as our hypothesis question relates to winrates, so we must group by champion in order to find their individual total games played, as well as the total games won in order to calculate the winrate. 

# Assessment of Missingness
### NMAR Analysis
The only column we are using that has missing values is <code>champion</code>. We believe that this is not NMAR, but MD. For every game, there are 12 columns, one for each player and one that analyzes the game. The game analysis can’t have a champion played, so those are missing. The missingness can be determined exactly by looking at other columns, such as ​​participantid. If this column is <code>100</code> or <code>200</code>, the champion column is missing a value. 

None of the columns appear to be NMAR. Most of the columns discuss stats, which are a part of every game and have no reason among itself to be missing. Columns that are not stats have missing values that can be estimated by other columns, but not by the columns themselves. 

### Missingness Dependency 

We tested the missingness of the <code>split</code> column. To do this, we ran a permutation test along with two other columns: <code>datacompleteness</code> and <code>position</code>. We first found the TVD by adding the differences in proportions of when split was and was not missing at each category of <code>datacompleteness</code> . This turned out to be 0.1703. Here is a visualization of the proportions which we found the TVD for: 

<iframe src="assets/league_dist.html" width=800 height=600 frameBorder=0></iframe>

We then shuffled <code>datacompleteness</code> and found the TVD again, and repeated this 500 times. The distribution of the shuffled test statistics can be seen here, where the red line is the observed value: 

<iframe src="assets/datacomplete.html" width=800 height=600 frameBorder=0></iframe>

As the visualization shows, our p-value was 0 as there is nothing greater than the observed statistic. Because this is less than the significance level of 0.05, we reject the null hypothesis. Because we are using a permutation test to judge missingness, the null hypthosis is that the missingness of <code>split</code> does not depend on <code>datacompleteness</code>, and our alternative is that <code>split</code> does depend on <code>datacompleteness</code>. We therefore say that <code>split</code> does depend on <code>datacompleteness</code>, and <code>split</code> is missing at random(MAR).

We can conducted the same test  the <code>position</code> instead of the <code>datacompleteness</code> column, and found that there is <code>split</code> does not depend on <code>position</code>. Here is the visualization for that: 

<iframe src="assets/position.html" width=800 height=600 frameBorder=0></iframe>

# Hypothesis Testing 
Null Hypothesis: Jinx has a 50% chance of winning in major regions

Alternative Hypothesis: Jinx has a greater than 50% chance of winning in major regions. 

Our test statistic is winrate: (games won)/(games played).

Significance Level(alpha): 0.05

After conducting our hypothesis test, we saw that the p-value is 0.11076. Because this is greater than the significance level, we fail to reject the null hypothesis, and conclude that Jinx has a 50% winrate in major regions and does not provide a competitive advangtage. 

Our question was: If someone plays Jinx in a competitive League of Legends game in a major region, are they more likely to win? Our null and alternative hypothesis test effectively answer this question because if a champion wins more than 50%, they are more likely to win(in League of Legends, you either win or you lose). Our test statistic effectively measures the proportion/likelyhood of a champion winning. We also chose our significance level to be 0.05 because that is standard. 


