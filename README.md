# dhcs-IMDB

### About  the Project
The cultural area we decided to focus on is the Film industry, mainly due to our mutual passion and overall 'geekiness' towards movies and cinema, and our curiosity considering trends throughout the history of popular cinema.

We set to explore those trends using data from the largest online movie database – www.IMDB.com.
But first we had to raise a question - how can we define ‘popular cinema’?

We decided to tackle this question by accessing only the IMDb ‘Top 1000’ movies, which are actually the 1000 movies with the highest IMDb rating. In other words, IMDb's 1000 most popular movies.

By extracting pieces of data for each movie on that list: rating, metascore, year, country, budget, gross, and more…
we are able to better understand the answer to the question:
 
‘Can we establish relationships among the various technical aspects of the Film industry, as we focus on its the most popular products?’

The ‘Visual’ tab contains numerous interactive graphs that show the different trends explored. See changes in popularity, budgets, award wins, genres and more... 
 
The ‘Map’ tab contains and interactive map that matches a movie title to its production country. Select a marker to see its title.
 
The ‘Database’ tab contains a table showing our entire movie collection, sorted by Rank. 

### Creation Process
1.    Gathering the data:

  Using a python library called ‘Selenium’, we were able to set up a demo-browser (using chrome webdriver) and access the ‘IMDb Top 1000’ page.

  For each movie appearing in the list, we used the proper HTML attributes the extract the wanted data: title, year, rating, metascore, gross and hyperlink to the movie’s own page, and identified the ‘Next’ button HTML attribute to have Selenium redirect to the next page containing the rest of the list.


  Then, realizing we need more data, we used the hyperlinks obtained to access each of the movie’s own page and scrap more data for each movie: country, genre, budget, awards, and duration.

  The data was saved as a CSV file using the python library ‘Pandas’.

2.    Cleaning the data:

  The cleaning actually happened during the previous phase. Before saving the data to the CSV, we had to perform the following corrections:

  - We relied heavily on an attribute called ‘Metascore’. The IMDb score is generated by the IMDb users' ratings while the Metascore ratings are the scores from the website Metacritic.com, written by professional critics. This allows us to say that the user’s ratings shows popularity while the metascore is more of an indication for the movie’s quality. Therefore, we filtered out all movies that didn’t have a Metascore, leaving us with 678 movies.

  - The budget for each movie was written with a different currency that matches the movie’s production country, and the amount was written with comma separation. We had to make sure the budgets can be compared. Therefore, we converted each budget to a USD budget using a python library ‘CurrencyConverter’, and removed commas.

  - The awards were given as a text whose format was one of the following: "x wins & y nominations.", "x nomination.", "Won x Oscars.", or "Nominated for X Oscars/Golden Globe/BAFTA."
  
  3.    Data presentation:
 

    We created the graphs using a software called ‘Tableau’, which was initially pretty difficult to master. Tableau received our CSV as input, and automatically categorized our columns into dimension and measures. Our graphs were created by crossing a dimension with measure, or multiple measures.

    We had a problem when trying to present a graph showing the most common genre. Each movie doesn’t belong to just one genre, but mostly 2 or 3 genres. First, we had to separate the genre column, which was formatted in the following way: “genre1, genre2, genre3”, into 3 columns.

    Then, we had to find a way to count the total occurrences of a genre which was a bit problematic. Eventually, we had to create a measure field for every genre which was based on the following calculation:    

    COUNT( IF CONTAINS([Genre1],<target_genre>) then 1 END)+

    COUNT( IF CONTAINS([Genre2],<target_genre>) then 1 END)+

    COUNT( IF CONTAINS([Genre3],<target_genre>) then 1 END)


    The map was created using Google Maps. We created CSV containing only the title and country columns. Then, we created a map within Google Maps, and imported the csv to receive the map showing all movie locations. Then, we added the embedded HTML to our website.
        Using string manipulations, we were able to receive the total amount of wins and nominations for each movies, saved as 2 different columns in the CSV.
