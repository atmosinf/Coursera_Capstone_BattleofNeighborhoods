# The Battle of the Neighborhoods - Open an Arcade in Manhattan
----
<span style="color:#3771a3">Amoel Geogy</span> <br>
<span style="color:#6da178;font-size:80%">July 23, 2021</span>


This is the Capstone project to complete the [IBM Data Science Professional Course](https://www.coursera.org/professional-certificates/ibm-data-science) on Coursera. In this course (which consisted of 9 separate sub-courses) we learned about certain topics like Data Science Methodology, Data Analysis, Data Visualization, connecting to databases and using SQL in Jupyter notebooks and Machine Learning with Python. In this project we will use the skills we acquired to solve a business problem.

----

## 1. Introduction - Business Problem
Our client wants to open an arcade in Manhattan. He has been to almost much all the arcades in Manhattan, but he does not find any of them satisfactory. Being an 80s kid, he lived through the golden age of arcades, and he wants to open one that will satisfy his nostalgia, and show the kids how it really used to be. 

The target audience will mostly be early teenagers to young adults. We would need to find the neighborhoods in Manhattan where the density of this crowd is high. It would make sense to search for areas which have many universities or schools.


## 2. Data
Based on this business problem, we can identify that we need data such as:
* locations of existing arcades
* locations of schools, universities and colleges
* geographical data like the coordinates and areas of each neighborhood in Manhattan

To get the locations of arcades and the academic institutions, we will use the [Foursquare API](https://developer.foursquare.com/docs/). We will use the categoryids provided in the Foursquare [website](https://developer.foursquare.com/docs/build-with-foursquare/categories/) to search for the data of Arcades and College & Universities. We will retrieve the Name, Latitude, Longitude and Category of these locations.

To get the neighborhood boudaries, we will use the geojson file from this [github repository](https://github.com/blackmad/neighborhoods/blob/master/manhattan.geojson). Furthermore, we will use the [geopy.geocoders](https://geopy.readthedocs.io/) module for the coordinates of the neighborhoods. 

We will use the location data to visualize the places on a folium map. We will use the visualizations to analyse the data and find points of interest. Finally we will use a density clustering algorithm (DBSCAN) to find the areas with the most universities and the least arcades. This would be the location where we might propose to the client to open his Arcade.

We plotted the Categories of the results in a bar graph. This allowed us to see that we have unwanted categories in the dataset (like Bar, Museum, etc), and we will filter them out later.

<img src="arcade_bargraph_snip.PNG" alt="arcade categories">


**Feature Selection:**<br>
For both the Arcade and University data, we have selected the Name, Latitude, Longitude and Category as the features to keep. We have dropped the other features.

Arcades:<br>
<img src="arcadedf_snip.PNG" alt="arcade dataframe">

Universities:<br>
<img src="unidf_snip.PNG" alt="university dataframe">

We then plotted the results using the folium library.

**Manhattan neighborhoods**<br>
<iframe src="man_neigh_map.html" height="500" width="700">
<br>  
  
**Universities and Arcades in Manhattan**
<iframe src="unimap.html" height="500" width="700">
  
  
## 3. Methodology<br>
We used the location data to find the location with the highest density of Universities. To find this cluster, we will use the DBSCAN (Density Based Spatial Clustering of Applications with Noise).
Using recursion, we will use the optimal value of epsilon and choose the min_samples to be = 5. Finally, we will plot the different clusters in different colors and identify the cluster with the highest density. If the number of arcades near this cluster is low, we will find the optimal spot to be near that area.

## 4. Analysis <br>
  
<iframe src="unimap.html" height="500" width="700">
<br>
We can see in the output of the DBSCAN clustering algorithm above that the cluster in pink seems to be the densest cluster. We will perform further analysis by adding the arcades back to the map. 
  
## 5. Results and Discussion
  
During the visualization of the data, we found that the northern part of Manhattan had only one arcade. When we plotted the data, we also saw that the density of Universities in the northern part (neighborhoods of Morningside Heights and Harlem) is quite high. This already looks quite promising.
After running a simple DBSCAN on the university locations, we found that indeed, the highest density was to the north of Central Park (colored in green), and the second densest cluster was in the south of Central Park (colored in green). Furthermore, the northern part has fewer arcades than the southern part of the borough.

## 6. Conclusion
  
<iframe src="finalmap.html" height="500" width="700">
<br>
Using the visualizations, analysis and the results of our clustering model, we can conclude that the ideal location to open an arcade would be just to the south of Morningside Heights. We have found this spot to be in the neighborhood of Upper West Side, in Bloomingdale. The area is marked by a blue circle in the final visualization. We can expect the students of Columbia University to start using this arcade when it is open.


