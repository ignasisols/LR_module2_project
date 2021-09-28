## Predicting movie gross worldwide revenue

The goal of this project is to generate a linear regression model that predicts worldwide movie revenue, such that it can be used by US movie producer companies to better understand what factors predict the success of a movie.

In order to provide such a recommendation, I have web-scrapped 2308 pages of IDMb, one for each movie. The inclusion criteria is movies between 2018 and 2021 with at least 200 votes on IMDb, produced in the US and with English as one of the languages used in the movie. 

I have used BeautifulSoup and Selenium for  web-scrapping IMDb, pandas for data wrangling and exploratory analysis, and sklearn for to perform linear regression. 

The features that I have web-scrapped are release_date,  in which country was initially released, number of user reviews, number of critic reviews, total award wins, total nomination wins, total Oscar wins, production companies, budget, opening weekend box office data in US and Canada, Gross revenue in US & Canada, Gross revenue worldwide, director, top actor, top writer, MPPA, runtime, genre, IMDb rating, number of votes, and metacritic score.

Most movies did not have budget or box office information: Only 369 movies have budget information, and only 691 movies have worldwide revenue. For this reason, I removed all movies that did not have worldwide revenue, ending up with a dataframe of 691 movies to analyse.

For the specific question in hand, I have done a preliminary analysis with the features being budget, opening weekend US & Canada, runtime and number of votes on IMDb (to estimate the impact of the movie on social media. A pairplot:

![plot 1](https://github.com/ignasisols/LR_module2_project/blob/main/pairplot_1.png)

And a  heatmap: 

![plot 1](https://github.com/ignasisols/LR_module2_project/blob/main/pairplot_1.png)

I have dealt with the NaN values in the budget column by replacing them with the average budget across all movies.

I have trained an OLS model with budget,  Gross revenue in US & Canada, and runtime as features, and Gross revenue worldwide as target. I have used the train_test_split function of sklearn,with 25% of data used to validate the model.  The R squared for the model is 0.92, and when scoring with the validation data, the R squared is 0.73 indicating that I am overfitting.

In the next days, I plan to increase the number of movies web-scrapped, and add new features like genre, MPPA (by making dummy variables), and explore regularization of these features, and doing  k-fold cross-validation. 