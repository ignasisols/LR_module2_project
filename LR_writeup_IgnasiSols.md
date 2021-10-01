## Predicting gross worldwide box office revenue for movies produced in the US:

Ignasi Sols 

## Abstract
We have been contacted by a movie producer in the US interested in obtaining a model to predict gross worldwide box office movie revenue. This information is relevant to them because, by having a good estimation of the worldwide box office revenue, they could make an informed decision regarding choosing to release their movie on a streaming service, vs the traditional theater release. I have trained an OLS regression model to answer this question.   

## Design
Linear regression is a good model for predicting gross worldwide box office, albeit not perfect as it can't have negative values. Being able to predict box office revenue as soon as possible after ending shooting the movie might provide a significant edge for movie producers, being able to strike better deals with streaming companies, were they interested in pursuing this kind of release.

## Data
I have web-scrapped 5719 movie pages from IMDb. The inclusion criteria has been: movies between 2015 and 2021, in English, produced in the US and with at least 200 votes on IMDb. 
This data has been filtered again to remove any non-null values in the 'budget' , 'opening weekend' and 'gross worldwide' columns, resulting in a final dataset of 914 movies. The features extracted were multiple: number critics reviews on IMDb, number of user reviews on IMDb, Metacritics score, IMDb rating, number of votes on IMDb, number of Oscar nominations, number of Oscar wins, total number of award wins, total number of award nominations, runtime, MPPA, genre, budget, opening weekend box office revenue in US and Canada, total US & Canada box office revenue, worldwide box office revenue, producer companies and release date. I additionally extracted the director information, top actor, and top writter. I also included information about the top 1000 actors according to an IMDb list. This list was mostly generated in 2014 with few additions over the following years, providing a good snapshot of good actors before 2015. 

## Algorithms
A new feature was added to the dataset, taking two values: '1' if the top actor was in the top 1000 actors list, and '0' if he was not. I also converted the categorical genre feature into 6 dummy variables, choosing the top 5 genres (action, adventure, comedy, crime, drama) and grouping the rest as 'Others'. I also converted the MPPA categorical feature into dummy variables.

*Models*
OLS linear regression was performed. 

*Model Evaluation and Selection*

I first run an OLS model with three predictor variables: 'budget', 'runtime' and 'is_top1000_actor'. Prior to running the model, no collinearity was observed between these features, and 'budget' showed the highest correlation with the target. 

I first trained the OLS model with a simple validation with a 67.66/33.33 train vs. holdout.
The R^2 score for the training set was = 0.609, and the test R^2 = 0.602, indicating little overfitting or underfitting. The adjusted R^2 was = 0.598.
I trained this  OLS model with 5-fold cross-validation on the training portion only, after split into 80/20 train vs. holdout. The mean r^2 was: 0.563, with a small variation: +- 0.039
MAE = $ 94,555,080.57

Next, I tried to improve the model by adding some of the dummy variables that I had generated before: the genre dummy variables 'action', 'adventure', 'comedy', 'crime', 'drama' and the MPPA dummy variables 'G', 'PG-13' and 'R'.
I then fitted the same models as with the baseline model: I first trained the OLS model with a simple validation with a 67.66/33.33 train vs. holdout. The R^2 score for the training set was = 0.62, and the test R^2 = 0.601, indicating a small overfitting. The adjusted R^2 was = 0.594, almost identical to the baseline model.
Next, I trained this OLS model with a 5-fold cross-validation on the training portion only, after split into 80/20 train vs. holdout. I kept the random state the same for the function train_test_split, to use the same split when running the 5-fold cross-validation. The mean r^2 was: 0.559, with a small variation: +- 0.042
MAE = $ 98,442,623.08

The baseline OLS model worked slightly better and, as a consequence that's the model I choose. This model worked poorly, though. When checking residuals visually, it showed a high variance and most negative residuals. 

## Tools
I used BeautifulSoup and Selenium for web-scrapping IMDb movie pages, pandas for data wrangling and exploratory analysis, sklearn for training and evaluating the linear regression models, and Seaborn for plotting.