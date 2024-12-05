## DATA 512 Course Project - Economic Impact of Wildfires on Tourism in St. Petersburg

### Goal of the Project
This project explores the effects of wildfire smoke on St. Petersburg, Florida, over a 60-year period. The analysis investigates the long-term impacts on public health, economic activities, and environmental quality, focusing on the city’s tourism-driven economy. The findings aim to assist policymakers and local authorities in developing strategies to mitigate wildfire-related risks, emphasizing economic resilience and community preparedness.

### License
This project is licensed under the [MIT License](https://opensource.org/licenses/MIT), which permits reuse, modification, and distribution with minimal restrictions. Users are encouraged to acknowledge the original creators when distributing copies or derivatives of this project.

### Process Flow

#### 1. Data Acquisition:
   - **Wildfire Data**: The analysis utilizes U.S. Geological Survey (USGS) data on wildland fires, specifically focusing on combined wildfire polygons. This dataset spans from the 1800s to the present and provides geo-located wildfire information essential for estimating smoke impacts.
   - **Air Quality Data**: Air Quality Index (AQI) data is sourced from the U.S. Environmental Protection Agency (EPA) via the AQS API. AQI measures are derived from air quality monitoring stations and help estimate smoke’s impact on air quality near the selected city.
   - **Economic Indicators**: Additional data sources include:
     - **Florida Department of Revenue’s Tourism Development Tax Data**: Represents revenue from tourism tax collections, reflecting the financial health of the local tourism sector. Previously known as “Bed Tax” it is collected from all the guests who engage in renting a Short-Term Rental (STR) for boarding and lodging purposes. As this signal is strongly correlated with the number of tourists visiting the city, we intend to use it to understand the impact of wildfire events/smoke estimates on the potential revenue of the tourism industry.
     - **St. Pete-Clearwater Airport Passenger Statistics**: Tracks the monthly volume of arriving and departing passengers, a proxy for visitor traffic. By analyzing trends in passenger frequency during wildfire smoke events, we can observe the potential impact on visitor numbers.
     - **Arts and Culture Production Economic Data**: A measure of the economic contributions from the arts and culture sectors, which are one of the major sectors in economic impact in the region. By analyzing these turnover amounts alongside wildfire smoke data, we can infer potential declines in visitor-driven cultural activities.
     - **SBA Disaster Loan Data**: This dataset will help provide a tentative estimate of the economic toll on small businesses during natural disasters. We primarily intend to use this to drive insights on government aids, insurance coverage/defaults and what steps can the administration take to help local businesses bounce back from such events.


#### 2. Data Cleaning and Merging:
   - **Geo-Spatial Filtering**: Wildfires within a 650-mile radius of St. Petersburg are selected, focusing on their proximity’s impact on air quality.
   - **Seasonal Data Filtering**: The analysis considers wildfires during the fire season (May 1 to October 31), when smoke impact is most significant.
   - **Inflation Adjustment**: Economic data is adjusted for inflation using the Consumer Price Index (CPI) for Pinellas County, ensuring comparability across years.

#### 3. Metric Calculation and Analysis:
   - **Smoke Impact Estimation**: A custom metric, the “Smoke Estimate,” is created using a logarithmic transformation of the ratio between the acres burned and the shortest geodetic distance of fire perimeters from the city. This methodology accounts for smoke dispersion and outliers.
   - **Economic Correlation Analysis**: Relationships between smoke estimates and economic indicators (e.g., Tourist Development Tax and airport passenger traffic) are analyzed, revealing potential impacts on tourism and local industries.
   - **Predictive Modeling**: A time series model ([FB-Prophet](https://facebook.github.io/prophet/)) is employed for forecasting trends in smoke impact and economic recovery metrics (Coverage Ratio), incorporating uncertainty estimates.

#### 4. Visualization:
   - **Distance-based Histogram**: A histogram displays the distribution of wildfire occurrences based on their distance from the city.
   - **Annual Acres Burned**: A time series graph shows trends in fire frequency and intensity within the analysis range.
   - **Economic Impact and Recovery Trends**: Visualizations highlight relationships between wildfire smoke, economic indicators, and recovery loan sufficiency over time.

### Model Description
Facebook's Prophet is an open-source tool designed for producing high-quality forecasts for time series data that may have non-linear trends, seasonal patterns, and changepoints. It is particularly effective for business applications requiring robust predictions with minimal tuning, such as forecasting demand or impact trends. Prophet allows users to incorporate holiday effects and uncertainty intervals, making it a versatile choice for complex data scenarios. For detailed documentation, visit the [Prophet documentation](https://facebook.github.io/prophet/).

### Repository Structure (including data files overview)
```
.
├── cleaned_data/                     # Processed datasets used in the analysis
│   ├── CPI St. Petersburg.csv        # Consumer Price Index data for St. Petersburg
│   ├── future_smoke_estimate.csv     # Projected smoke impact estimates
│   ├── gj_data_within_650_miles.json # Geospatial wildfire data within 650 miles
│   ├── mean_smoke_impact_estimate_for_year.json  # Annual smoke impact estimates
│   ├── St. Pete Airport Passengers.csv           # Airport passenger data for the city
├── graphs/                           # Visualizations and graphs generated during analysis
├── raw_data/                         # Raw datasets before preprocessing
│   ├── extension_data/               # Additional datasets for extended analysis
|       ├── sba loan data/            # Small business loan-related data
|       ├── TourismDevelopmentTax/    # Data on tourism tax revenue
|       ├── passengers-by-month-history.pdf  # Historical passenger data report
|       ├── CAGDP2_FL_2001_2021.csv   # Data for Art, culture and recreation sectoral GDP
│   ├── fire_data/                    # Raw wildfire-related data
├── .gitignore                        # Git ignore file
├── LICENSE                           # License information (MIT License)
├── README.md                         # Repository documentation
├── Part 1 - Common Analysis.pdf      # Project report detailing analysis methodology and findings
├── Part3-Pechakucha-St.Petersburg_RohitChandiramani.pptx # Presentation on the project
├── analysis.ipynb                    # Main Jupyter Notebook for analysis
├── extension_analysis.ipynb          # Additional analysis notebook for extended insights
```

### Data and Code Sources

- [**USGS Wildfire Dataset**](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81): The primary data source for fire polygons, this dataset provides detailed geospatial information on wildfires across the U.S. It allows for analysis of fire size, location, and frequency over time, which is essential for estimating smoke impact on urban areas.
  
- [**EPA Air Quality System (AQS) API**](https://aqs.epa.gov/aqsweb/documents/data_api.html): This API provides access to AQI data, which includes air pollutant measurements from EPA-monitored stations across the U.S. This data is essential for validating the smoke impact estimates against official air quality measures.
- [**Florida Department of Revenue Tourism Tax Data**](https://floridarevenue.com/dataPortal/Pages/TaxResearch.aspx): Reflects financial health of the tourism sector.
- [**St. Pete-Clearwater Airport Passenger Statistics**](https://fly2pie.com/news-and-media/passenger-statistics): Proxy for visitor traffic analysis.
- [**Arts and Culture Production Data**](https://www.bea.gov/data/special-topics/arts-and-culture): Represents economic contributions from cultural activities.
- [**SBA Disaster Loan Data**](https://www.sba.gov/document/report-sba-disaster-loan-data): Assesses economic recovery sufficiency during disasters.

- **Provided Code Examples**:
    - [*epa_air_quality_history_example.ipynb*](https://drive.google.com/file/d/1fwS60QStiMDqwINvW2LEDFBX5xg6Wnmg/view?usp=drive_link): Demonstrates how to retrieve AQI data from the EPA's AQS API.
    - [*wildfire_geo_proximity_example.ipynb*](https://drive.google.com/file/d/1B7AGlaW7d-27bHKLVXGBwLt8T-Elx-HB/view?usp=drive_link): Provides methods for calculating distances between cities and wildfire perimeters, which aids in estimating potential smoke travel distances.

These code templates and data resources, provided by Prof. David McDonald from the University of Washington, support the analysis and facilitate access to essential external data sources, ensuring consistency across project submissions. The example code and dataset documentation are licensed under the [CC-BY](https://creativecommons.org/licenses/by/4.0/) license, permitting reuse and adaptation with attribution to the original author.