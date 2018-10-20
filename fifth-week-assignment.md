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

## Results

### Neighborhood K-Means Clustering based on Mean Ocurrence of Each Venue Category

With the previously encoded data, we will now aim to cluster the neighborhoods into five clusters, each one with different major characteristics. K-means clustering is the algorithm that will be used - this algorithm aims to partition n observations into k clusters in which each observation belongs to the cluster with the nearest mean. K-Means uses an iterative refinement technique, and it is also referred to as Lloyd's algorithm. In the next pictures we show how the five clusters are characterised, in terms of median percent share of each kind of neighborhood.

#### Clusters in Toronto

The Toronto city clusters are presented below.

<a href="https://i.imgur.com/h6iI4yj.png">
  <img src="https://i.imgur.com/h6iI4yj.png" alt="img2">
</a>

Cluster 0 aggregates neighborhoods with a a huge proportion of restaurants, followed by bars and then services. The parks and nature proportiona share in this cluster is higher than similar clusters in New York, indicating few residential venues like closed residential buildings, and bigger parks and florested areas (as is expected in some parts of Toronto than in an urban sprawl like NYC).

Cluster 1 aggregates neighborhoods with a huge proportional share of services (more than 50%!) indicating that neighborhoods classified in this cluster probably are commercial districts or city centers.

Cluster 2 aggregates neighborhoods with a high prevalence of parks and nature, and also transportation infrastructure. There are services, restaurants and bars but they aren't a common occurence in these areas. Here we also have the neighborhoods with the highest proportional share of leisure, education, cultural, and sports venues (probably indicating some kind of university presence).

Cluster 3 aggregates neighborhoods with balanced shares of restaurants, bars, clubs and leisure. This cluster also has the lowest parks and nature proportional share, indicating that neighborhoods in these areas are highly urbanized parts of the city, indicating high development.

Cluster 4 aggregates the highest proportional share of bars and clubs in Toronto, indicating that these regions for some reason are attracting business related to nightlife and food. This cluster will be further analysed to answer our specified business problem.

In the map below we can see the geographical visualization of the different types of clusters created using K-Means for Toronto. The colors indicate the biggest proportional share of venue category (using the same legend from the pie charts, except for the red one that indicate the balanced Cluster 3).

<a href="https://i.imgur.com/9IciPnZ.png">
  <img src="https://i.imgur.com/9IciPnZ.png" alt="img2">
</a>

#### Clusters in New York City

The New York City clusters are presented below.

<a href="https://i.imgur.com/lTbor6T.png">
  <img src="https://i.imgur.com/lTbor6T.png" alt="img2">
</a>

Cluster 0 aggregates neighborhoods with a near equal rate of restaurants, bars, and services venues, It is similar to Cluster 4 in the sense that the proportions are similar between these same three venue categories, except Cluster 4 have a bigger proportion of leisure, sports and cultural venues (probably indicating universities and schools present).

Cluster 1 aggregates neighborhoods with a high prevalence of parks and nature, and also transportation infrastructure. There are services, restaurants and bars but they aren't a common occurence in these areas.

Cluster 2 aggregates neighborhoods with a huge proportion of services, followed by restaurants and bars, indicating that these neighborhoods are probably commercial districts or city centers.

Cluster 3 aggregates the largest proportion of restaurants and bars of all clusters, meaning that neighborhoods grouped in this cluster are important entities of study for our business problem related to restaurants and bars distribution.

In the map below we can see the geographical visualization of the different types of clusters created using K-Means for New York City.
The colors indicate the biggest proportional share of venue category (using the same legend from the pie charts, except for the yellow one that indicate Cluster 4).

<a href="https://i.imgur.com/aBcXbkQ.png">
  <img src="https://i.imgur.com/aBcXbkQ.png" alt="img2">
</a>

After the study of the data presented, we selected some clusters of interest in each city.

### Toronto Analysis

