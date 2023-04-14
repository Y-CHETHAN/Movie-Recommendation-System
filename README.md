# Movie Recommendation System Data Warehouse Project
## About Dataset
This dataset describes 5-star rating and free-text tagging activity from MovieLens, a movie recommendation service. It contains 100836 ratings and 3683 tag applications across 9742 movies. These data were created by 610 users between March 29, 1996 and September 24, 2018. This dataset was generated on September 26, 2018.

Users were selected at random for inclusion. All selected users had rated at least 20 movies. No demographic information is included. Each user is represented by an id, and no other information is provided.

The data are contained in the files links.csv, movies.csv, ratings.csv and tags.csv.

## Flowchart
![image](https://user-images.githubusercontent.com/75234991/232089335-4d32ff79-0f31-4560-b311-04933626e9fd.png)

## Source Code
```python3
import numpy as np
import pandas as pd

links_df=pd.read_csv("links.csv")
links_df.head()

movies_df=pd.read_csv("movies.csv")
movies_df.head()

ratings_df=pd.read_csv("ratings.csv")
ratings_df.head()

tags_df=pd.read_csv("tags.csv")
tags_df.head()

df=movies_df.merge(ratings_df,on='movieId')

df.head()

M_a='Assassins (1995)'
recommended_movies=[]
movie_db=df[df['title']==M_a]\
  .sort_values(by='rating',ascending=False)
for user in movie_db.iloc[:5]['userId'].values:
  rated_movies=df[df['userId']==user]
  rated_movies=rated_movies[rated_movies['title']!=M_a]\
    .sort_values(by='rating',ascending=False)\
    .iloc[:5]
  recommended_movies.extend(list(rated_movies['title'].values))
recommended_movies=np.unique(recommended_movies)
for movie in recommended_movies:
  print(movie)

gmovie_genres=df[df['title']==M_a].iloc[0]['genres'].split('|')
scores={}
for movie in recommended_movies:
  movied=df[df['title']==movie].iloc[0]
  movie_genres=movied['genres'].split('|')
  score=0

  for gmovie_genre in gmovie_genres:
    if gmovie_genre in movie_genres:
      score=score+1

  scores[movie]=score

recommended_movies=sorted(scores,key=lambda x:scores[x])[::-1]

for movie in recommended_movies:
  print(movie)
```

