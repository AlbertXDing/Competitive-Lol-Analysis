# Project 3 – Competitive League of Legends Match Analysis 📊

# Introduction
### Introduction and Question Identification 

# Cleaning and EDA
### Data Cleaning
### Univariate Analysis
### Bivariate Analysis
### Interesting Aggregates

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


