+++
title = "Movie Genre Classifier"
subtitle = ""

# Add a summary to display on homepage (optional).
summary = "A Movie Genre Classifier by Budget and Revenue"

date = 2019-05-23T23:02:30-05:00
draft = false

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = ["Chaowei Wang"]

# Is this a featured post? (true/false)
featured = false

# Tags and categories
# For example, use `tags = []` for no tags, or the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
tags = ["NLP", "Artificial Intelligence", "Classifier", "Naive Bayes"]
categories = []
+++

## Procedure
Please refer to the previous blog for data acquisition and processing as well as sever and DBMS configuration.
For the classifier developing, SVM and Naive Bayes have been tested on the movie dataset. Due to the similar accuracy and better time complexity for Naive Bayes, we finally developed the classifier by Naive Bayes. Html/CSS, Php and Python are used for developing the classifier. Procedure are listed as following,

1. Since this classifier is developed depended on LAMP, runing python directly on Apache is not a good choice. We use an intermediate php script to call the python script running which is similiar to run python through bash.

2. The Naive Bayes Classifier was trained in python by movie dataset, and using 10% to test the accuracy of the classifier. The movie dataset include two numeric columns, budget and revenue, one character column, genre. We use the equation of Naive Bayes to calculate the probability of a movie with certain budget and revenue belonging to certain genres, and pick up the genre to be the movie genre which has the largest probability. For example, if we want to check if a movie is action with budget $15,000,000 and revenue $356,296,601, we can calculate the probability by the formula below. We also have to calculate other probabilities for other genres with the same budget and revenue. If probability of action is the highest, we conclude a movie with budget $15,000,000 and revenue $356,296,601 belong to genre action. 
![img](/img/formular1.gif)
3. We save the trained classifier as a file for future quick access.
4. A simple webpage is developed by html/css. A php script developed for handling user input and call another python script to run the classifier retrieving final genre.

*Scripts on Github: [GitHub](https://github.com/mangfu1231/classifier.git)*

## Naive Bayes Algorithm
Bayes theorem provides a way of calculating the posterior probability, P(c|x), from P(c), P(x), and P(x|c). Naive Bayes classifier assume that the effect of the value of a predictor (x) on a given class (c) is independent of the values of other predictors. This assumption is called class conditional independence.  
P(c|x)=(P(x|c)*P(c))/P(x)  
In our case, we want to calculate the probability for a given genre by providing budget and revenue. The equation can be written as:
![img](/img/formular1.gif)
The equation can be further rewrite as:
![img](/img/formular2.png)
Since our attribute is not a category, we need to use the distribution of the numerical variable to have a good guess of the frequency. We take the drama and action budget distribution as an example.
![img](/img/distributionDrama.png)
![img](/img/distributionAction.png)
From the two chart above, we can see action movie is prone to have a higher budget compare to drama.

## Features
![img](/img/mainClf.png)
This is the main page for user typing.
![img](/img/result.png)
After user type in budget and revenue, it will return the most likely genre by the giving two values along with the probability.

##### Reference
[1] https://stackabuse.com/implementing-svm-and-kernel-svm-with-pythons-scikit-learn/  
[2] https://www.datacamp.com/community/tutorials/naive-bayes-scikit-learn  
[3] https://stackabuse.com/scikit-learn-save-and-restore-models/  
[4] https://scikit-learn.org/stable/modules/multiclass.html  
[5] https://scikit-learn.org/stable/modules/generated/sklearn.naive_bayes.MultinomialNB.html  
[6] https://chrisalbon.com/machine_learning/naive_bayes/multinomial_naive_bayes_classifier/  
[7] https://www.analyticsvidhya.com/blog/2017/08/introduction-to-multi-label-classification/  
[8] https://www.saedsayad.com/naive_bayesian.htm

##### Site Access
http://18.191.69.72/classifier.html
