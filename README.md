# Assessing the Relationship between New York City Precipitation Patterns and Global Land Temperature Anomalies: Implications for Climate Change Analysis
<p align="center">
  <img src="https://static01.nyt.com/images/2021/08/07/us/07xp-elsalandfall-2/07xp-elsalandfall-2-superJumbo.jpg" />
</p>

### Overview:
Studies indicate that extreme weather conditions are likely to become more frequent with the global rise in climate change. Given the recent heavy rainfall we have experienced in NYC over the summer, the purpose of this project is to explore whether or not these changes in NYC's precipitation levels show any observable correlations with global land temperature changes from 1900 to 2021. My underlying hypothesis was that the frequency of precipitation in New York would not show any observable increase on an annual basis, but more on a seasonal basis. In order to prove this hypothesis, I applied various time-series analysis/plotting techniques on my datasets.


### Data:
Both of the datasets used for this project are from the National Oceanic and Atmospheric Administration (NOAA).
- **[Daily NYC Precipitation (1900-2021)](https://www.ncdc.noaa.gov/cdo-web/datasets/GHCND/stations/GHCND:USW00094728/detail)**: Contains daily precipitation values taken from the NYC Central Park weather station. The weather station provides records starting from 1869, however, for this project only the records starting from 1900 were used. Precipitation values are measured in millimeters (mm.). The base value of 32mm. is used instead of 0mm.—even for days with no rainfall (dataset documentation does not specify why). In order to access and downlaod this dataset, the [NOAA API](https://www.ncdc.noaa.gov/cdo-web/webservices/v2) has to be utilized. 

- **[Monthly Global Land Temperature (1900-2021)](https://www.ncdc.noaa.gov/cag/global/time-series/globe/ocean/all/1/1900-2021)**: Contains monthly global land temperature values from 1900 to 2021. **The temperature values are based on land temperature** ***anomalies*** (i.e. a description of how the overall average temperature of the surface of the Earth deviates from what is expected) with the base periods being 1901-2000. This dataset is available for direct download. 

### Technique:
- #### Part 1: Retrieving and Cleaning Datasets
  - For retrieving the NYC precipitation dataset, I first had to generate an API key and then choose a weather station ID (GHCND:USW00094728) from the NOAA website. Then I had to make a JSON API call using the key and station ID to download and save the data as a CSV file. The data download portion took a while since I was working with a large time frame. The global land temperature dataset was directly downloadable as a CSV file. 
  - For cleaning the datasets, the datetime module was mainly utilized. 
- #### Part 2: Combining Datasets 
  - Although both of the datasets used the same year range (1900-2021), the precipitation dataset gave **daily measurements** while the land temperature dataset gave **monthly average measurements**. In order to ensure this would not be a problem when combining the datasets, I had to make a seperate dataframe of monthly precipitation averages. 
  - The land temperature and new monthly precipitation datasets were then merged using an **inner join** based on their values of month and year, and then saved to a new dataframe.
- #### Part 3: Data Analysis/Visualization
  - (See **[Analysis](#analysis)**)


### Analysis:

This first chart is a time series line plot which shows daily precipitation values from 1900 to 2021. Although the chart is very crowded, we can see a general distribution of precipition values. The chart shows the values for a total of **44,413 days with the mean, minimum, maximum, and standard deviation values being 37.8mm., 32.0mm., 378.1mm., and 16.4mm., respectively**. It may seem like it is impossible to make any constructive observations from looking at this chart, however, if we take a closer look we can see **dramatic spikes in precipitation values occur around 1900, 1980, and 2021**. More interestingly, if we count the occurance of the **number of spikes above 250mm. from 1900 to 1960 compared to the number of spikes from 1960 to 2021**, we can see an **increase in frequency**. 
<p align="center">
  <img width="700" height="530" src="https://raw.githubusercontent.com/Saida0/Data-Science-Project/main/PRCP_Daily.png">
</p>


Keeping in mind that certain months are naturally presented with more rainfall, I decided to look at seperate monthly precipitation averages using subplots. For most of the months, we can see an **increasing trend in the average precipitation value** as well as an **increase in the frequency of heavy rainfall spikes**. For instance, for the month of **June, between 1900 to 1960 (60-year interval)**, there was only **one instance where the precipitation value went past 45mm.**, but **between 1980 to 2021 (40-year interval)**, there were about **five instances where average rainfall went past the 45mm. threshold**.
<p align="center">
  <img width="1000" height="580" src="https://raw.githubusercontent.com/Saida0/Data-Science-Project/main/PRCP_Monthly1.png">
</p>


This chart is a simple time series line plot of the monthly global land temperature average. It shows a clear **increasing linear trend**, but how does it compare with the monthly NYC precipitation data?
<p align="center">
  <img width="700" height="530" src="https://raw.githubusercontent.com/Saida0/Data-Science-Project/main/Land_Temp_Monthly.png">
</p>


Because the two datasets use different metrics (millimeters vs. Celsius), I initially wanted to compare them by tracking their percent change in value from either their starting values from 1900 OR percent change from their anomaly values; however, using this method of "percent change" as a common metric for comparison gave unclear results. I resorted to using a secondary y-axis instead.

Although average monthly NYC precipitation does not show the same direct increasing trend as the average monthly global land temperatures, they seem to **show value spikes around the same years**. For instance, **both datasets reached new records for maximum values around 2016 (2.5C° for land temperature and 60mm. for precipitation**).
<p align="center">
  <img width="1000" height="575" src="https://raw.githubusercontent.com/Saida0/Data-Science-Project/main/Comparing_Monthly_PRCP_Land.png">
</p>


### Conclusion:
- #### What were the results? Was my hypothesis correct?
  - In my hypothesis, I had predicted that only looking at daily precipitation values would not show the same increasing trend as there is with the global monthly temperature data, but rather seasonal year-to-year precipitation values would. This hypothesis was somewhat correct because when looking at the data on a average monthly year-to-year basis, certain months showed an increasing trend.  

- #### What would I have done differently?
  - When cleaning and plotting the precipitation data, I would have dropped the days where there was little or no rainfall. Then, I would have done a distribution plot with the total number of days presented with only heavy rainfall for each year. This plotting method would have probably shown a better look at the increasing occurance of heavy rainfall in NYC.
