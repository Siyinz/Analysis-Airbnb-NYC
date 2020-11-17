# Data Analysis: Airbnb in NYC

After being founded in 2008, Airbnb has grown tremendously. Guests and hosts have used it to expand on traveling possibilities and present a more unique, personalized way of experiencing the world. New York City is the third-largest Airbnb market in the world 1, with over 48,800 listings in the year of 2019, which means there are over 40 homes being rented out per square km in NYC on Airbnb. Every time I traveled to other cities, I always tried to find a good (relatively cheap but well-decorated) place to rest via Airbnb, and I was always curious about the supply and demand pattern of the Airbnb market. I would like to know more about the rental landscape in NYC through this analysis. I have not been to NYC before, hopefully I could get some good recommendations on airbnb listings for my next trip.

### Following are a few questions that this analysis aims to answer:
1. Which neighbourhood was the most expensive one in 2019?
2. What was the most popular neighbourhood on airbnb in 2019?
3. What type of room is popular?
4. Find out what features distinguish each neighbourhood and predict which listing is in which neighbourhood using current data.

### Data Source
This dataset describes the listing activity and metrics in NYC, NY for 2019. The dataset was created by Kaggle user Dgomonov ( https://www.kaggle.com/dgomonov/new-york-city-airbnb-open-data ), and this is a public dataset released by Airbnb. The original source can be found here ( http://insideairbnb.com/ ), and it is sourced from publicly available information from the Airbnb site. The data is in csv format, and the latest update date is December 04, 2019. This data contains 16 columns, 48895 unique values. Imported all necessary files and packages, I removed unnecessary data from the data like last_review, name, id, and host name as they do not support the data required. I filled the missing values with zero, and did the visualization using seaborn, pyplot, matplotlib.

### Questions
#### Question one: Which neighbourhood was the most expensive one in 2019?
#### Method:
Before doing the analysis, I noticed that in the original dataset there are a good amount of missing values, and all of them cluster in "reviews_per_month", "last_review", "host_name", and "name". I decided to drop the column "name" and "host_name". Because they are irrelevant and insignificant to our data analysis, and the “host_id” and location information (“longitude” and “latitude”) could provide the same function to identify the hosts and their listings. Besides, for ethical reasons, it might be better to not use real names to do data exploration and analysis. 

I used a simple method to deal with NaN value in "last_review" and "review_per_month". From the table we could know that "last_review" is the date of last review. If there is no review available ("number_of_reviews" column with the value of 0), the "last_review" will be filled with NaN, and the "reviews_per_month" will also be NaN. To deal with the missing value, I decided to drop the column of "last_review", since it is not very relevant and useful. For the missing value in "reviews_per_month", I filled in zero.

In addition, I also dropped the “id” column, since it did not have specific meaning and could not provide extra information. 

Based on that, for the first question where I would like to explore the relations between neighbourhood groups and price, I only selected two columns: “neighbourhood_group” and “price”. 

Firstly, I grouped the data by “neighbourhood_group” and got a describe table. From the describe table, I noticed that there are several extreme price values. In order to get a better visualization, I decided to keep the listings with prices under 600 (firstly tried with 1000, which still contained many extreme values). After removing the extreme values, I used a violin plot to visualize the density and distribution of prices across different neighbourhoods. 

I also used the OLS regression model and ANOVA to see if there are statistically significant differences between the prices in different neighbourhoods. 

#### Analysis and Results:
![img1](https://github.com/Siyinz/Analysis-Airbnb-NYC/blob/main/img/1.png)

According to the violin plot and the summary table above, we could notice that airbnb listings in Manhattan have a relatively high average price with $165 per night. But from the distribution, it seems that the prices for majority listings across different neighborhood groups are all between 50 and 150. Therefore, I used the OLS model to further explore if there are statistically significant differences between the prices in Manhattan and in other neighborhoods.

According to the violin plot and the summary table above, we could notice that airbnb listings in Manhattan have a relatively high average price with $165 per night. But from the distribution, it seems that the prices for majority listings across different neighborhood groups are all between 50 and 150. Therefore, I used the OLS model to further explore if there are statistically significant differences between the prices in Manhattan and in other neighborhoods.

![img2](https://github.com/Siyinz/Analysis-Airbnb-NYC/blob/main/img/2.png)

I used “price” as the dependent variable and neighborhood_group as the independent variable, and the data of Manhattan was used as the reference group to be compared. From the results, the R-squared is very small with the number of 0.028 which means only less than 3% of variance could be explained by the model. 

Compared to the reference group, all four neighborhood groups are statistically significant with the p value of 0, which suggests that there are statistically significant differences between the airbnb prices in Manhattan and in different neighborhoods.

Therefore, from these tables and graphs, I was able to interpret that Manhattan is the most expensive area for Airbnb listings in New York City. It is reasonable, since the house prices and rental prices in Manhattan are also very high. I wish I could incorporate NYC housing or census data into this analysis.

### Question two: What was the most popular neighbourhood on airbnb in 2019?
#### Method:
I dropped “id”, "last_review", "host_name", and "name" columns, and fulfilled the missing value as I did in the first question. In order to have a better sense of the popular level. I removed the listing records with 0 reviews. From the data description table, I noticed that half of the listings only have small amounts of reviews (under 10 reviews), and three quarters listings’ reviews are under 35. Therefore, I defined the popular level by the number of reviews of each listing: low level with number of reviews less or equal to 10; medium level with reviews from 10 to 35; high level with the review number over 35. Then I used scatter plots to show the relations between location and popular level. To further explain the relationship, I also added another scatter plot/heatmap to show the prices across different areas. Finally, I presented a bar chart of the number of listings in each neighbourhood group to provide an alternative explanation to  the popular level. 

#### Analysis and Results:
Airbnb users give reviews to the host according to their experience on the basis of location, cleanliness and other parameters. The data set did not provide rating scores for each listing, but the number of reviews is available. Normally, the better experience the users have, the higher possibility that they are willing to give a review. Even though people may also put an effort in reviews if they have bad experience, generally there will be fewer customers for those airbnb providing bad service, which may lead to fewer reviews. 

Here I worked with the reviews data, and I grouped them into three popular levels: high, medium, and low, according to the number of reviews. Before the analysis, I guessed that the more popular neighbourhoods will tend to have better connectivity (public transportations), and will be closer to the city hotspots (like Times Square, Empire State, Wall Street, etc).

![img3](https://github.com/Siyinz/Analysis-Airbnb-NYC/blob/main/img/3.png)

However, the results we got seem to be different from my original guess. From the map above, we could clearly see that almost no high/medium popular level records in the Manhattan area. It seems like Queens and Bronx are the most popular areas. Considering the answer we got from question one, I wonder whether the high prices will be the reason for low review numbers in the Manhattan area, and even Brooklyn. The following graphs confirmed my thought. Downtown Manhattan is the clear winner when it comes to high prices, as is true for the neighbourhoods of Brooklyn close to Manhattan. 

![img4](https://github.com/Siyinz/Analysis-Airbnb-NYC/blob/main/img/4.png)

Is my original guess wrong? If we consider the popular level by looking at the number of listing records, we will get a different result. There are a greater number of Airbnb listings in Brooklyn and Manhattan compared to other three neighbourhoods, even though they get low number of reviews and their prices are relatively high. One explanation could be: for their commuting and travelling convenience, customers still have a high demand for airbnb listings in Manhattan and Brooklyn. But due to the high housing prices and rental prices in those areas, the price for airbnb listings are high, and customers are likely to only have limited space. In that case, other than the location advantage, customers could hardly think of other positive experiences. Therefore, they might not be willing to leave a review. If there were data of rating score available, it could easily answer the questions. 

![img5](https://github.com/Siyinz/Analysis-Airbnb-NYC/blob/main/img/5.png)

### Question three: What type of room is popular?
#### Method:
I dropped “id”, "last_review", "host_name", and "name" columns, and fulfilled the missing value as I did in the first question. To explore the differences between three room types, firstly I used seaborn countplot to see the number of records for each type of room. Then I use a catplot to see the number of reviews for each room type. Thirdly, I compared the number of records for three room types in different neighbourhood groups, and also used a catplot to see the differences on review numbers. 

#### Analysis and Results:
![img6](https://github.com/Siyinz/Analysis-Airbnb-NYC/blob/main/img/6.png)

From the bar charts above, we could learn that in the airbnb market, the majority of listings are either entire homes/apartments or private rooms. Only a small number of market share are shared rooms. The low number of shared room records could be explained from both demand and supply perspectives, since most people nowadays care about their privacy and would appreciate a private space to rest, not only for customers but for hosts as well. And you have to pay higher prices for the privacy you want. In other words, the prices for private rooms and entire homes/apartments is much higher than the prices for shared rooms. 

![img7](https://github.com/Siyinz/Analysis-Airbnb-NYC/blob/main/img/7.png)

If we looked into room types across different neighbourhood groups, the answer could be slightly different. Like the data for the whole NYC, the shared room has the least amount of records in all the neighbourhood groups. In Brooklyn, the number of private rooms is a bit higher than the number of entire homes. It is the same as other areas like Queens, Staten Island, and Bronx, although the entire number of listings in those areas are pretty low, compared to Brooklyn. However, the data for Manhattan is different. The number of entire homes and apartments is greatly higher than private rooms, not to mention shared rooms. I actually could not find a good explanation for that. From the demand side, is that because private rooms in Manhattan are pretty small so that customers prefer the entire home/apt to get more space? From the demand side, is that because the hosts find the living expenses in Manhattan is too high, so they would live in a relatively cheap place like the Bronx, and then rent their homes for extra money? Hopefully a new yorker could give us some insights.  

### Question four: Find out what features distinguish each neighbourhood and predict which listing is in which neighbourhood using current data.
#### Method: 
I dropped “id”, "last_review", "host_name", and "name" columns, and fulfilled the missing value as I did in the first question. Then I used a pairplot to explore the relationship between 'price', 'minimum_nights', 'number_of_reviews', 'availability_365', where I color-coded by different neighbourhood groups.

Secondly, I made a random forest model and tried to predict which listing is in which neighbourhood group using current data. In order to make the model, I dropped 'neighbourhood', 'host_id', 'longitude', and 'latitude', since 'host_id' is irrelevant, and columns like 'neighbourhood', 'longitude', and 'latitude' are highly connected to ‘neighbourhood_group’. That's to say, if you know either the information of ‘neighbourhood’ or the location information, you could identify which neighbourhood group the listing locates. 
After dropping those columns, I used Label Encoder to convert those variables with string value, as sklearn is not able to process non-numeric data. Then, I splitted the complete dataset into training and testing datasets by 70% and 30%, which enabled me to build a random forest classifier to predict the neighbourhood group variable.

Finally, I used a bar chart to show the most important features in the model. 

#### Analysis and Results:
![img8](https://github.com/Siyinz/Analysis-Airbnb-NYC/blob/main/img/8.png)

From the pairplot above, we could confirm some answers we got in the previous questions. Like Manhattan is the most expensive area in NYC and Bronx is the cheapest place to live in NYC; Queens and Bronx got higher review numbers compared to Manhattan and Brooklyn. We could also know from the plots that the minimum nights to stay in the Bronx is shorter than that in other areas. For availability, airbnb listings in Manhattan and Brooklyn are likely to have short periods available to rent while listings in other places tend to be longer. 

![img9](https://github.com/Siyinz/Analysis-Airbnb-NYC/blob/main/img/9.png)

After experimenting with k-folds and max-depth using cross-validator for my Random Forest classifiers, I used max-depth of 9 and n_estimators of 15. With Random Forest classifiers, I was able to predict the neighbourhood group at an accuracy of 59.09%. It is not that accurate because we only have a limited amount of features. The important features that affected the predictions were price and calculated_host_listings_count. From the analysis above, we could understand how prices distinguish different areas. But in this report, I paid little attention to the number of listings each host owns. We might get some insights on hosts’ socioeconomic status across different areas. It may also be able to give an explanation on why from the supply side, the entire home/apartment type is more popular in Manhattan than other areas.  
