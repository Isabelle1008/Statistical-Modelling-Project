# Final-Project-Statistical-Modelling-with-Python

## Project/Goals
This project fetches real-time data of bike stations from the Bicing API.
 This data provides information on bike stations, it extracts key details such as the station's name, latitude, longitude, and the number of free bikes available at each station. This data was then converted into a structured Pandas Data Frame, which can be further analyzed or used for predictions or reports. 
The data from Yelp API was also fetched and it provides nearby restaurant information.
A single comprehensive Data Frame containing bike station data and Yelp data predicted bike availability at different stations. 
It allows analysis of the relationship between bike station availability and nearby restaurants, which can be useful for providing recommendations, insights, or building predictive models.
 The data will be used for classification tasks such as predicting the availability of bikes at the stations based on nearby restaurant data and other features.
A regression model was built to predict the number of free bikes available at bike stations based on various restaurant-related features. The goal was to determine how factors like restaurant ratings, review count, and proximity (distance) affect bike availability at nearby stations.
A classification model was built 
The goal was to predict bike availability at various stations using a classification model. Incorporation of external data from Yelp about nearby restaurants enriches the prediction process and identifies any patterns that might influence bike availability. This can help users find stations with better bike availability, potentially near highly rated restaurants or places with high foot traffic.


## Process
### With city_bikes data
 Request Data from the Bicing API: 
 The code first sends a GET request to the Bicing API to retrieve real-time bike station data. The data contains information about the stations, including the station name, location, and number of free bikes.

 Parse the JSON Response:
Once the data is successfully retrieved, the response is parsed from JSON format. The stations key from the API response contains all the information about the available bike stations.

Process and Store the Data
The code then processes each station's data and stores it in a list of dictionaries. Each dictionary corresponds to one bike station. This list is then used to create a Pandas DataFrame.
Display the DataFrame:
 the DataFrame with the parsed bike station data is displayed.
 
 ### with Yelp_foursquare data
 Fetch Yelp Data for Nearby Restaurants:
For each bike station, we query the Yelp API to find nearby restaurants within a 1000-meter radius. This is done for each bike station by using its latitude and longitude as search parameters. We filter the results to include only restaurants and collect information like name, category, latitude, longitude, rating, review count, and distance from the bike station.
Combine Yelp Data with Bike Station Data:
Once the Yelp data for nearby restaurants is collected, we combine it with the bike station data. We use the station column as the key to merge the two datasets.

comparison of both datasets
understanding how nearby businesses might influence bike availability, Yelp provides better coverage in terms of:
Volume of results
Granular details (e.g., ratings, reviews)
Business classification and category labeling

Yelp’s strength lies in user-generated data such as star ratings and reviews, which were critical features in our machine learning model.
 Foursquare, while useful for broader POI detection, offered fewer results and less data depth for each business.

Yelp is more suitable for data-rich projects involving consumer behavior, business popularity, or machine learning models that rely on ratings and reviews.
 Foursquare may still be useful for broader POI discovery, especially in less commercially dense areas or when you need consistent global data.


### joining _data
The pd.merge() function from the Pandas library was used to combine two DataFrames: yelp_df (restaurants data) and bike_df (bike station data). This is done based on a common column: station, which represents the bike station name in both datasets.
This allows performing exploratory data analysis (EDA) to find trends, such as bike stations with high or low availability near popular restaurants.
Building models to predict bike availability based on nearby restaurant characteristics.
Using the dataset to create location-based recommendations or insights for bike station planners or restaurant owners.


### model_building
The original dataset contained information about both bike stations and nearby restaurants.  Focus was on:
Restaurant features: rating, review_count, distance_m, and restaurant category (encoded into dummy variables).
Target variable: free_bikes, representing the number of available bikes at a given station.
transform categorical restaurant categories into numerical features using one-hot encoding by using Pandas' get_dummies() function.

 select the features used to predict bike availability (free_bikes). These include:
•	Numerical features: rating, review_count, distance_m.
•	Categorical features: One-hot encoded restaurant categories.
We separate the features (X) and the target variable (y):

X = df_model[features]
y = df_model['free_bikes']
Then, we add a constant term (intercept) to the model using sm.add_constant():
X = sm.add_constant(X)
fit an OLS regression model using statsmodels:
model = sm.OLS(y, X).fit()
Finally, we display the model summary, which provides statistical information about the regression:

## Results
The output of the OLS regression model includes the following key metrics:
Coefficients: The estimated impact of each feature on bike availability.
p-values: Statistical significance of each feature. Features with a p-value less than 0.05 are considered statistically significant.
This model helps understand how various restaurant-related factors (such as rating, review count, and proximity) influence bike station availability. By interpreting the coefficients and statistical significance of the features, informed decisions can be made about where to place more bike stations or how to improve bike availability near popular restaurants.

## Challenges 
API Rate Limits: The Yelp API had rate limits that needed to be managed. A time.sleep() function is used to pause the requests and avoid exceeding the limit.
Data Matching: Some bike stations did not have any nearby restaurants, which created gaps in the dataset.
## Future Goals
Include other relevant features such as weather conditions, or population density. 
Incorporate time-based data (e.g., bike availability at different times of day) to improve predictions.
