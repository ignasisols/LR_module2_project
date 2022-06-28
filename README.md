# Predicting gross worldwide box office revenue for movies produced in the US:

  Ignasi Sols 

## Abstract

  I was interested in this project because my brother has worked in movies as a cinematographer, and one of my relatives was a popular cinema director back in Spain.The aim of the project was to predict gross-worldwide revenue with a linear regression model. This model could be used by movie producers when deciding between releasing their movie on theaters or on streaming services. 
  
The jupyter notebook web_scrapping_IMDb.ipynb contains all the code used for web-scrapping IMDb, and the notebook Linear_regression_modeling.ipynb contains all the linear regression modeling. 

## Design

  Linear regression is a good model for predicting gross worldwide box office, albeit not perfect as it can't have negative values. Being able to predict box office revenue as soon as possible after ending shooting the movie might provide a significant edge for movie producers, being able to strike better deals with streaming companies, were they interested in pursuing this kind of release.

## Data

  I have web-scrapped 5719 movie pages from IMDb. The inclusion criteria has been: movies between 2015 and 2021, in English, produced in the US and with at least 200 votes on IMDb. 
  This data has been filtered again to remove any non-null values in the 'budget' , 'opening weekend' and 'gross worldwide' columns, resulting in a final dataset of 914 movies. The features extracted were multiple: number critics reviews on IMDb, number of user reviews on IMDb, Metacritics score, IMDb rating, number of votes on IMDb, number of Oscar nominations, number of Oscar wins, total number of award wins, total number of award nominations, runtime, MPPA, genre, budget, opening weekend box office revenue in US and Canada, total US & Canada box office revenue, worldwide box office revenue, producer companies and release date. I additionally extracted the director information, top actor, and top writter. I also included information about the top 1000 actors according to an IMDb list. This list was mostly generated in 2014 with few additions over the following years, providing a good snapshot of good actors before 2015. 

## Feature Engineering:

 A new feature was added to the dataset, taking two values: '1' if the top actor was in the top 1000 actors list, and '0' if he was not. I also converted the categorical genre feature into 6 dummy variables, choosing the top 5 genres (action, adventure, comedy, crime, drama) and grouping the rest as 'Others'. I also converted the MPPA categorical feature into dummy variables.

I also created a new variable with the month in which the movie was released, and made dummy variables. I also converted the production companies feature into dummy variables, labeling as 'Other' those production companies that produced fewer than 4% of the movies in this dataset. 

I also did several feature transformations: I squared the budget, and I also computed the logarithm of the budget. In addition, I transformed the target variable: first I tried its log transformation, and then a box-cox transformation. The aim of these transformations was to meet the linear regression assumptions that were violated otherwise.


## Algorithms

I first set a 10-fold cross-validation scheme, and a 80/20 training/test scheme, which I used during the whole analyses. 

I trained a baseline OLS model with the two numerical features available: budget and runtime. Then, I improved this model by trying different features, including transformations of the budget feature (quadratic and logarithmic transformations). Given that the linear regression assumptions were always broken (in particular, the residuals were not normally distributed and their variance was not constant), I proceeded to try different target feature transformations. The one that had the best effect in terms of solving the broken assumptions was the box-cox transformation. Then, the logarithm of the budget feature was the one providing better results in terms of the adjusted R^2 and the MAE. 

Lasso and Ridge regularization was implemented for all these models, via the scikit-learn methods LassoCV and RidgeCV. A wide range of lambda values was tested. 

The best performing model was a Ridge model:

- Lambda = 4.422. 

- R^2 = 0.667
- Adjusted R^2 = 0.633
- Overall MAE = $ 86.98M
- MAE for movies with a predicted revenue of less than 250M dollars = $39.8M
- MAE for movies with a predicted revenue between 250M and 1B dollars = $213.8M
- MAE for movies with a predicted revenue larger than 1B dollars = $805M

Therefore, this model might be more useful for movies with a smaller budget. 

## Tools

I used BeautifulSoup and Selenium for web-scrapping IMDb movie pages, pandas for data wrangling and exploratory analysis, sklearn for training and evaluating the linear regression models, and Seaborn for plotting.
