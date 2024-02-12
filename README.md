# Final-Project-Statistical-Modelling-with-Python

## Project/Goals
This project takes data from three APIs (CityBikes, FourSquare Places, and Yelp Fusion) and combines them to analyze the dependence of rental bike availability on nearby businesses and landmarks in Tokyo, Japan.

## Process
### Data Acquisition and Exploratory Data Analysis
The [city_bikes.ipynb](./notebooks/city_bikes.ipynb), [yelp_foursquare_EDA.ipynb](./notebooks/yelp_foursquare_EDA.ipynb), and [joining_data.ipynb](./notebooks/joining_data.ipynb) detail my data acquisition and EDA process. 

In summary, I obtained all of the rental bike info for Tokyo, Japan from the the CityBikes API over an ~8 hour period. I then looked for businesses and landmarks within ~1000m of the stations using both the Yelp Fusion and Foursquare Places APIs, with a focus on categories that I thought were likely to affect bike usage in the area. I combined this data together and placed it in a sqlite database ([yelp_foursquare_EDA.ipynb](./data/Docomo_stations.db)), which I used in my model building step.

The exploratory data analysis consisted of plotting the Docomo Cycle Stations on a [map of Tokyo](./images/underwater_bikes.png). This returned a surprising amount of underwater rental bicycle stations, which is something I should probably look into in future analyses. I also compared the data returned by both the Foursquare Places and Yelp Fusion APIs, and found that the Foursquare Places data, while more sparse than the data provided by Yelp Fusion, was more appropriate for the analysis that I would be carrying out. Lastly, I plotted a correlation matrix between various characteristics of the Docomo stations and the number of nearby places that fit into various categories (restaurants, bars, landmarks/parks, and convenience stores). This initial correlation matrix showed little to no correlation between different features in the collected data.

### Model Building

I created both linear and logistic regression models, detailed in [this notebook](./notebooks/model_building.ipynb). Neither fared particularly well.

## Results
Even after cleaning the data and dropping unhelpful features, the best (fair) linear regression I could achieve had an adj. R-squared of 0.068. Using similar data but converting free_bikes to a Boolean indicating if any bikes were available, the logistic regression model predicted that all data was equal to the value that was most common in the dataset (True). This indicates that the other features had little to no predictive significance.

The lack of success of these two models indicates to me that more data should be collected, both from the initial APIs and from different sources.

## Challenges 
Throughout the data acquisition and modelling process, I felt that I needed a great deal more data to determine any relationships and build reliable models. One issue was that, due to the short timeline of the project, I only had an opportunity to collect data 12 times from CityBikes during the period of 08:15:04 and 15:42:03 Tokyo (JST) on 2024-02-08. If the availability of bikes is time-dependent, this simply is not enough data to determine that. This is also, in my mind, the most important feature to examine, as it could also increase the relevance of certain features that did not appear to have any effect on my current models. For example, the number of nearby bars was determined to not be relevant in the logistic regression, but it might have been if data was collected later in the evening. It is also possible that the total utilization across all Docomo Cycle Stations is much higher on the weekends, and no data was collected during that period.

The other, more over-arching challenge to this analysis is that rental bicycle usage is, to an extent, a dependent on the movement of people within the cities. Bicycles do not necessarily need to be returned to the same station that they were taken from, and this is not reflected in an analysis of places that are only within a very short cycling distance of the initial station. My initial goal in the data acquistion process was to leverage the data available at [Public Transportation Open Data Center](https://developer.odpt.org/en/users/sign_up) and utilized in the [Mini Tokyo 3D](https://minitokyo3d.com/) to incorporate trends involving mass human movement. However, I have not been able to gain access to this data as of yet.

## Future Goals
As stated above, I would like to collect data from CityBikes over a much longer timeframe. In addition, I want to incorporate data from more sources, most importantly the [Public Transportation Open Data Center](https://developer.odpt.org/en/users/sign_up). I think that my models can be drastically improved by the inclusion of more, and more relevant, data.

