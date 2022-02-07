# **CTA Ridership Analysis**

## Problem Statement

CTA (Chicago Transit Authority) ridership levels have dramatically changed in the last two years due in large part to the COVID-19 pandemic. Considering Illinois' history of budgeting troubles and the large population that typically relies on the CTA suddenly not using it anymore, being able to predict CTA ridership has never been more practical. The goal of this project is to too find the most suitable way to predict CTA total ridership at different levels. Predicting at the Daily level is more helpful for riders while a longer weekly and monthly predictions are more helpful for operational purposes. We will determine which Time Series Model performs the best via AIC and RMSE, and which Regression performs the best via R2 and RMSE.

## Background

The Chicago Transit Authority (CTA) operates the nation’s second largest public transportation system. On an average weekday, 1.6 million rides are taken on CTA.[`source`](https://www.transitchicago.com/facts/) With such large ridership numbers and a proposed 2022 operating budget of \\$1.75 billion, it is critical that bother riders and administrators have a good understanding of the trends and expectations for what ridership will look like in the future.

In addition to a variety of models, a wide variety of related features will be examined as well to help adjust for the shock to the to CTA ridership levels due to COVID. Included in these features are such notable values as: Treasury Yield Curve Rates, weather, government COVID restriction indicators, vaccination rates, and new car registrations. These factors are believed to be related to ridership levels, and should influence positively the accuracy of our regression and Vector autoregression (VAR) models.


### Data

* [`CTA Ridership`](https://data.cityofchicago.org/browse?q=ridership&sortBy=relevance): The primary data source, pulled from most recent ridership data as of January 28, 2022
* [`CATA`](http://www.cata.info/news/?CategoryId=4&pg=5&F_All=y): Chicago Automobile Trade Association new car registration data
* [`Weather`](https://www.ncei.noaa.gov/access/search/data-search/daily-summaries?bbox=42.082,-87.830,41.686,-87.434&startDate=2001-01-01T00:00:00&endDate=2022-01-24T23:59:59): Chicago weather data back to 2001
* [`COVID Response`](https://covidtracker.bsg.ox.ac.uk/): Government Covid response data
* [`Chicago Vaccination Rates`](https://data.cityofchicago.org/Health-Human-Services/COVID-19-Daily-Vaccinations-Chicago-Residents/2vhs-cf6b): Vaccination rates over time in Chicago
* [`Gas Commodity Data`](https://finance.yahoo.com/quote/RB%3DF/historyperiod1=978307200&period2=1643673600&interval=1d&filter=history&frequency=1d&includeAdjustedClose=true): Historical stock data ticker 'RB=F'
* [`US Treasury Yield Curve`](https://home.treasury.gov/policy-issues/financing-the-government/interest-rate-statistics?data=yield): From US Department of the Treasury
* [`Chicago Car Crash Data`](https://data.cityofchicago.org/Transportation/Traffic-Crashes-Crashes/85ca-t3if): Tracks car crashes reported to police
* [`Weekly Retail Gas Price Data`]https://www.eia.gov/dnav/pet/hist/LeafHandler.ashx?n=PET&s=EMM_EPMRR_PTE_YORD_DPG&f=W): From US Energy Information Administration

### Folder Layout

In this repository you'll find four folders: '0.0-prep_cleaning,' '1.0-merging,', '2.0-eda', and '3.0-modeling.' In this current folder you'll also find the pdf for my presentation.

In the '0.0' folder you'll find a few notebooks containing inital examination of data and some very light cleaning for before the merging step. In here you'll also find a short web scraper used to download all the pdf files from the CATA website in order to compile all Chicago new car registration data. 

In file '1.0' you'll find the heave lifting in terms of data cleaning. The daily file contains most of the cleaning with the weekly and monthly being derived in large part from that data with some new data added.

Folder '2.0' contains the EDA for this project. You'll find a few charts including Autocorrelation and Partial Autocorrelation charts and the testing of those correlations for use in the modeling section.

Finally, the '3.0' folder contains the code for the models run. You'll find around half a dozen versions of timeseries plots from ARIMA to Prophet, as well as a few basic regression models such as RandomForest and XGBoostRegressor.

### Data Dictionary

| Feature                               | Type               | Description|
|---------------------------------------|--------------------|------------|
|bus                                     |float64| CTA bus ridership|
|rail_boardings                          |float64| CTA "L" train ridership| 
|total_rides                             |float64| CTA combined ridership|
|prcp                                    |float64| All Chicago preciptation (rain,snow,etc.)|
|tmax                                    |float64| Max temp|
|tmin                                    |float64| Min temp|
|gas_open                                |float64| Opening price for ticker: (RB=F)|
|gas_close                               |float64| Closing price for ticker: (RB=F)|
|gas_volume                              |float64| Trade volume for ticker: (RB=F)|
|3_mo                                    |float64| US Treasury Yield Curve Rate|
|6_mo                                    |float64| US Treasury Yield Curve Rate|
|1_yr                                    |float64| US Treasury Yield Curve Rate|
|2_yr                                    |float64| US Treasury Yield Curve Rate|
|3_yr                                    |float64| US Treasury Yield Curve Rate|
|5_yr                                    |float64| US Treasury Yield Curve Rate|
|7_yr                                    |float64| US Treasury Yield Curve Rate|
|10_yr                                   |float64| US Treasury Yield Curve Rate|
|20_yr                                   |float64| US Treasury Yield Curve Rate|
|C1_School closing                       |float64| US Treasury Yield Curve Rate|
|C2_Workplace closing                    |float64| Specified COVID Restriction indicator for Illinois|
|C3_Cancel public events                 |float64| Specified COVID Restriction indicator for Illinois|
|C4_Restrictions on gatherings           |float64| Specified COVID Restriction indicator for Illinois|
|C5_Close public transport               |float64| Specified COVID Restriction indicator for Illinois|
|C6_Stay at home requirements            |float64| Specified COVID Restriction indicator for Illinois|
|C7_Restrictions on internal movement    |float64| Specified COVID Restriction indicator for Illinois|
|C8_International travel controls        |float64| Specified COVID Restriction indicator for Illinois|
|E1_Income support                       |float64| Specified COVID Restriction indicator for Illinois|
|E2_Debt/contract relief                 |float64| Specified COVID Restriction indicator for Illinois|
|H1_Public information campaigns         |float64| Specified COVID Restriction indicator for Illinois|
|H2_Testing policy                       |float64| Specified COVID Restriction indicator for Illinois|
|H3_Contact tracing                      |float64| Specified COVID Restriction indicator for Illinois|
|H6_Facial Coverings                     |float64| Specified COVID Restriction indicator for Illinois|
|H7_Vaccination policy                   |float64| Specified COVID Restriction indicator for Illinois|
|H8_Protection of elderly people         |float64| Specified COVID Restriction indicator for Illinois|
|ConfirmedCases                          |float64| Confirmed Illinois COVID Casesv
|ConfirmedDeaths                         |float64| Confirmed Illinois COVID Deaths|
|StringencyIndex                         |float64| Indicator of intensity of COVID restriction|
|StringencyLegacyIndex                   |float64| Indicator of intensity of COVID restriction|
|GovernmentResponseIndex                 |float64| Specified COVID Restriction indicator for Illinois|
|ContainmentHealthIndex                  |float64| Specified COVID Restriction indicator for Illinois|
|EconomicSupportIndex                    |float64| Specified COVID Restriction indicator for Illinois|
|total_daily_doses                       |float64| Total COVID Vaccine doses sum for Chicago|
|total_daily_cum                         |float64| Cumulative total COVID vaccine doses for Chicago|
|first_dose_daily                        |float64| Number of first doses of the COVID vaccine given|
|first_dose_cum                          |float64| Cumulative number of first doses of the COVID vaccine given|
|first_dose_percent_pop                  |float64| Percent of population given first dose of vaccine|
|vax_series_completed_daily              |float64| Number of people given both doses of vaccine|
|vax_series_cum                          |float64| Cumulative number of people given boths doses of vaccine|
|vax_series_percent                      |float64| Percent of population that has complete both doses of vaccine|
|crash_occurrences                       |float64| Number of car accidents in Chicago that have a filed police report|
|damage_indicator                        |float64| 1 - 3 indicator of cost of Chicago car crashes 3 being the most expensive|
|gas_price                               |float64| Retail gas prices for Chicago|
|new_light_truck_reg                     |float64| New light truck registrations in Chicago
|new_car_reg                             |float64| New car registrations in Chicago|
|new_total_reg                           |float64| Total combined new car and truck registrations in Chicago|


## Executive Summary

In this project we seek to explore the affect that COVID-19 had on CTA ridership and whether or not we can predict past the inital drop in ridership. To do this we will be using a varieyt of timeseries and regression models.

The first step was to collect all the necessary data. The CTA website provided the primary data on ridership, however, their data is not all up-to-date and is only updated rarely so cleaning and resampling the most up-to-date data into the form I needed was essential. A few methods were used to collect the other data used in this project. Most of it was open source provided by different government and eduactational bodies. One notable exception is the Chicago Automobile Trade Association who had all the data on Chicago new car registrations listed on their website in about one hundred fifty pdf files. To solve for this, I built a short web-scraper to go into their website and download all the pdf's for entry into a spreadsheet. Some of the data received from this website was corrupt or inaccurate so I imputed the mean of the surrounging cells into those NaN's.

Once all the data was received, it had to be compiled into three separate final files at different dat/time levels: daily, weekly, monthly. The reason for this is to compare both model accuracy at different levels of time as well as practicality. For example, an average CTA rider won't have much of a use for monthly predictions on ridership, but a daily or weekly prediction of number of riders could lead to useful predictions on train delays. On the other hand monthly ridership predictions could be an invaluable resource in determining operating expenses of the CTA by the administration. But since historical data on ridership only goes back about 20 years, data loss was a huge concern for this project, so having a larger iteration of the same dataset could lead to very different results. 

![](../capstone_data/imgs/dailyridership.png)

As we can see above the daily ridership for busses and trains is fairly consistent until 2020 in which it dips severly as the number of confirmed COVID cases spikes. Worth noting is the density of the line plot for the daily data. It has a very muddy shape that is not emulated in the weekly and monthly data. This density led to some interesting results when comparing the plots

![](../capstone_data/imgs/Linear-annual-lag.png)

The first model was a Linear Time Series with a variety of lags included based on Autocorrelation and Partial Autocorrelation charts. As we can see it seems to fit to the data fine until the drop in ridership in which it has trouble adjusting. This was the throughline for this project. Models couldn't adjust for an extreme shock like the pandemic, despite some steps taken to help it improve.

![](../capstone_data/imgs/Prophetpredsdaily2.png)

For example, one of the models tested was Facebook's Prophet model. While this model didn't score as well as some of the other's, especially at the monthly level, it was a flexible enough model where I could adjust seasonality and Holidays at a fairly granular level. The above plot shows the result of one of those tests, where I created a COVID on and off season to let the model know ahead of time to expect some volatility. As you can see, this had very modest success. The model recognized the seasonality, but, unfortunately, a season is a repeating even whereas this is a single massive shock so trying to game the system this way was not as succesful. Worth noting is doing a base Prophet model appeared to be extremely effective had the COVID drop not happened. It conformed very well to the subtle trends and seasonality in the training data, however it was this auto trend detection that led to its downfall.


## Conclusions and Recommendations


#### Daily

| Model                                 | RMSE               | Other    |
|---------------------------------------|--------------------|------------|
| Linear w/ annual                      | 317,766.52         | AIC: 151,287.11 |
| Linear w/o annual                     | 207,743.97         | AIC: 165,448.67 |
| ARIMA(9,1,12)                         | 182,640.85         | AIC: 163,297.62 |
| SARIMAX(6, 1, 2)x(5, 0, [1, 2, 3], 7) | 729,083.44         | AIC: 164,875.68 |
| SARIMAX(6,1,2,7)                      | 56,628,560,806     | AIC: 164,823.30 |
| VAR                                   | 335,815.98         | AIC/BIC: 18.18  |
| Prophet                               | 373,906.89         | MDAPE: .042     |
| RandomForest                          | 358,914.75         | R2: 0.41, 0.35  |
| LinearRegression                      | 371,335.56         | R2: 0.34 ,0.31  | 
| XGBoost                               | 358,299.85         | R2: 0.40, 0.36  |
|                                       |                    |                 |


#### Weekly

| Model                     | RMSE         | Other          |
|---------------------------|--------------|----------------|
| LinearTime w/ Annual      | 1,875,878.55 | AIC: 22,137.64 |
| LinearTime w/o Annual     | 1,141,954.78 | AIC: 23,562.97 |
| ARIMA(23,1,18)            | 736,057.29   | AIC: 24,116.00 |
| Auto-ARIMA(8,1,2)         | 780,236.69   | AIC: 24,362.11 |
| SARIMAX(8,1,2)(6,1,2)[52] | 860,067.67   | AIC: 22,086.11 |
| VAR                       | 780,051.84   | AIC/BIC: ~16.5 |
| Prophet                   | 1,570,733.39 | MDAPE: 0.028   |
| LinearRegression          | 752,057.08   | R2: 0.86, 0.84 |
| RandomForest              | 674,141.51   | R2: 0.96, 0.87 |
| XGBoostRegressor          | 666,553.70   | R2: 0.98, 0.87 |
|                           |              |                |


#### Monthly

| Model                     | RMSE          | Other          |
|---------------------------|---------------|----------------|
| LinearTime w/ Annual      | 17,196,311.05 | AIC: 5,879.04  |
| LinearTime w/o Annual     | 19,463,350.10 | AIC: 6,110.61  |
| ARIMA(17,1,10)            | 6,515,672.95  | AIC: 6,139.96  |
| Auto-ARIMA(3,1,5)         | 6,155,633.02  | AIC: 6,249.84  |
| SARIMAX(8,1,5)(6,1,4)[12] | 5,461,922.37  | AIC: 5,781.00  |
| VAR                       | 6,278,740.81  | AIC/BIC: ~44   |
| Prophet                   | 13,110,986.04 | MAPE: 0.10     |
| LinearRegression          | 5,239,220.40  | R2:0.85, 0.68  |
| RandomForest              | 5,612,426.81  | R2: 0.89, 0.63 |
| XGBoostRegressor(tree)    | 5,570,271.10  | R2: 0.87, 0.64 |
| XGBoostRegressor(linear)  | 5,574,917.50  | R2: 0.83, 0.63 |
|                           |               |                |



Above we can see the results of all the models at the differnt time levels. The timeseries models were built around their AIC scores while the Regressions around their R2 score as primary determination factor of efficacy. RMSE was the leveler and allowed for a convenient comparison across the board.

The most successful model was Vector Autoregressions by a long shot. This is due to the highly correlated nature between CTA Ridership and some of the other factors included in those models. However, for models with a single target value, The SARIMA models tended to perform the best followed very closely by the linear models which was an interesting and unexpected result. All ARIMA based models and regression models were tuned both manually and via GridSearch to find the best parameters.

The most effective regresion model ended up being the XGBoostRegressor followed closely by RandomForest models. Unsruprisingly they were slightly overfit despite regurlarzation efforts, but other than at the monthly level, it was not by much. 

It seems clear from these results that at this time the TimeSeries forecasts are not accurate enough to be very practical for business or personal usage purposes. The sudden drop in ridership and the continued uncertainty around the COVID virus, as well as the status of travel and work, leads to a near impossible standard to predict to. Having said that, several of these models did a fine job forecasting around the drop, just not through it. Special attention was paid to how the training and testing sets were split. The model that were split before the pandemic failed to adjust to the drop, while the models that were split on or near the pandemic had trouble recovering from the drop.

The best predictions came at the weekly level. This makes sense considering the percentage of data lost to the monthly resample. The data in monthly was just too generalized to be very effeictve in modeling and the opposite can be said for the daily data. The weekly showed decent bias/variance tradeoff and some of the regressions were salvageable. It could be a useful tool at some point in the future to hone further in on the regression variable of value for general predictions.

When continuing work on this project here are a few things that can be impoved.

1. Although the Prophet model didn't generalize to the pandemic very well, with more time spent creating customer holidays to indicate a one-time event, I believe it could perform even more impressively.
2. More data is needed. CTA will hopefully continue to update their datasets and at some point more data will have huge impact on accuacy of forecasts.
3. I was able to make a few ineracitve forecast charts that would be great in an app or connected to GoogleMaps to help predict how busy the CTA is at that time. Similar to the existing function they have for restaurants.

## Citations
