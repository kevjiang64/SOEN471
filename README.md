# SOEN471: Big Data

## Abstract

Tennis is interesting because it is an individual sport where the professional players each have their own unique playstyle, techniques, strengths, and weaknesses. Federer is known for his dominance on grass fields, whereas Nadal dominates clay fields. Match data such as the terrain type, the ability to deliver and handle serves, tiebreaks and matchups could be used to obtain valuable statistics about each player's strengths and weaknesses. [A large 800 MB dataset of over 2 million tennis matches from Kraggle](https://www.kaggle.com/ehallmar/a-large-tennis-dataset-for-atp-and-itf-betting) will be used in this project.

## Introduction

In 2007, Roger Federer and Rafael Nadal were considered the two best tennis players of all time. Federer was known for his dominance on grass fields, whereas Nadal was undefeated on clay fields. To determine which player was the best, regardless of which field a match was played on, a unique exhibition match was organized around a field built specifically for the occasion that had one side made out of clay, and another side made out of grass. The match was called The Battle of Surfaces.

The reason such a match was even possible, and the reason why there was so much hype surrounding this match, is because Tennis is a sport where each player has a high degree of specialization. Tennis being a mostly individual sport only further emphasizes a player’s specializations, as there are no teammates to cover for a player's weaknesses.

The high specializations of Tennis and the high quality data available makes it an interestings sport to do data analysis on as a way to figure out each player’s strengths and weaknesses. There are many factors and attributes about each player, their playstyles and overall skills that can be used to calculate the advantages and disadvantages of a match against another player. Being an individual sport, it should be very easy to narrow down an analysis to specific players, something which can’t be done on a team-based sport. Furthermore, analyzing players one at a time would give much more accurate results than analysing an entire sports team, where there are too many variables to take into account, and where different players join and leave the team every year which can dramatically change how a team plays from one year to the next.

## Materials and Methods

The project will be based on a dataset we found on Kaggle. Pulled directly from International Tennis Federation and ATP sources,  it is made of 7 different .csv files (all_matches.csv, all_players.csv, all_tournaments.csv, betting_moneyline.csv, betting_spread.csv, betting_totals.csv and countries.csv) and is around 800 MB in size which we believe will suffice for the development/tests. Within those 7 files, we have reliable data for over 2000 000 tennis matches along with betting data, data on all the players that were in those matches as well as all the tournaments in which the games were part of. The betting data is composed of 3 distinct components: the Money Line which corresponds to the predicted winner of the match, the Spread which predicts if the difference in games/sets between both players is higher than expected and finally the Totals which predicts if the total games/sets of both players is higher than expected. (Important Note: The tracking of betting data only starts in 2010 and data tracking is not complete prior to 1993.)

For the technologies, the plan is to utilize the programming tools we have skimmed through in class such as PySpark, Dask and new ones like Scikit-Learn and Tensorflow. Both Scikit-Learn and TensorFlow seem to be very promising technologies as they possess some components that we definitely want to incorporate to deal with the dataset. As our knowledge regarding Big Data technologies is still rather minimal, this list might change and get updated as we progress in our project and get more insight on other tools that might come in handy for us.. 

For algorithms, we mainly plan on using classification/clustering techniques to compare on how precise and accurate each algorithm is when it comes to identifying a player’s skills. For Classification, we will incorporate methods such as Decision Trees and Random Forests to categorize all the players in the dataset based on their skills. For clustering, algorithms such as K-Means and Centroid-based clustering all seem doable with the data that we have. We will be able to accomplish the work as the dataset possesses statistics on how points were won in a match by any player. 

## References

Barnett, T., &amp; Clarke, S. R. (2005, April). Combining player statistics to predict outcomes of tennis matches. Retrieved April 05, 2021, from https://www.researchgate.net/profile/Stephen-Clarke-11/publication/228614352_Combining_player_statistics_to_predict_outcomes_of_tennis_matches/links/544007600cf2be1758cff789/Combining-player-statistics-to-predict-outcomes-of-tennis-matches.pdf?origin=publication_detail

Hallmark, E. (2018, August 27). A large Tennis dataset for ATP And itf betting. Retrieved February 19, 2021, from https://www.kaggle.com/ehallmar/a-large-tennis-dataset-for-atp-and-itf-betting

Sipko, M. (2015, June 15). Machine Learning for the Prediction of Professional Tennis Matches. Retrieved April 05, 2021, from https://www.doc.ic.ac.uk/teaching/distinguished-projects/2015/m.sipko.pdf

