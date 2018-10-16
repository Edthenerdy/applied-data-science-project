# Fifth Week Assignment – The Battle of the Neighborhoods - Final Report


## Introduction & Business Problem:
This work will be focused on creating and visualizing neighborhood's profiles, more specifically neighborhoods localized in boroughs in Toronto and New York City. These profiles will be based on the numbers and categories of venues present in each neighborhood in these cities, classifying each neighborhood based on statistical data and automated analysis using classification algorithms. Hopefully, these city profiles can give valuable insights about the life and economy of each region, making possible better-informed decision making for business and better public policymaking. Naturally, the target audience of this work are urban planners, policymakers, or urban services business looking to expand. This work is an extrapolation of the idea suggested in the assignment instructions.

The main business problem attacked in this work is based on how to determine the optimum location for a new business – a restaurant, bar, or office building. This problem can be solved by means of inferred data about already existing business. Naturally certain types of enterprises tend to be built in the same areas, through economic incentive or public regulations. Data about venue category density in a neighborhood can provide valuable information about probable new markets or regions with low offerings in certain types of service. It is important to also mention that the inexistence of certain types of enterprises can also mean that there is no demand for their services, indicating that just data about venues, without additional socioeconomic information about the regions, is not sufficient data for constructing a complete picture. Nevertheless, it is possible to construct robust profiles about the urban makeup of the cities, sufficient for kickstarting the plans for new business, and this will be our main goal.

## What will be used: Data & Tools
Two cities will be analyzed in this work: Toronto and New York City. The boroughs and neighborhoods names and postal information from Toronto are extracted from a Wikipedia article¹, and the same data for New York City is provided by the course in previous assignments in a JSON file². With this information at hands, the Google Geocoder API can be used to extract geographical coordinates of each neighborhood using their names and postcode as input. The coordinates will be utilized for map generation, and as input for the Foursquare API, that will be leveraged to provision venues information for each neighborhood. A sample of the venue data extracted with Foursquare API calls is showed in the picture below.

<a href="https://i.imgur.com/MOxxyoY.png ">
  <img src="https://i.imgur.com/MOxxyoY.png" alt="Data Sample">
</a>

We will focus on the venue category parameter, refining and clustering different categories of venues in major groups that will facilitate the analysis and also make possible the generation of better visualizations. Clustering algorithms like K-Means will be used to automatically group the neighborhoods in similar groups. Plotly, Seaborn and Folium Python packages are used for data rendering and visualization, providing rich graphs and maps.

[1] https://en.wikipedia.org/wiki/List_of_postal_codes_of_Canada:_M

[2] https://ibm.box.com/shared/static/fbpwbovar7lf8p5sgddm06cgipa2rxpe.json

## Methodology 
### Stage 1 - Business Understanding
As stated in the previous section of this report, our main goal is to create a reliable profile of the neighborhoods in New York City and Toronto. Our fictional business sponsors are two entrepeneurs, one looking to open a new restaurant in New York City and another one looking to open a new bar in Toronto.
### Stage 2 - Analytic Approach
To decide the ideal neighborhood for the new business, we must classify the neighborhoods into three main different kinds of regions based on the proportion of venue categories present in each one: 
1 - Residential
2 - Services
3 - "Going Out"
After the necessary data preparation (collection, encoding and normalization) the neighborhoods will be clustered into three groups using the k-means clustering algorithm. To solve our business problem, the third cluster "Going Out" will be further studied, and the venue categories in these neighborhoods in this group will be expanded, to give insight in the kinds of places that do not already exist in these neighborhoods. The information can help our business sponsors decide what kind of restaurant or bar are lacking and are probbable bunsiness opportunities.
### Stage 3 - Data Requirements
As stated in the Data & Tools section, the data requirements for this research are the venue information for each neighborhood in Toronto and New York City. Consequently, information about the neighborhoods (names and geographical coordinates) are also necessary.
### Stage 4 & 5 - Data Collection & Understanding
The required data is collected in the first parts of the Jupyter Notebook. Toronto boroughs and neighborhoods are scrapped from the wikipedia link in [1] using the BeautifulSoup package, and the New York City boroughs and neighborhoods information is scrapped from the JSON file provided in [2].
Then, with the neighborhood and borough names, and using the Google Geocode API, we extract the geographical coordinates of each neighborhood. At this point the data is organized in a Pandas DataFrame like the following:

<a href="https://i.imgur.com/wSKFCbb.png ">
  <img src="https://i.imgur.com/wSKFCbb.png" alt="Data Sample 2">
</a>

The "New York City, NY" dataframe has 5 boroughs and 302 neighborhoods, and the "Toronto, ON" dataframe has 11 boroughs and 210 neighborhoods. With the data collected at this point we can already visualize geographically each neighborhood using the Folium package to generate interactive Leaflet maps.

#### New York Neighborhoods Visualization
<a href="https://i.imgur.com/rPCQob4.png ">
  <img src="https://i.imgur.com/rPCQob4.png" alt="New York">
</a>

#### Toronto Neighborhoods Visualization
<a href="https://i.imgur.com/HnWkoig.png ">
  <img src="https://i.imgur.com/HnWkoig.png" alt="Toronto">
</a>

Departing from the same DataFrame, we now use the Foursquare API to collect venue data. Using the geographical coordinates of each neighborhood, API calls are made requesting the top 200 venues in a radius of 1000 meters. The results are inserted in a new pandas dataframe, as presented in the following picture.

<a href="https://i.imgur.com/e3pwKTw.png ">
  <img src="https://i.imgur.com/e3pwKTw.png" alt="Data Sample 3">
</a>

We generate geographical visualizations of the venue data as well, presented below in red dots. The "ny_venues" dataframe has 20537 venues and 466 unique venue types, and the "to_venues" dataframe has 9306 venues and 334 unique venue types. The proportion in number of venues are expected, considering the population and population density of these two cities.

#### New York Venues Visualization
<a href="https://i.imgur.com/dRJJXBE.png ">
  <img src="https://i.imgur.com/dRJJXBE.png" alt="New York venues">
</a>

#### Toronto Venues Visualization
<a href="https://i.imgur.com/COS36wu.png ">
  <img src="https://i.imgur.com/COS36wu.png" alt="Toronto venues">
</a>

## Results
results discussion

## Conclusion
blablabla
