# Movie Recommendation System Data Warehouse Project
## About Dataset
This dataset describes 5-star rating and free-text tagging activity from MovieLens, a movie recommendation service. It contains 100836 ratings and 3683 tag applications across 9742 movies. These data were created by 610 users between March 29, 1996 and September 24, 2018. This dataset was generated on September 26, 2018.

Users were selected at random for inclusion. All selected users had rated at least 20 movies. No demographic information is included. Each user is represented by an id, and no other information is provided.

The data are contained in the files links.csv, movies.csv, ratings.csv and tags.csv.

## Algorithm
1. Import the necessary libraries: numpy and pandas
2. Read the 'links.csv', 'movies.csv', 'ratings.csv', and 'tags.csv' files into separate dataframes: links_df, movies_df, ratings_df, and tags_df
3. Merge the movies_df and ratings_df dataframes on 'movieId' to create a new dataframe called df
4. Set the movie title M_a to the movie you want to recommend similar movies for
5. Find the top 5 users who rated M_a the highest by filtering the df dataframe for rows where the title is equal to M_a, sorting by rating in descending order, and selecting the top 5 userId values
6. For each user, find their top 5 rated movies (excluding M_a) by filtering the df dataframe for rows where the userId is equal to the user and the title is not equal to M_a, sorting by rating in descending order, and selecting the top 5 title values
7. Combine all recommended movies into a single list and remove duplicates using numpy's unique function
8. For each recommended movie, calculate a similarity score based on the overlap between its genres and M_a's genres by splitting the genre strings and comparing the resulting lists
9. Sort the recommended movies by similarity score in descending order using the sorted function with a lambda function as the key argument
10. Print the recommended movies in order of similarity score using a for loop
