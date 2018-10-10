# First Week Assignment – The Battle of the Neighborhoods

## Introduction & Business Problem:
This work will be focused on creating and visualizing neighborhood's profiles, more specifically neighborhoods localized in boroughs in Toronto and New York City. These profiles will be based on the numbers and categories of venues present in each neighborhood in these cities, classifying each neighborhood based on statistical data and automated analysis using classification algorithms. Hopefully, these city profiles can give valuable insights about the life and economy of each region, making possible better-informed decision making for business and better public policymaking. Naturally, the target audience of this work are urban planners, policymakers, or urban services business looking to expand. This work is an extrapolation of the idea suggested in the assignment instructions.

The main business problem attacked in this work is based on how to determine the optimum location for a new business – a restaurant, bar, or office building. This problem can be solved by means of inferred data about the already existing business. Naturally certain types of enterprises tend to be built in the same areas, through economic incentive or public regulations. Data about venue category density in a neighborhood can provide valuable information about probable new markets or regions with low offerings in certain types of service. It is important to also mention that the inexistence of certain types of enterprises can also mean that there is no demand for their services, indicating that just data about venues, without additional socioeconomic information about the regions, is not sufficient data for constructing a complete picture. Nevertheless, it is possible to construct robust profiles about the urban makeup of the cities, sufficient for kickstarting the plans for new business, and this will be our main goal.

## What will be used: Data & Tools
Two cities will be analyzed in this work: Toronto and New York City. The boroughs and neighborhoods names and postal information from Toronto are extracted from a Wikipedia article¹, and the same data for New York City is provided by the course in previous assignments in a JSON file². With this information at hands, the Google Geocoder API can be used to extract geographical coordinates of each neighborhood using their names and postcode as input. The coordinates will be utilized for map generation, and as input for the Foursquare API, that will be leveraged to provision venues information for each neighborhood. A sample of the venue data extracted with Foursquare API calls is showed in the picture below.

<a href="https://i.imgur.com/MOxxyoY.png ">
  <img src="https://i.imgur.com/MOxxyoY.png" alt="Data Sample">
</a>

We will focus on the venue category parameter, refining and clustering different categories of venues in major groups that will facilitate the analysis and also make possible the generation of better visualizations. Clustering algorithms like K-Means will be used to automatically group the neighborhoods in similar groups. Plotly, Seaborn and Folium Python packages are used for data rendering and visualization, providing rich graphs and maps.

[1] https://en.wikipedia.org/wiki/List_of_postal_codes_of_Canada:_M

[2] https://ibm.box.com/shared/static/fbpwbovar7lf8p5sgddm06cgipa2rxpe.json