For Toronto, we selected the clusters 3 and 4. The cluster 4 aggregates neighborhoods with high numbers of bars and good demand and accessibility for the public (suburban areas), indicating places with lower rents and property prices - relative to city center neighborhoods, of the also selected cluster 3. Cluster 3 groups the more urbanized and developed parts of Toronto, with several services category venues - making these areas great neighborhoods with high demand for restaurants, bars, nightclubs, etc. The list of neighborhoods in this cluster is presented below, and they basically form a list of places with well established business in the restaurant/bar/clubs segment. The optimal location for a new business in the restaurant or bar category can be further studied with the granular data about the specific themes of restaurants and bars. High demand signals high offerings and also higher competitivity, meaning that it's probably better to start a "new" kind of venue, in an untapped market in an underdeveloped or suburban area.

#### Good neighborhoods for establishing new restaurant venues in Toronto (possible untapped markets):

Richview Gardens, Roselawn, Rouge, Royal York South West, Scarborough Town Centre, Silverstone, Parkview Hill, Mimico NW, Mount Olive, Oriole, Maryvale, South Steeles, Wexford Heights, Wilson Heights, Woodbine Gardens, York Mills West, Wexford, Thorncliffe Park, Thistletown, South of Bloor, St. Phillips, Steeles West, The Beaches West, The Queensway West, Martin Grove Gardens, Cliffside West, Downsview North, Downsview Northwest, Downsview West, East Birchmount Park, Dorset Park, Albion Gardens, Bathurst Manor, Beaumond Heights, Bedford Park, Birch Cliff, Caledonia-Fairbanks, Cedarbrae, Jamestown, Kennedy Park, Kingsview Village, Kingsway Park South West, L'Amoreaux West, Lawrence Heights, Lawrence Manor, Lawrence Manor East, Leaside, Malvern, Ionview, India Bazaar, Glencairn, Henry Farm, Hillcrest Village, Humbergate, Fairview

#### Good neighborhoods for restaurant venues in Toronto (but probably saturated markets):

Railway Lands, Silver Hills, York Mills, South Niagara, Bathurst Quay, CN Tower, King and Spadina, Lawrence Park, Island airport, Harbourfront West

### New York City Analysis

For NYC, we selected the clusters 0 and 4. The cluster 4 aggregates neighborhoods with high but balanced proportions of services, restaurants, and bars/clubs. Comparing cluster 4 with cluster 0, that aggregates city center neighborhoods with very high proportional share of restaurants and also relatively high proportion of services, we can notice that cluster 4 is behind cluster 0 in the gentrification, or urban development process. This information can be used to plan the best locations for a restaurant business based on the intentions of our business sponsor: does he want to open a restaurant in some place with high demand, but also high price of entry or he wants to bet in a place with less entrenched competitiors and also good demand? We list the possible neighborhoods for each group in the next subsection.

#### Good neighborhoods for establishing new restaurant venues in NYC (not so much competition and good demand - "safe bets"):

Oakland Gardens, North Side, North Riverdale, North Corona, Noho, Prospect Heights, Pelham Parkway, New Brighton, Murray Hill, Manhattanville, Manhattan Valley, Manhattan Beach, Lower East Side, Murray Hill, Morningside Heights, Midtown South, Ravenswood, Upper West Side, Turtle Bay, Tudor City, Tottenville, Throgs Neck, Sunnyside Gardens, Williamsburg, Whitestone, West Village, West Brighton, Sunnyside, Stuyvesant Town, Roosevelt Island, Rockaway Beach, Riverdale, Ridgewood, Schuylerville, Sheepshead Bay, Steinway, South Side, South Ozone Park, City Island, Chinatown, Central Harlem, Bushwick, Clifton, Clinton Hill, Bayside, Bay Ridge, Astoria, Annadale, Bedford Stuyvesant, Briarwood, Bergen Beach, Woodside, Hamilton Heights, Great Kills, Gramercy, Kingsbridge, Jackson Heights, Inwood, Hunters Point, Elmhurst, Edgewater Park, East Village, East Harlem, Fieldston, Fort Hamilton, Fort Greene, Forest Hills Gardens, Flushing, Flatbush, Yorkville

