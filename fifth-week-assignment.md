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

#### Manually group Foursquare's venues categories found in New York City and Toronto

The Venue Category data extracted with the Foursquare API is very granular, to facilitate the visualization of data the 334 unique types of venues in Toronto and the 466 unique types of venues in New York City will be grouped into eight larger categories:

 <ul>
  <li>Bars and Clubs</li>
  <li>Restaurants</li>
  <li>General Services</li>
  <li>Leisure & Sports</li>
  <li>Culture & Education</li>
  <li>Parks & Nature</li>
  <li>Transportation Infrastructure</li>
  <li>Residential</li>
</ul> 

In the image below we can see the number of subcategories inside each larger one. This classification was made by hand, as the Foursquare API do not provide hierarchical category information.

<a href="https://i.imgur.com/8t4pEhs.png">
  <img src="https://i.imgur.com/8t4pEhs.png" alt="img1">
</a>

As it can be noted, New York City have slightly more variety of venues than Toronto. This is expected as the population in New York City is much larger than in Toronto, and also the number of neighborhoods.

#### Data Encoding

The next important step is the preparation of the data for the clustering/classification algorithms we are going to use later. Usually, only numeric inputs are valid in these algorithms, so in this section of our Jupyter Notebook the dataframes with venue data collected and classified so far is encoded, creating a bigger dataframe following the model in the picture below:

<a href="https://i.imgur.com/rko7EOJ.png">
  <img src="https://i.imgur.com/rko7EOJ.png" alt="img2">
</a>

This data is then grouped for each Neighborhood, resulting in a dataframe with the number of venues in each category for each neighborhood. With this data prepared, we can generate several rich visualizations about the statistical venue makeup of New York and Toronto.

#### Understanding the Data Collected so Far

In this section we list some visualizations and distributions relevants to the topic of this work. First, a bar chart about the number of venues collected for each neighborhood and the correspondent distribution of neighborhoods based on the number of venues collected.

<a href="https://i.imgur.com/Ht2pYOK.png">
  <img src="https://i.imgur.com/Ht2pYOK.png" alt="img2">
</a>

<a href="https://i.imgur.com/halmwux.png">
  <img src="https://i.imgur.com/halmwux.png" alt="img2">
</a>

As it can be noted, New York City have several neighborhoods with "100" venues. A curious detail is the fact that for some reason the Foursquare API returned only 100 venues for each neighborhood, even after declaring expicitly that we wanted 200 in the API request. Nevertheless, several neighborhoods do not have more than one hundred venues returned and this won't be a big problem for our objectives.

##### Restaurants Distribution in Each City

Repeating the plots but only considering venues of the "Restaurant" category, we can have an idea about the number of these types of business in each city and also their distribution between different neighborhoods. Both cities have some neighborhoods with several restaurants, indicating that there are agglomerations of business of the same kind at certain locations that will be further studied.

<a href="https://i.imgur.com/OOBMQCT.png">
  <img src="https://i.imgur.com/OOBMQCT.png" alt="img2">
</a>

<a href="https://i.imgur.com/qbgJfiS.png">
  <img src="https://i.imgur.com/qbgJfiS.png" alt="img2">
</a>

Comparing both distributions we can conclude that the restaurant business in New York City is much more saturated than in Toronto, as only few neighborhoods have been "taken" by these establishments.

<a href="https://i.imgur.com/6xG4uJB.png">
  <img src="https://i.imgur.com/6xG4uJB.png" alt="img2">
</a>

##### Bars and Clubs Distribution in Each City

The Bars and Clubs distribution are much more different between Toronto and NYC. In NYC this kind of business seems also saturated, with lots of places distributed between several neighborhoods, while in Toronto there are much more inequality in bars and clubs distribution between the neighborhoods - In Toronto this kind of business is concentrated in few neighborhoods.

<a href="https://i.imgur.com/PwujFnn.png">
  <img src="https://i.imgur.com/PwujFnn.png" alt="img2">
</a>

##### General Services Distribution in Each City

The general services distribution is somewhat similar between the two cities, but still following the same pattern than the previous ones - New York seems more saturated while in Toronto some neighborhoods have a deficiency of services.

<a href="https://i.imgur.com/PLvEVIj.png">
  <img src="https://i.imgur.com/PLvEVIj.png" alt="img2">
</a>

#### Neighborhood K-Means Clustering based on Mean Ocurrence of Each Venue Category

With the previously encoded data, we will now aim to cluster the neighborhoods into five clusters, each one with different major characteristics. K-means clustering is the algorithm that will be used - this algorithm aims to partition n observations into k clusters in which each observation belongs to the cluster with the nearest mean. K-Means uses an iterative refinement technique, and it is also referred to as Lloyd's algorithm. In the next pictures we show how the five clusters are characterised, in terms of median percent share of each kind of neighborhood.



## Results
results discussion

## Conclusion
blablabla
