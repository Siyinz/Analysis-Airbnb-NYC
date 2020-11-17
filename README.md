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

According to the violin plot and the summary table above, we could notice that airbnb listings in Manhattan have a relatively high average price with $165 per night. But from the distribution, it seems that the prices for majority listings across different neighborhood groups are all between 50 and 150. Therefore, I used the OLS model to further explore if there are statistically significant differences between the prices in Manhattan and in other neighborhoods.


