471 Report


## Abstract

There exist many different techniques for predicting the outcome of professional Tennis matches. Using these techniques, it could be possible to gain very large sums of money through sports betting. The fact that Tennis is an individual sport where the professional players each have their own unique playstyle, techniques, strengths, and weaknesses allows models for predicting the outcome of matches to reach a level of accuracy that is better than most humans. In this report, we will implement and evaluate different techniques and models that can be used to predict these professional matches. To help us with this task, [A large 800 MB dataset of over 2 million tennis matches from Kraggle](https://www.kaggle.com/ehallmar/a-large-tennis-dataset-for-atp-and-itf-betting) as well as [ATP tournament results from 2000 to 2017](https://www.kaggle.com/gmadevs/atp-matches-dataset ) will be used in this project.

## Introduction

In 2007, Roger Federer and Rafael Nadal were considered the two best tennis players of all time. Federer was known for his dominance on grass fields, whereas Nadal was undefeated on clay fields. To determine which player was the best, regardless of which field a match was played on, a unique exhibition match was organized around a field built specifically for the occasion that had one side made out of clay, and another side made out of grass. The match was called The Battle of Surfaces.

The reason such a match was even possible, and the reason why there was so much hype surrounding this match, is because Tennis is a sport where each player has a high degree of specialization. Tennis being a mostly individual sport only further emphasizes a player’s specializations, as there are no teammates to cover for a player's weaknesses.

The high specializations of the sport and the high quality of data available makes Tennis an interestings sport to do data analysis on as a way to figure out each player’s strengths and weaknesses, and ultimately predict the winner of a match. There are many factors and attributes about each player, their playstyles and overall skills that can be used to calculate the advantages and disadvantages of a match against another player. Considering the sports betting industry is worth over 203 billion USD, being able to predict the outcome of a match given a set of features could give us an advantage over other betters, which could result in considerable gains for us.

## Materials and Methods

The project will be based on datasets we found on Kaggle. Pulled directly from International Tennis Federation and ATP sources,  the first dataset is made of 7 different .csv files (``all_matches.csv``, ``all_players.csv``, ``all_tournaments.csv``, ``betting_moneyline.csv``, ``betting_spread.csv``, ``betting_totals.csv`` and ``countries.csv``) and is around 800 MB in size which we believe will suffice for the development/tests. Within those 7 files, we have reliable data for over 2000 000 tennis matches along with betting data, data on all the players that were in those matches as well as all the tournaments in which the games were part of. The betting data is composed of 3 distinct components: the Money Line which corresponds to the predicted winner of the match, the Spread which predicts if the difference in games/sets between both players is higher than expected and finally the Totals which predicts if the total games/sets of both players is higher than expected. (Important Note: The tracking of betting data only starts in 2010 and data tracking is not complete prior to 1993.)

The second dataset is composed of 17 individual .csv files from all the ATP tournaments dating from 2000 all the way up to 2017. This dataset offers data on over 50000 tennis matches which includes several interesting tennis data statistics such as the players ranks, age, etc that can be of use to build our prediction models. Although there are quite a bit of  null values within the dataset, it is thankfully large enough so that it won’t hinder our work. 

For this project, we aim to implement and compare two algorithms for predicting the outcome of tennis matches. 

The first of these algorithms is the Markov chain method which was first described in the 2005 paper by Barnett and Clarke. We will be using PySpark to preprocess the data. Once we obtain the values we need, we will feed them to the Markov chain, a recursive Python function, which will give us the predicted outcome of a match. To test the quality of the Markov chain method, we will split the dataset into a training set and a validation set and we will measure the resulting F1-score.

The second algorithm will center around Logistic Regression, a supervised learning classification algorithm. Just like the first algorithm, the paper has hinted on using the following to predict a tennis match outcome. The raw dataset will first get preprocessed using Pandas and Numpy. Afterwards, we will separate the outcomes from the features and feed it to Scikit-Learn implementation of the Logistic Regression. We will produce two Logistic Regressions. The first one will only be using two features: these two features are the rank difference as well as the rank difference in points. The second one will be using multitudes of features all based upon players statistics. To name up a few, we will use a player’s rate of aces, breakpoints, first serve rate, second serve rate, etc. Using Logistic Regression, we will evaluate how accurate each of them are and compare them. To do so, we will compare their accuracy score.  

## Results

### Markov Chain

To measure the quality of the Markov Chain method, we took a subsample of our dataset, split it into a training and a validation set, then measured the resulting F1-Score.

Our validation set consisted of all matches with Roger Federer from 2010 to 2015. Our testing set consisted of all matches with Roger Federer from 2016 onwards.

While we would’ve loved to use all matches, not just the ones featuring Roger Federer, preprocessing the entire dataset was not a realistic goal for us to achieve in the project. While the Markov Chain method is great at predicting the outcome of a single match in a reasonable time, preprocessing a dataset to quickly find the outcome of many matches is very slow. Our very small subsample took over 6 minutes to compute on our workstations.

Here are the results we obtained with our two sets:

| True Positives | False Positives | True Negatives | False Negatives |
|--|--|--|--|
| 80| 13| 0| 0|

These results give us the follow scores:

- **Precision:** 86%
- **Recall:** 76%
- **F1-Score:** 81%

### Logistic Regression
Firstly, for both logistic regressions, we had to load all the 17 individual files from the dataset and combine them together. Afterwards, quite some bit of preprocessing had to be done for it to be adequate for the final dataset.

For the first Logistic Regression, since we are wishing to make predictions by comparing ranks, we had to create  two new columns (rank_difference, rank_difference_in_points) and incorporate them to the dataframe by subtracting ``loser_rank`` to ``winner_rank`` and ``loser_rank_points`` to ``winner_rank_points``. Furthermore, since every match in the dataset was a win (Has a column “winner_name”) , we had to interchange the players in  “winner_name” and “loser_name” with a for-loop in some cases so that the outcomes contain 2 different classes which are necessary for the Logistic Regression.

 Here are the independent/dependent variables for the first LR:
 ![image](https://user-images.githubusercontent.com/47062063/115100857-9b126f80-9f0d-11eb-9110-38a92038b874.png)


Here are the results for the first Logistic Regression: 




For the second Logistic Regression, we had to compute the average of every single player statistic for every single player within the 17 .csv files. Once again, we had to interchange “winner_name” and “loser_name” for similar reasons. (Note: Computing this took around 20 minutes.)

Here are the independent/dependent variables for the second LR: 
![image](https://user-images.githubusercontent.com/47062063/115100867-a8c7f500-9f0d-11eb-997f-790511ba31bb.png)

Here are the results for the second Logistic Regression: 
 


## Discussion

For the Markov Chain method, although our model works and matches the original description of the method from 2005 quite closely, many improvements to the method have been discovered since. Sipko discusses some of these techniques:  Knottenbelt’s Common Opponents averaging, Time Discounting, Surface Weighting, and Uncertainty Measurements. Implementing these techniques would greatly improve our results with the Markov Chain.

For the Logistic Regression algorithm, the results we got were perfectly according to our expectations. Our hypothesis relied on the idea that simply having rank difference for an independent variable will be less accurate than using the average of every tennis player statistic because it isn’t enough to reflect the profile of a player. Simply having a higher number or position doesn’t really explain nor tell how you perform on the field.  It does it’s job rather well. However, the problem resided in it being that having the better rank doesn't necessarily guarantee victory as upsets can happen or else every best player/team in sports would only have undefeated records. As for using the actual statistics of tennis players, the main difference is that it covers all the missing points of the first logistic regression. The average for every tennis statistic does give us a brief overview on how each player performed during his matches as this set of features gives us a reliable way of estimating how he is going to play every game which explains why it’s more accurate. However, this method is not absolute either as it isn’t possible that every single player in the dataset has played the exact same number of games. Therefore, the averages might be inflated for some players depending on how many games they were part of. However, looking at our results, it still represents a rather viable way of predicting the outcome of a match.

For all methods, although our F1-Score is able to prove to us that our implementations are able to accurately predict the outcome of a match, to truly find out if our implementations give us an edge over other betters we would have to measure the **Return On-Investment** of our models, which is unfortunately out of the scope of our project.


## References
[1] Barnett, T., & Clarke, S. R. (2005, April). Combining player statistics to predict outcomes of tennis matches. Retrieved April 05, 2021, from https://www.researchgate.net/profile/Stephen-Clarke-11/publication/228614352_Combining_player_statistics_to_predict_outcomes_of_tennis_matches/links/544007600cf2be1758cff789/Combining-player-statistics-to-predict-outcomes-of-tennis-matches.pdf?origin=publication_detail
[2] Hallmark, E. (2018, August 27). A large Tennis dataset for ATP And itf betting. Retrieved February 19, 2021, from https://www.kaggle.com/ehallmar/a-large-tennis-dataset-for-atp-and-itf-betting
[3] Madurska, A. M. (2012, June 17). A Set-by-Set Analysis Method For Predicting The Outcome Of Professional Singles Tennis Matches. Retrieved April 07, 2021, from https://www.doc.ic.ac.uk/teaching/distinguished-projects/2012/a.madurska%20.pdf
[4] Sipko, M. (2015, June 15). Machine Learning for the Prediction of Professional Tennis Matches. Retrieved April 05, 2021, from https://www.doc.ic.ac.uk/teaching/distinguished-projects/2015/m.sipko.pdf
[5] GMAdevs. (2017, February 07). Association of Tennis Professionals matches. Retrieved April 17, 2021, from https://www.kaggle.com/gmadevs/atp-matches-dataset


