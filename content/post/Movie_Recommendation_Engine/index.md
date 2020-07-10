+++
title = "Movie Recommendation Engine"
subtitle = ""

# Add a summary to display on homepage (optional).
summary = "A Content-based Movie Recommendation Engine Refined by Popularity"

date = 2019-05-23T23:14:44-05:00
draft = false

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = ["Chaowei Wang"]

# Is this a featured post? (true/false)
featured = false

# Tags and categories
# For example, use `tags = []` for no tags, or the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
tags = ["Machine Learning", "Recommender", "tf-idf"]
categories = []
+++

## Procedure
Please refer to previous blog for data acquisition and processing as well as sever and DBMS configuration.  
For the recommender developing, vector space model is initially applied to calculate similarity between any two movies based on movie overview. We also introduce movie popularity to refine the result ranking. Html/CSS, php and python are used for developing the recommender system. Procedure are listed as following,

1. Since this recommender is developed depended on LAMP, runing python directly on Apache is not a good choice. We use an intermediate php script to call the python script running which is similiar to run python through bash.

2. Since phase one have developed tf-idf algorithm by php, in this phase, we build the tf-idf algorithm by python and retrieve top 10 movies which are similar to the movie user input. We adjust the top 10 movie rank by introducing popularity, this is because we think a similar movie might not be the most of interested to the user, a popular and at the same time a similar movie may be a better choice compare to similar one solely.

*Scripts on Github: [GitHub](https://github.com/mangfu1231/recommender)*

## Content-Based Recommender
Content-based recommender suggest similar items based on a particular item. This system uses item features, such as genre, director, description, actors, etc. for movies, to make recommendations. The general idea behind these recommender systems is that if a person likes a particular item, he or she will also like an item that is similar to it.
In our dataset, we have overview to describe each of movies, we will compute TF-IDF vectors for each movie based on overview. This will give us a matrix where each column represents a word in the overview vocabulary and each row represents a movie. By the vectors we calculated, we can have pairwise similarity scores for all movies and recommend movies based on that similarity score. Mathematically, the similarity scores is defined as follows:
![img](/img/cos.png)
The tf-idf algorithm explanation in detail can be found in phase 1 blog.
We can further refined the recommender system by introducing more features to get a better ranking mechanism. Considering users may be not only interested in similar movies, but a popular movie along with similarity may be the movie they are most interested in. Take this into consideration, we refine the ranking mechanism by introducing popularity feature to re-rank the top ten movie which are retrieved by similarity scores of tf-idf. By observing distribution of popularity value, the popularity value take down as 1% of their original values. And contribution to 20% of the whole score, the similarity scores recalculate as 80% accordingly. The final ranking scores is defined as follows:
![img](/img/weight.png)
The movie display order is re-ranked by the final score.
For example, a user want to find recommendations by input "The Godfather", the original recommender will return the results by similarity solely,
![img](/img/score1.png)
However, by introducing popularity, the movie re-orders as,
![img](/img/score2.png)
![img](/img/movieRank.png)
We intuitively say the "The Godfather: Part 3" is more of interested to user who finds suggestion based on "The Godfather" than "Blood Ties". 

## Features
![img](/img/mainR.png)
This is the main page for user input.
![img](/img/resultR.png)
After user type in movie title, the ten most similar movies adjusted by popularity values will return.

##### Reference
[1] https://towardsdatascience.com/intro-to-recommender-system-collaborative-filtering-64a238194a26  
[2] https://docs.scipy.org/doc/numpy/user/index.html  
[3] https://www.datacamp.com/community/tutorials/recommender-systems-python?utm_source=adwords_ppc&utm_campaignid=1565261270&utm_adgroupid=67750485268&utm_device=c&utm_keyword=&utm_matchtype=b&utm_network=g&utm_adpostion=1t1&utm_creative=332661264374&utm_targetid=aud-392016246653:dsa-473406569915&utm_loc_interest_ms=&utm_loc_physical_ms=9026867&gclid=CjwKCAjwk7rmBRAaEiwAhDGhxI-2uAm_xMOQ9m8mGlKTAOcqqy6Y5To3oQwYI8SPl_bpyZvUE_aTGhoC9OgQAvD_BwE  
[4] https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html

##### Site Access
http://18.191.69.72/rec.html