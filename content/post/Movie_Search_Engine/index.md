+++
title = "Movie Search Engine"
subtitle = ""

# Add a summary to display on homepage (optional).
summary = "A TF-IDF Ranking Search Engine"

date = 2019-05-01T18:11:30-05:00
draft = false

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = ["Chaowei Wang"]

# Is this a featured post? (true/false)
featured = false

# Tags and categories
# For example, use `tags = []` for no tags, or the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
tags = ["NLP", "TF-IDF", "Search Engine", "Data Mining"]
categories = []

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["deep-learning"]` references 
#   `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
# projects = ["internal-project"]

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
[image]
  # Caption (optional)
  caption = ""

  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = ""
+++

## Procedure
1. Find the movie dataset
2. Configure a EC-2 web server provided by AWS, this includes install apache, MySQL, phpmyadmin and python interpreter (for latter development). 
3. Deploy the movie dataset into MySQL DBMS.
4. Develop the front end page by html and css.
5. Develop the back end by php. Php access the data stored in MySQL. Php calculates the tf-idf value for the overview of each movie’s. Each movie assigns a n dimensional vector after that. When an user type in keywords, Php calculates the user query as a new tf-idf vector. Finally we calculate the similarities between the user query and each of the movies by tf-idf values. Returning all the results ordered by similarity value decreasingly.

*Scripts on Github: [GitHub Pages](https://github.com/mangfu1231/search-engine.git)*

## TF-IDF Algorithm
TF-IDF is short for Term Frequency and Inverse Document Frequency. It is a ranking mechanism applied to search engine mostly. It takes each unique words as terms in the document. In our project, we produce a TF-IDF vector for each description of movies. Each TF-IDF vector contains data on how important a given word is to that document. As the name indicates, it consists of two components, TF and IDF.

1. Compute TF: Term Frequency
The term frequency (TF) is a measure of how frequently a term appears in a document. We compute it using this formula:
![tf](/img/tf.png)
Notice the more the term appears in the document, the higher the TF score.

2. Compute IDF: Inverse Document Frequency
The inverse document frequency (IDF) measures how frequently a term appears in all documents using this formula:
![idf](/img/idf.png)
Through IDF, we punish common words to minimize the importance of the term for the documents. For example, common words like "the", "is", or "a" may appear in all of documents, it apparently not important at all, which means these words are not relevant to a user query.

3. Combined TF-IDF score
Finally, we compute the final TF-IDF relevance score for the term by multiplying the two above numbers together:
![tfidf](/img/tfidf.png)

4. Implement cosine similarity
After this we get a sparse matrix including all the terms and documents in terms of description. When users give a query, we treat it as a new vector, the cosine similarity between the query vector and all document vectors take the search job completed.
![tfidf](/img/cos.png)
We return all the movie title which has similarity value larger than one ordered decreasingly.

## Features
![main](/img/main.png)
This is the main page movie searching.
![top](/img/top.png)
Take keywords “beautiful day” as an example, the page returns a bunch of results consisting by movie title and overview in an ranked manner. It clearly indicates the top ranked results contain all or part of the keywords, “beautiful” and “day”, in this example. 
![bottom](/img/bottom.png)
The bottom ranked results although contain all or partial keywords (in most cases partial), the overview apparently consist of more words/terms than the top ones. This indicates out term frequency mechanism works.

##### Reference
[1] https://vijayasankarn.wordpress.com/2017/01/17/setting-lamp-stack-in-ubuntu-16-04-using-aws-ec2/  
[2] https://courses.cs.washington.edu/courses/cse373/17au/project3/project3-2.html  
[3] http://phpir.com/simple-search-the-vector-space-model  
[4] http://www.chuggnutt.com/stemmer-source

##### Site Access
http://18.191.69.72/search.html