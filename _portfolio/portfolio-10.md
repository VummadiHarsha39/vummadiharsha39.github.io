---
title: "Personal Project: In-Depth Look at Suffolk County Transit's Performance and Impact"
date: 2025-07-19
excerpt: "Suffolk County Transit's Data Analysis Case Study "
collection: portfolio
---



## Preface 
As a daily commuter in Suffolk County, the efficiency and reach of our local transit system, Suffolk County Transit (SCT), have always impressed me. Given Suffolk’s unique position as the largest easternmost county in the USA, I felt compelled to investigate whether SCT truly delivers on its purpose. This deep dive into SCT's operations aims to provide a comprehensive understanding of its performance, service coverage, and socio-economic impact.

This project is structured into three distinct parts, each offering a unique perspective on SCT:
* Part 1: Bus Ridership Analysis (2013–2016): A detailed examination of ridership trends and patterns.
* Part 2: SCT’s Performance Measures and Operational Characteristics (2013–2023): An analysis of key performance indicators and operational efficiency.
* Part 3: SCT Bus Route Analysis, GIS Visualization, and Social Demographic Impact: A comprehensive look at route coverage, visualized using GIS, and an assessment of its effectiveness in serving different social demographics, particularly poverty areas.


## Part 1: Bus Ridership Demographics: A Deep Dive into Trends and Distribution (2013–2016)

The initial phase of our project delves into understanding bus ridership demographics and overall trends from 2013 to 2016. By analyzing historical data, we aim to identify patterns in ridership over time and understand the distribution across various fare types. The data for this visualization was sourced from opendata.suffolk.

![Bus Ridership Pie Chart](/images/Bus_Ridership.png)

### Flow of Code:
* Data Preparation and Initial View: We began by loading bus ridership data from a CSV file into a pandas DataFrame. A 'Date' column was created by combining 'MONTH' and 'YEAR' for time-series analysis. A 'Total_Ridership' column was then calculated by summing all individual fare type columns (e.g., 'FULL_FARE', 'STUDENT'). The first 5 rows of the processed DataFrame were printed to confirm the new columns.
* Ridership Trend and Summary: A line plot was generated to visualize the 'Total_Ridership' over the 'Date' range, illustrating monthly trends from 2013 to 2016. The script also calculated and printed the total annual ridership from 2013–2015 (excluding 2016 for accuracy) and the average monthly ridership per year (including 2016).
* Fare Type Distribution: The percentage distribution of ridership across various fare types for the entire period (2013–2016) was calculated and then visually represented using a pie chart.

### Output Analysis:
### Total Monthly Bus Ridership (2013–2016)
This line graph visualizes the fluctuations in total bus ridership on a monthly basis from January 2013 to December 2016. We can observe seasonal patterns, typically with higher ridership in certain months of the year, and an overall trend in ridership over the four-year period.

![Bus Ridership Data Graph](/images/Bus_ridership_data_graph.png)

## Part 2: SCT’s Performance Measures and Operational Characteristics (2013–2023)
Data for this section was imported from the Federal Transit Administration (FTA), and we then extracted the relevant SCT records. This part of our analysis focuses on key performance indicators (KPIs) and operational characteristics of the transit system from 2013 to 2023. We aim to understand efficiency, productivity, and fleet health over time.
This segment of the analysis focuses on loading, cleaning, and deriving key performance indicators (KPIs) from national-level transit data.
### Performance Measures
![Graph of Performance Measures](/images/Performance_measures.png)
### Operational Charateristics
![Graph of OE](/images/OE.png)

## Part 3: SCT Bus Route Analysis, GIS Visualization, and Social Demographic Impact
![Map of Hamlets](/images/hamlets.png)

I consider this part the heart of the project, as I wanted to achieve a truly perfect visualization, moving beyond regular maps and random dots. Therefore, I took a significant step by opting to visualize SCT’s structure and Suffolk’s demographics in QGIS

![QGIS](/images/Qgis 2.png)

### Route Analysis
This segment of our analysis delves into the performance and characteristics of bus routes, linking them to demographic data, specifically poverty rates in Suffolk County. This helps us evaluate if service provision aligns with community needs.
This Python script uses pandas and geopandas for data manipulation, shapely for geometric operations, and matplotlib/seaborn for visualization.
First, the script handles data loading and preprocessing. It loads GTFS (General Transit Feed Specification) data files, which include routes.txt, trips.txt, shapes.txt, stop_times.txt, and stops.txt. Additionally, it loads geospatial data for New York Census Tracts from tl_2024_36_tract.shp and attribute data (population and poverty) from ACS CSV files. The script then filters these to include only Suffolk County tracts, and calculates poverty rates per tract.

![Route Graph](/images/route.png)

Next, the script processes route-level metrics. It uses the shapes.txt data to create LineString geometries for each unique route shape. These geometries are reprojected for accurate length calculations in kilometers. The total trips and unique stops for each route are calculated from trips.txt and stop_times.txt respectively, and these metrics are merged into the main routes analysis DataFrame. This DataFrame is then prepared for spatial analysis, with bus stops converted into a GeoDataFrame, which is subsequently spatially joined to census tracts to enrich stop data with poverty rates.

![QGIS Map](/images/Qgis.png)

Finally, the script performs quantitative analysis and generates visualizations. It calculates the average poverty rate for each route based on its stops’ poverty rates, merging this data into the final analysis DataFrame. The script then generates two key visualizations: a scatter plot comparing route frequency (total trips) with the average poverty rate of its stops, and a categorized box plot showing route frequency distribution across poverty quartiles. These visualizations allow for a clear assessment of service distribution relative to socio-economic indicators.

## Conclusion
In essence, these insights paint a picture of SCT’s potential role in promoting equity. The data indicates that residents in Suffolk County’s higher-poverty areas likely have reasonable access to bus services, as evidenced by trip frequencies that meet or exceed the system’s average. This suggests a foundational level of transit accessibility in communities that may rely on public transport for essential daily activities, thereby contributing to social equity within the county.

Our analysis ultimately confirmed that Suffolk County Transit effectively provides service coverage within Suffolk, the region’s largest easternmost county—a finding both curiously insightful and thankfully reassuring. 

If you want know about this project in great detail, please follow up on this medium link
"https://medium.com/@vummadiharsha123/summer-project-1-analyzing-suffolk-county-transit-with-qgis-python-9482692bbb80"