#### Good neighborhoods for establishing new clubs and bars in NYC (not so much competition and good demand - "safe bets"):

Ozone Park, New Springville, New Dorp Beach, New Dorp, Queens Village, Pleasant Plains, Malba, Lindenwood, Marine Park,  Mount Hope, Morrisania, Mill Basin, Middle Village, Maspeth, Westerleigh, Rosedale, Richmond Valley, Sea Gate, Starrett City, South Jamaica, Soundview, Lefrak City, Charleston, Castle Hill, Co-op City, Baychester, Bay Terrace, Arlington, Bellerose, Bloomfield, Heartland Village, Holliswood, Hunts Point, Glendale, Elm Park, Eastchester, East Flatbush, Erasmus, Georgetown, Floral Park

#### Good neighborhoods for restaurant venues in NYC (but probably saturated markets - entrenched business):

Allerton, Olinville, Old Town, Ocean Parkway, Ocean Hill, Norwood, New Lots, Paerdegat Basin, Park Hill, Parkchester, Queensboro Hill, Prospect Park South, Prospect Lefferts Gardens, Prince's Bay, Port Richmond, Park Slope, Manhattan Terrace, Madison, Longwood, Little Neck, Mariner's Harbor, Melrose, Mount Eden, Mott Haven, Morris Park, Midwood, Rego Park, Utopia, University Heights, Unionport, Tribeca, Sutton Place, Sunset Park, Washington Heights, Woodhaven, Williamsbridge, Westchester Square, Weeksville, Wakefield, Rugby, Rosebank, Rochdale, Richmond Hill, Remsen Village, St. Albans, Spuyten Duyvil, Soho, Laurelton, City Line, Canarsie, Cambria Heights, Civic Center, Dongan Hills, Ditmas Park, Cypress Hills, Corona, Concord, College Point, Brownsville, Bay Terrace, Bath Beach, Auburndale, Bayswater, Bronxdale, Borough Park, Douglaston, Bensonhurst, Belmont, Bellaire, Hillcrest, Highland Park, Greenwich Village, Greenridge, Grasmere, Grant City, Graniteville, Hollis, Howard Beach, Kew Gardens Hills, Kensington, Jamaica Hills, Jamaica Estates, Jamaica Center, Homecrest, Glen Oaks, Eltingville, Edenwald, East Tremont, East New York, Far Rockaway, Fresh Meadows, Fordham, Flatlands, Flatiron, Forest Hills

### Refining the results

From all the cities listed above, we can interact with the charts generated with Plotly in the Jupyter Notebook of this project and analyze the absolute number of restaurants and bars. Assuming that fewer restaurants are indicative of possible market opportunities we can refine the lists of clustered neighborhoods provided above:

#### Best Neighborhoods for Restaurants in Toronto

CN Tower, Lawrence Park, Mimico NW, Mount Olive, L'Amoreaux West, Fairview, St. Phillips, Royal York South West, Scarborough Town Centre.

#### Best Neighborhoods for Restaurants in NYC

Ozone Park,  Queens Village, Charleston, Old Town, Ocean Parkway, and Forest Hills.

## Conclusion

We finish this report with the conclusions of the study: a lot of assumptions are made to arrive at the final refined results. These assumptions can probably be wrong, and further study with more data must be taken to verify the quality of, or if any of the correlations really exist. Nevertheless our assumptions are simple and seem to be right: if there is a lot of restaurants in some area, it is probably because exists demand in this place. However, the market can also be saturated, or a very expensive area - considerations that our business sponsor must take into account when deciding where he will open his new restaurant. Because of these doubts, we researched two main types of neighborhoods: neighborhoods with high concentration of restaurant business (high competitivity) and also neighborhoods with good number of restaurants (indicating that some kind of demand exists) but not so many restaurants to make competition a problem. 

The business sponsor can safely choose one of the neighborhoods listed as best. For a more comprehensive decision, the specific venue type (if it is a brazilian restaurant, or persian one, etc.) can be checked - and the venue with the lowest competition can be chosen accordingly.
