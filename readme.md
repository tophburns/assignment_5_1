# Problem Statement

A survey of drivers was conducted where multiple driving scenarios are presented and the driver is offered a coupon to a local restaurant, bar or coffee house and then asked if they would accept the coupon. The survey contains 12,684 individual driver responses. The data includes driver attributes such as gender, approximate age, marital status, education, occupation, income, along with monthly restaurant, bar and coffee house visits of the driver. Additionally, the data includes contextual attributes about the driving scenario, eg. location of the driver and the destination of the coupon, weather and temperature at the time of the scenario, etc. The goal of this analysis is to identify any driver characteristics that would distinguish between customers that would accept a coupon versus those that would not.

# Data Summary

In exploring the quality of the data, I observed the following:

- The `car` column contains almost no data, less 1% of the responses include information about the car. Additionally, the few data values we have for the car are inconsistent in their meaning, including only a single make and model, "Mazda5", a generic description of "crossover" and entries that are simply stating the car is too old to install Onstar. Based on this I conclude the `car` column contains little value to my analysis and removed it from the dataset.
- There are various inconsistencies in the spelling and naming conventions used in the data. Examples include a mix of CamelCase and snake_case, a column named `CarryAway` that represents how often the driver purchased takeout food, but the corresponding coupon is referred to as "Carry out & Take away". I renamed several of these columns/values to address these inconsistencies and minimize the risk of misinterpreting the data due to a mismatch of wording.
- Every survey question about frequency of visits to bar, coffee house or restaurants is missing approximately 1% of their values. I replaced all these missing values with a new `no_answer` value so I could accurately represent this data, the driver didn't answer the question, and isolate and do further analysis on this subset of data if it looked informative.
- The majority of the survey questions are categorical fields. Even columns like `age` and `temperature` that have numeric values, contain a limited set of values that are actually buckets. Age for instance has buckets:
  - below 21
  - 21 - 25
  - 26 - 30
  - 31 - 35
  - 36 - 40
  - 41 - 45
  - 46 - 49
  - 50 plus
- Approximately 0.5% of the rows contained duplicate values. However, since this data does not contain any uniquely identifying driver information, I see no reason to believe these are actually duplicate survey responses. It's possible these are simply identical driving scenarios and responses from different drivers. If we had birth date instead of age buckets, drivers make, model and year of their car, or exact income from 1040 tax filing, then we could identify the individual drivers and know for sure if these rows represent duplicate responses. As such, I did not remove or modify any of these duplicate rows.

# Findings

## Overall Findings

Overall, 56.84% of drivers accepted the coupon that was offered. The coupons were for 5 different types of businesses: Bar, Coffee House, Carry Away, Restaurants costing less than 20 dollars and Restaurants costing between 20-50 dollars. The majority of coupons offered were for coffee houses, which had 50% acceptance rate. Higher cost destinations had lower acceptance rates, with bar coupons only accepted 41% of the time and more expensive restaurants 44% acceptance. However, lower cost restaurants and take away showed high coupon acceptance, with take away coupons being accepted ~74% of the time and <20$ restaurants being accepted ~71%.

In general, drivers are more likely to accept coupons for higher cost or boutique destinations (eg. bars, coffee houses, restaurants > $20) if they already frequent these types of establishments more than once per month. This is true independent of other factors like income or age. However, when it comes to inexpensive restaurants or take aways, all drivers showed positive acceptance rates of coupons to these establishments.

There are a few occupations that accepted some coupons at elevated rates. For example, healthcare workers, transporation workers and students accepted coffee coupons at high rates ranging from 61-74%. Similary, bar coupons were accepted at higher rates for drivers working in Life, Physical or Social Sciences, Architecture & Engineering and Production roles (62-67% acceptance rates). Further exporation could be done to identify particular occupations to target these coupons to in an effort to increase overall adoption.

Weather also plays a role in coupon acceptance with sunny days showing a higher acceptance rate at 59% compared to rainy days at 46%.

Below are a more summary details on how the acceptance rate was impact by driver monthly visits beyond the summary given above. More details on my research and findings, including multiple plots of the data, can be found [in the associated Jupyter notebook](./prompt.ipynb)

## Recommendations

My initial recommendation would be to focus on coupons to lower cost restaurants and take aways, particularly on warm sunny days. For more expensive destinations, targeting those coupons at particular audiences to increase adoption. For instance, healthcare workers and students accept coffee coupons at high rates, targeting these coupons for drivers in the proximity of universities and hospitals should show high levels of acceptance.

## Next Steps

If I were to continue exploring this data I would look to see if other demographics impact acceptance rate like education level, marital or family status. Or some of the contextual data, for instance is a driver more likely to accept a coupon if they're on their way home versus on their way to work? Would you accept a bar coupon on your way home but not on your way to work? Or vice versa with coffee coupons?

## Bar Coupons

Drivers who frequent bars more than once per month are more likely to accept a coupon to a bar. The acceptance rate for drivers who frequent bars 1 or more times per month range from 65% to 78%. Whereas individuals who visit bars less than once per month only accepted bar coupons 44% of the time. Drivers who never go to bars rejected bar coupons 81% of the time. This held true regardless of other driver attributes like income or age. For example, in looking at the acceptance of bar coupons across income, I saw now indication of any income bracket that was more likely to accept the coupon.

## Coffee House Coupons

Similar to bars, the determining factor to whether drivers accept a coupon to a coffee house is primarily determined by the drivers monthly coffee house visits. The more often the drivers already goes to coffee houses, the more likely they are to accept a coupon to a coffee house. And similar to the bar coupons, income was not an indicator of coffee coupon acceptance. However, driver occupation was, specifically healthcare workers, transporation workers and students all had high acceptance rates ranging from 61% to 74%.

## Expensive vs Cheaper Restaurants

Expensive restaurants exhibited a similar trend as bar and coffee house coupons with the accept rate dependent on existing visit habbits. However, that trend **does not hold true** for cheaper restaurants. Coupons for cheaper restaurants (less than 20 dollar restaurants and take aways) demonstrated different trends then the coupons to more expensive (or botique) destinations. These cheaper options saw positive acceptance rates across the board, even for drivers that didn't frequent these restaurants, with acceptance rates ranging from 55% - 89%. For example, drivers who went to under $20 restaurants fewer than once per month still accepted coupons to these restaurants 67% of the time. We see similar trends, but slightly higher with the carry away coupons, with acceptance rates ranging from 67% - 86%.

## Weather

There is a small improvement in coupon acceptance rate based on weather. Sunny days had higher acceptance rate at 59% compared to rainy days at 46%. Similary, temperature showed a small improvement in acceptance rate as the temperature increased, 80 degree day had acceptance rate of 60% compared to 53% for 30 degree days.

