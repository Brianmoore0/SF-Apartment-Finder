# SF-Apartment-Finder
### Purpose
The purpose of this project is to provide new renters and those unfamiliar with the San Francisco real estate market with advanced analytics and resources, allowing them to:

1. **Part 1:** Identify / sort desirable neighborhoods from undesirable neighborhood based on crime and venue data. 
2. Determine if a potential apartment or house is over or underpriced. 

### Data used: 
1. [Craigslist Housing Data](https://sfbay.craigslist.org/d/apts-housing-for-rent/search/apa)
2. [Foursquare Venue Data](https://developer.foursquare.com/)
3. [City of San Francisco Crime Database](https://data.sfgov.org/Public-Safety/Police-Department-Incident-Reports-2018-to-Present/wg3w-h783)
4. [San Fransisco GeoJSON data(to determine neighborhood boundaries)](https://data.sfgov.org/Geographic-Locations-and-Boundaries/Analysis-Neighborhoods/p5b7-5n3h)

### Methodology: 
1. **Part 1.1 (Identifying Low Crime Neighborhoods):** [Police activity data](https://data.sfgov.org/Public-Safety/Police-Department-Incident-Reports-2018-to-Present/wg3w-h783) was gathered from the city of San Francisco and grouped by neighborhood in which a police event took place. This yields a sum of police events by neighborhood. Also, note that data is filtered to show only events taking place between Jan 2020 and Apr 2020. The sorted data was then visualized using the Google Maps API. Based on crime levels alone, it looks like: **Pacific Heights, Height, Noe Valley, and Russian Hill look like great candidates for a safe living environment.**

2. **Part 1.2 (Identifying High Quality Neighborhoods):** By understanding the types and concentrations of venues in each neighborhood (restaurants, parks and other places of interest), we can learn quite alot about the places residents visit outside of school and work. As a result, we should target neighborhoods with high concentrations of venues that provide residents with ample access to venues that promote personal and social wellbeing. Using [Foursquare Venue Data](https://developer.foursquare.com/)100 random venues were gathered for each neighborhood in the city using the Foursquare API. After cleaning the data, the venues were grouped by neighborhood and clustered by the concentration of three types of venues: Parks, Gyms and Coffeeshops using a Kmeans Algorithm. The resulting clusters identify neighborhoods with high concentrations of the venues listed above. 

    Once plotted, I examined the resulting clusters and found that neighborhoods in clusters 1 (purple) and 2 (blue) contained the highest quantities of park venues with adequate densities of gyms as well as coffee shops. Cluster 2 Neighborhoods consisted of: Haight, Twin Peaks, Golden gate park, and Castro/ Upper Market. Cluster 0 Neighborhoods contained: Visitacion Valley, Russian Hill, Presido, and others.

2. **Part 2 (Identifying Under/Overpriced Apartments):** By building a dataset of over 1100 scraped craigslist apartment listings, we can use important features like: square footage (area), number of bedrooms, and location(lat, lon) to identify over/underpriced apartments using a machine learning classifier. Given the four inputs listed above the scraped data is split into test/train subsets and passed to a random forest regressor. After training, all subsequent apartment listings can be run through the model, helping the user understand if the apartment is over or underpriced. 

### Future Directions:  
Given the results of data and models used, I’m confident that it will provide useful results to those looking to lease an apartment in San Francisco. Regardless, I view my attempts here simply as a proof of concept. To take my analysis to the next level, I’ll need to begin with more metrics that signal neighborhood quality. For instance, I’ll need to quantify each neighborhood’s access to public transportation as well as integrate more venue data from Foursquare and other sources. I’ll also need to integrate crime data into the Random Forrest apartment pricing model to more accurately determine how neighborhood data affects apartment pricing. Finally, I’ll need to develop a method to visualize the data concisely in one map to make findings as clear as possible to end users.