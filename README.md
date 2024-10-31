## DATA 512 Course Project - Part 1: Common Analysis

### Goal of the Project
This project explores the effects of wildfire smoke for St. Petersburg, Florida over a 60-year period. With increased frequency of wildfires impacting air quality across the western U.S., this analysis provides insights into the estimated smoke impacts on public health, economic activities, and environmental quality. The final deliverable aims to assist policymakers and local authorities in understanding and preparing for wildfire-related risks.

### License
This project is licensed under the [MIT License](https://opensource.org/licenses/MIT), which permits reuse, modification, and distribution with minimal restrictions. Users are encouraged to acknowledge the original creators when distributing copies or derivatives of this project.

### Process Flow

#### 1. Data Acquisition:
   - **Wildfire Data**: The analysis uses U.S. Geological Survey (USGS) data on wildland fires, specifically focusing on combined wildfire polygons. This dataset spans the U.S. and its territories, offering geo-located wildfire information from the 1800s to the present.
   - **Air Quality Data**: Air Quality Index (AQI) data is sourced from the U.S. Environmental Protection Agency (EPA) via the AQS API. The AQI measures are derived from air quality monitoring stations and are useful for estimating the impact of smoke on air quality near the selected city.

#### 2. Data Cleaning and Merging:
   - **Geo-Spatial Filtering**: Wildfires within 650 miles of the assigned city are selected, focusing on fires impacting the air quality in the vicinity. The distance is calculated using geodetic methods to accurately assess which fires are likely to affect the city's air quality.
   - **Seasonal Data Filtering**: The analysis considers only wildfires occurring during the primary fire season, from May 1 to October 31 each year, when smoke impact on air quality is typically highest.

#### 3. Metric Calculation and Analysis:
   - **Smoke Impact Estimation**: A custom metric is developed to estimate annual smoke impact based on proximity, fire size, and acreage burned. This metric serves as a rough indicator of how much wildfire smoke may reach the city.
   - **AQI Comparison**: The custom smoke impact metric is compared with EPA's AQI measures to assess the validity of the smoke impact estimation and provide insights into correlations with monitored air quality.
   - **Predictive Modeling**: A time series model ([FB-Prophet](https://facebook.github.io/prophet/)) is applied to predict smoke impact trends for the next 25 years, incorporating uncertainty estimates to guide future projections. This predictive approach aids in assessing potential long-term impacts on city planning and air quality.

#### 4. Visualization:
   - **Distance-based Histogram**: A histogram displays the distribution of wildfire occurrences based on their distance from the city, highlighting the range used for smoke impact estimation.
   - **Annual Acres Burned**: A time series graph shows the total acres burned each year within the analysis range, providing a visual trend of fire frequency and intensity near the city.
   - **Smoke and AQI Comparison**: Another time series visualization compares the annual smoke impact metric with AQI data, revealing trends in smoke influence on city air quality.

### Data and Code Sources

- [**USGS Wildfire Dataset**](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81): The primary data source for fire polygons, this dataset provides detailed geospatial information on wildfires across the U.S. It allows for analysis of fire size, location, and frequency over time, which is essential for estimating smoke impact on urban areas.
  
- [**EPA Air Quality System (AQS) API**](https://aqs.epa.gov/aqsweb/documents/data_api.html): This API provides access to AQI data, which includes air pollutant measurements from EPA-monitored stations across the U.S. This data is essential for validating the smoke impact estimates against official air quality measures.

- **Provided Code Examples**:
    - [*epa_air_quality_history_example.ipynb*](https://drive.google.com/file/d/1fwS60QStiMDqwINvW2LEDFBX5xg6Wnmg/view?usp=drive_link): Demonstrates how to retrieve AQI data from the EPA's AQS API.
    - [*wildfire_geo_proximity_example.ipynb*](https://drive.google.com/file/d/1B7AGlaW7d-27bHKLVXGBwLt8T-Elx-HB/view?usp=drive_link): Provides methods for calculating distances between cities and wildfire perimeters, which aids in estimating potential smoke travel distances.

These code templates and data resources, provided by Prof. David McDonald from the University of Washington, support the analysis and facilitate access to essential external data sources, ensuring consistency across project submissions. The example code and dataset documentation are licensed under the [CC-BY](https://creativecommons.org/licenses/by/4.0/) license, permitting reuse and adaptation with attribution to the original author.