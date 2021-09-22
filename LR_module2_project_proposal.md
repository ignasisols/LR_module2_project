#### Question/need:  
- **What is the framing question of your analysis, or the purpose of the model/system you plan to build?**
The purpose of this analysis is to develop a linear regression model that best predicts box office movie profit.


#### Data Description:
- **What dataset(s) do you plan to use, and how will you obtain the data?**
I plan to obtain most of the data from IMDb (or, alternatively, Box Office Mojo), by doing web scrapping with Beautiful Soup and Selenium. This data will provide information for fields like movie budget and revenue. I plan to add a measure of how good are the actors of each movie. I plan to add this information from websites like ranked.com, or IMDb pro if it was possible to scrap the data. I plan to use data from 2018,2019 movies and 2020,2021 movies to be able to investigate any change between the best predictors pre-and post- covid-19.

- **What is an individual sample/unit of analysis in this project? What characteristics/features do you expect to work with?**
The individual sample/unit of analysis in this project will be a given movie. I plan to scrap data from the top 500 movies of 2018, 2019, and 2021 - a total of 1500 movies  (but this should be discussed given that there would be a different number of movies pre-and post- covid). I am planning to work with features as genre, budget, production companies, runtime, number of reviews, number of awards, number of user reviews, number of critic reviews, Metascore, scores for the quality of the actors and, if possible, scores for directors and screen writers. 

#### Tools:
- **How do you intend to meet the tools requirement of the project?**
I plan to use beautiful soup and selenium for web scrapping, pandas for data wrangling and EDA, sklearn for linear regression, and matplotlib and seaborn for plotting. 

- **Are you planning in advance to need or use additional tools beyond those required?**
I am not planning to use additional tools beyond those required.


#### MVP Goal:
- **What would a [minimum viable product (MVP)] look like for this project?**
To be able to develop a linear regression model that predicts well the profit for a given movie.