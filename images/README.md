# Creating-the-Best-Airbnb-in-Seattle
[interactive visualization tool](https://public.tableau.com/app/profile/nahyy4315/viz/CuratingthebestairbnbinSeattle/Geospatialanalysis)
(please hover over the parts of the viz which might not be displaying properly due to versioning incompatibilities)

## Contents Page

- [Introduction](#introduction)
  - [Data](#data)
- [Neighbourhood Analysis](#Neighbourhood-Analysis)
  - [Dashboard Demo](#Dashboard-Demo)
  - Dashboard details & analysis into:
    - Most influential factor impacting price
    - Relationship between most influential factor and price

- [Geospatial Analysis](#Geospatial-Analysis)
  - [Dashboard Demo]()
  - Dashboard details & analysis into:
    - Neighbourhoods ranked based on price, rating and popularity metrics in foursquare
    - Dissapointing listings in Neighbourhoods
          
- [Competitor Analysis](#Competitor-Analysis)
  - [Dashboard Demo](#Dashboard-Demo)
  - Dashboard details & analysis into:
    - Relationship between age and listing prices with ACF
    - Relationship between CPI and listing prices
    - Concentration of property ownership in Neighbourhoods
    - Best time of the year to operate an AirBnB

- [Amenities Analysis](#Amenities-Analysis)
  - [Dashboard Demo](#Dashboard-Demo)
  - Dashboard details & analysis into:
    - Market Basket Analysis on Amenities Offered
    - Identify amenities that people are willing to pay and how much more they will pay
    - How breakfast offerings affects prices in neighbourhood with many attractions vs less attractions 

- [Conclusion and Recommendations](#Conclusion-and-Recommendations)


## Introduction
Running an Airbnb has always fascinated me, and Seattle's vibrant atmosphere and proximity to nature further piqued my interest. This led to the motivation behind this project: to gain a comprehensive understanding of the Airbnb market in the city. The primary objective of this data analytics project is to analyze the Airbnb market in Seattle and provide valuable insights for potential hosts and travelers.

The project will leverage data from Airbnb listings, along with external datasets, to create an [interactive visualization tool](https://public.tableau.com/app/profile/nahyy4315/viz/CuratingthebestairbnbinSeattle/Geospatialanalysis) that offers insights into the following aspects of Airbnb rentals in Seattle:

1. Neighbourhoods
2. Attractions
3. External Market Conditions
4. Amenities

The resulting interactive visualization will serve as a valuable tool for both current and potential Airbnb hosts, as well as travelers looking for the best accommodation options in Seattle

Additionally, a sentiment analysis segement to analyze guest experience through text mining of guest reviews has been conducted to understand the factors affecting the overall guest experience.

### Data
- AirBnB data was sourced from [Kaggle](https://www.kaggle.com/datasets/airbnb/seattle)
- Data on all attractions in Seattle was extracted with the Foursquare API
- CPI data was sourced from [Federal Reserve Economic Data (FRED)](https://fred.stlouisfed.org/)

## Neighbourhood Analysis
The objective of this dashboard was to provide a comprehensive yet broad overview into different neighbourhoods in Seattle. 
<br>

### Dashboard Demo:
![Neighbourhoods Dashboard Demo](images/neighbourhood_db.gif)
<br>
The first revelation is that neighbourhoods that with above median prices are typically on the western side of Seattle. On the other hand, the cheaper neighbourhoods are on the innerside of the city . 

<div style="display: flex; flex-direction: row;">
    <img src="images/nbh above med.png" alt="Western side" width="500" />
    <img src="images/nbh under med.png" alt="Others" width="500" />
</div>

Next, investigations will delve deeper into the behaviour of the market across time. Excluding 2016 due to the lack of data, between 2014 to 2015 it seems like every neighbourhood has been experiencing falling prices along with an increase in quantity listings except for Magnolia, Beacon Hill, Lake City and Other Neighbourhoods. 

Since Other Neighbourhoods is a catchall term for listings in neighbourhoods "not recognised" by Airbnb, it is not suprising to be amongst the few cities with the largest variance. However, Magnolia is a "recognised city" like Beacon Hill, Lake City so it is worthwhile invesitgating why the variances  is so large in Magnolia.

Lastly, based on the the dashboard, reasonable prices to charge is between $72 to $150, depending on the neighbourhood. However, since this is more than 100% higher than the lower bound charged across all neighbourhoods as seen below, further research was conducted to understand the reason behind the drastic price differences.

![Alt text](images/nbh_lower_bound.png)

A correlation test against price was conducted. It shows that the number of people a listing accomodates is highly correlated with price.

<img src="images/price_correlation.png" alt="correlation">

Digging deeper to understand how the number of people a listing accomodates, we see that the average price peaks when there are 11 people to accomodate and dips at 15.

<img src="images/accom_price_correlation.png" alt="accommodation distribution">

## Geospatial Analysis:
<br>

### Dashboard Demo:
![Geospatial Dashboard Demo](images/geospatial_db.gif)
<br>
Attractions data extracted from the Foursquare API included other insightful information like:  
| Field       | Description                                                                                                             |
|-------------|-------------------------------------------------------------------------------------------------------------------------|
| rating      | A numerical rating (from 0.0 to 10.0) of the FSQ Place, based on user votes, likes/dislikes, tips sentiment, and visit data. Not all FSQ Places will have a rating. |
| popularity  | Measure of the FSQ Place's popularity, by foot traffic. This score is on a 0 to 1 scale and uses a 6-month span of POI visits for a given geographic area.   |
| price       | A numerical value (from 1 to 4) that best describes the pricing tier of the FSQ Place, based on known prices for menu items and other offerings. Values include: 1 = Cheap, 2 = Moderate, 3 = Expensive, and 4 = Very Expensive. |

After ranking the neighbourhoods according to respective attraction data based on average rating, popularity and price, it can be seen that attractions in Downtown, Capitol Hill and Ballard dominates accross all boards on popularity, rating and priciest neighbourhoods. Whereas the opposite would be said for attractions in Interbay and Cascade.  

![Alt text](images/attractions_ranked.png)

Based on prior travelling experience, a dissapointing situation as a tourist was when an attraction is one where popularity was higher than actual ratings and price was high. I engineered a new feature to capture this situation by taking the difference of popularity and rating for each attraction. Since dissapointment is also a product of price, this difference is also multiplied by the Price. After data preparation like min max scaling and replacing the 0s in price with 1, now we can clearly see the neighbourhoods with a concentration of dissapointing attractions being Downtown, Capitol Hill and Ballard.

![Alt text](images/disapointmentboxplot.png)

## Competitor Analysis
This segment of the analysis concerns external market conditions, the relationship between CPI and listing prices, property ownership in Seattle's neighborhoods and the impact of time in terms of age and demand.
<br>

### Dashboard Demo:
![Competitor Dashboard Demo](images/competitor_analysis.gif)
<br>
The relationship between age and listing prices was determined with Autocorrelation Function (ACF) after outliers in prices were removed and the data is smoothed with low pass filters. The ACF plot does show a positive correlation between the prices at different lags. This suggests that the prices tend to be similar over time. This may be due to a number of factors, such as the fact that Airbnb listings are often priced based on the same factors, such as the location and amenities of the listing.

![Alt text](images/ACF.png)

The relationship between CPI and listing prices was determined by the correlation coefficient between Airbnb listing prices and CPI data: 0.009861794181379615. This indicates a very weak linear relationship. That said, a correlation coefficient near 0 does not imply that there is no relationship between the variables; but that the relationship is not well-explained by a linear model. Other complex relationships or factors at play could be missed by the correlation coefficient alone.

Concentration of property ownership in Seattle's neighborhoods impacts Airbnb operations in several ways: by influencing property supply and competition, which directly affects profitability. Additionally, the significant presence of Airbnb businesses may reduce available long-term rental units, unlocking a new market with alternative pricing strategies to explore. 

The dashboard was created by implementing calculated fields in the scorecard and set actions to link the table to the scorecard. This allows the user to interact with the neighbourhood in the table to see the percentage of hosts with more than 10 listings (within Seattle) to their names and the proportion of listings in the neighbourhood that they collectively own. The insight gleaned from this is that the concentration of ownership is the highest in University District. 7.81% of hosts in University District own more than 10 listings. In total, the listings they own make up 45% of listings within University District.

Apart from concentration affecting the supply of AirBnBs in the market, the question of when is the best time to operate an AirBnB came to mind. To determine this, the change in price and number of listings depending on month will be considered. As seen below, listing prices rise significantly from June to September, explainable by the fact that there are less listings available for reservation in summer. There is also a rise in December which shows that people often visit during winter holidays too, although the increase in price is not as large as 70% of listings are on average available in December.

<div style="display: flex; flex-direction: row;">
    <img src="images/image-1.png" alt="change in qty available" width="500" />
    <img src="images/image-2.png" alt="change in price" width="500" />
</div>

Lastly, the dashboard also makes use of the simple linear regression model feature in Tableau to check for the significance in relationship between price and age of listings in month for different property types. Results for the apartment property type are as detailed: 

1. the R-squared is approximately 0.0006662, which is a very low value, It suggests that there is a weak or almost negligible linear relationship as changes in the number of months between first and last listings do not lead to significant changes in the price of listings.
2. the model's predictions may not be very precise as, predicted prices from the regression model deviate from the actual prices by around 78.785 units. 
3. p-value less than 0.0001 indicates that the results are statistically significant at a very high level of confidence. 
While the low p-value indicates that there is a statistically significant relationship between months and price, the extremely low R-squared value suggests that this relationship is practically insignificant. In other words, while the model shows that there is a statistical association between months and price, this association is so weak that it has very little practical relevance or explanatory power.  


## Amenities Analysis:
<br>

### Dashboard Demo:
![Amenities Dashboard Demo](images/amenities_db.gif)
<br>
The objective of the amenitites dashboard was to identify the amenities that are most frequently offered, detect patterns in ammenities offered, highlight those that people are willing to pay for and understand roughly how much more it is that they are willing to pay.

The dashboard makes use of market basket analysis to identify the amenities that are most frequently offered and detect amenities often offered in conjuction. This visualization makes use of sets, calculated fields and association rules.

The figure below shows the top 2 most frequently offered amenities are kitchen (12.18%) and heating (12.82%) and they often exist within a listing together. <br>
![Alt text](images/kitchen_mba.png)

To identify the amenities that people are willing to pay for, a Chi Square test was conducted. As seen below, kitchen, pool, tv, doorman, heating and gym are amenities with the highest Chi Square result and p-values.These amenities seem to be offered in specific property types like how only condominiums have amenities like doorman, pool and gym.
<br>
![Alt text](images/Amenity_chi.png)
<br>
In order to identify and quantify the impact of amenities on the median price of a selected property type, the dashboard applies proportional brushing.

Taking apartments for example, the visualisation below reveals the different amenities that contribute to prices. Lisitings with doorman amenities fetch a median price of $170, those with a pool fetch a median price of $150, those with a gym fetch a median price of $145. These amenities are rare and non-essentials, reflective of a more luxurious listing. 
![Alt text](images/ammenities_tiers.png)

On the other hand, apartments with breakfast included have the lowest median prices at $85 an interesting point for futher investigation. The breakdown of listings offering breakfast across neighbourhoods and property types can be seen below. Breakfast is often offered in houses, mostly in Central area and Rainer Valley. Given that these neighbourhoods are quite drastic in terms of the number of attractions, we can investigate how breakfast offerings affects prices.

<div style="display: flex; flex-direction: row;">
    <img src="images/breakfast.png" alt="change in qty available" width="500" />
    <img src="images/attractionsquantityneighbourhood.png" alt="change in price" width="500" />
</div>

Prices are dividied by the number of people the listing accomodates to isolate prices from the relationship with accomodation. The below histogram visualizing the distribution of prices shows that listings offering breakfast are cheaper in Rainer Valley than Capitol Hill, despite Capitol Hill having more attractions and places to visit for breakfast. This shows the demand for breakfasts exists as it actually value adds to the guest experience and guests are willing to pay more for the amenity. On the other side, breakfast is offered more frequently in cheaper listings in Rainer Hill as 8 listings offering breakfast are the cheapest, this likely is the case as breakfast is offered as a function of convenience due to the lack of attractions nearby. <br>
![Alt text](images/rainervscapitol.png)

## Conclusion and Recommendations

What neighbourhoods to operate in? <br>

| Shortlisted Neighborhoods | Rationale | Prices to Charge |
|---------------------------|-----------|------------------------|
| Downtown         | Listing prices have been increasing since 2011. The airbnb market has also been growing with more offering their place up for rent. Many attractions all over the neighbourhood makes it an attractive neighbourhood for tourists. Market saturation wise, there are less commercialized hosts, differentiation can easily be done through provision of breakfast or lowered cleaning fees.  | Above median price of $150 in the summer and $100 during other seasons |
| West Seattle            | Like Downtown, listing prices and quantity of listings have been increasing since 2011. Although there are not as much attractions in this neighbourhood, most of the attractions are not dissapointing and a large portion belong to the realm of nature. That said, attraction-density wise, it is among the worst. Therefore, a good way to differentiate would be through providing breakfast or a stocked kitchen. Market saturation wise, only 1 host in West Seattle owns more than 10 listings, which is relatively acceptable compared to University District.   | Above median price of $101 in the summer and $80 during other seasons, also depends on accomodation capacity |
| Queen Anne            | Listing prices have fallen as the quantity of listings on the market increased.  Market saturation wise, only 2 hosts in Queen Anne owns more than 10 listings, which is relatively acceptable compared to University District. That said, there are a 26 owning between  4 to 6 listings. Attraction density wise, the listings in this neighbourhood has between 18 to 48 attractions within 300m and has around 200 attractions as well. Highly rated attractions have a good mix of restraunts with cultural diverity, parks and outdoorsy places, making it a fun place tourists will gravitate to. | Above median price of $119 in the summer and $80 during other seasons |

What amenities to offer? <br>

Across all neighbourhoods, it seems like there are already plenty of apartments in the market. I think a condominium that has a doorman,access to a pool and gym will be good to fetch higher prices. Offering breakfast in Downtown and Queen Anne can also fetch higher prices however it is not really worth it in West Seattle unless the listing is situated somewhere inaccessible since it is less touristy and people are not as willing to pay more. 
