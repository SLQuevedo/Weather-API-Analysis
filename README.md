# python-api-challenge

# WeatherPy
# Opening the Project
Inside the WeatherPy folder there is a file called WeatherPy.ipynb, please open this file with Jupyter Notebook. I will explain each part of my code as they appear in this ReadMe file. My code is annotated so please reference it as you see fit. If you wish to run this code you must provide your own API key for OpenWeatherMaps and have citipy installed. 

# Obtaining Data
To get the cities I used to provided code. The code randomly generates latitude and longitude coordinates and then it uses these coordinates to find the closest city with the citipy nearest city method. Using an if statement we check to make sure that we don't add any duplicate cities to our list.

Now that we have our sufficiently large (at least 500) list of cities we use the OpenWeatherMap API to get our current weather data. We start by building our query url by using the the base url from OpenWeather, our API key and the units. I went with celsius. I create an empty dictionary that will hold all of our data for each city. I can now create a for loop that goes through my list of cities and gathers data from OpenWeather. I use an if statement to check to see if the city is in the database, so that my code doesn't break. I could have also done a try + except statement. A line for each city is printed when it is being processed and put into our dictionary. 

# Converting and Cleaning Data
With the dictionary of city data we are able to convert it into a dataframe and put it into a csv file. I perform an aggregation to see if there are any data points that are unusable. For example if I had a maximum value of 185 in our longitude column, I would have to perform a .loc to remove those data points. In our case we only had to make sure that our humidity was no greater than 100. Luckily we had no incorrect values so our data is ready to go. 

I have provided some commented out code to show what the cleaning process would look like. 

# Plotting the Data by City Latitude
I put my data for city latitude and temperature into a scatter plot. I then save this result as a png file that can be viewed in the "output_data" folder. 

For the next graph, I put my data in for city latitude and humidity into a scatter plot. I save the result in the "output_data" folder.

I do the same for city latitude vs cloudiness and city latitude vs wind speed.

# Linear Regression by Hemisphere
First I filter my data to get cities in the northern and southern hemisphere. I accomplish this by finding cities with a latitude greater than 0 for Northern hemisphere cities and finding cities with a latitude less than 0 for Southern hemisphere cities. I make sure to check the min and max of my newly filtered data to make sure I don't have any negative or positive values respectively. I was curious about how many cities we had for each hemisphere and checked that as well.

For the cities in the Northern hemisphere I create graphs for max temp vs latitude, humidity vs latitude, cloudiness vs latitude, and wind speed vs latitude. I apply a regression to each of these graphs to see if there is a strong correlation between the two parameters. 

I do the same for Southern hemisphere cities.


# Findings
Based off our graphs it seems that latidute has a strong correlation to the maximum temperature for the Northern and Southern hemispheres. For both the Northern and Southern hemisphere the temperature rises as the latitude gets closer to the equator. We can conclude that warmer temperatures are near the equator. Latitude didn't have a strong correlation to humidity, cloudiness or windspeed. I think it would be interesting to investigate these three aspects to see if there is any correlation between them. I noticed that between the Northern and Southern hemisphere graphs for wind speed vs latitude they looked similar. I calculated the mean, median, sem, var and standard deviation of each hemispheres wind speed and found that the values were similar. I think this strengthens the observation that there is not correlation between latitude and wind speed.  

# VacationPy
# Opening the Project
Inside the VacationPy folder there is a file called VacationPy.ipynb, please open this file with Jupyter Notebook. I will explain each part of my code as they appear in this ReadMe file. My code is annotated so please reference it as you see fit. If you wish to run this code you must provide your own API key for GoogleMaps. *You must run WeatherPy.ipynb before running this file.*

# Heatmap
First I configure gmaps and then I plot a heatmap based off location and humidity. 

# Filtering Data
I filter my weather data by temperatures less than 26.6667 celsius and greater than 21.1111 celsius first. Then I filter by wind speeds less than 10 mph and with cloudiness at 0%. I check to make sure my filtered data has no null values. If there were null values we would have to drop that data. Luckily, all of our data has values.

# Hotel Map
I rename my filtered weather dataframe to hotel_df. I then set up the variables I will need to construct my query url. The parameter dictionary has a location radius of 5000 meters, type of business is lodging and my google api key. I put my lat/lng parameter inside my loop because this changes with each city. I print out my values as they are being processed with a try/except. I then put markers for the hotels onto the heat map that I made prior. 
