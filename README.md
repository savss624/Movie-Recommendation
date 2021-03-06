# Movie Recommendation System using KNN Item-Based Collaborative Filtering
![intro image](https://www.vshsolutions.com/wp-content/uploads/2020/02/recommender-system-for-movie-recommendation.jpg)

## Recommender Systems
Most internet products we use today are powered by recommender systems. Youtube, Netflix, Amazon, Pinterest, and long list of other internet products all rely on recommender systems to filter millions of contents and make personalized recommendations to their users. Recommender systems are well-studied and proven to provide tremendous values to internet businesses and their consumers. In fact, I was shock at the news that Netflix awarded a $1 million prize to a developer team in 2009, for an algorithm that increased the accuracy of the company’s recommendation system by 10%.

Although recommender systems are the secret source for those multi-billion businesses, prototyping a recommender system can be very low cost and doesn’t require a team of scientists. You can actually develop your own personalized recommender for yourself. It only takes some basic machine learning techniques and implementations in Python. Here, we will start from scratch and walk through the process of how to prototype a minimum viable movie recommender.

## Approaches
Recommender systems can be loosely broken down into three categories: content based systems, collaborative filtering systems, and hybrid systems (which use a combination of the other two).
Here, I'm gonna use the collaborative filtering approach which builds a model from a user’s past behaviors (items previously purchased or selected and/or numerical ratings given to those items) as well as similar decisions made by other users. This model is then used to predict items (or ratings for items) that the user may have an interest in.

Collaborative filtering systems use the actions of users to recommend other movies. In general, they can either be user-based or item-based. Item based approach is usually preferred over user-based approach. User-based approach is often harder to scale because of the dynamic nature of users, whereas items usually don’t change much, and item based approach often can be computed offline and served without constantly re-training.
To implement an item based collaborative filtering, KNN is a perfect go-to model and also a very good baseline for recommender system development.

## But what is the KNN? 
KNN is a non-parametric, lazy learning method. It uses a database in which the data points are separated into several clusters to make inference for new samples.
KNN does not make any assumptions on the underlying data distribution but it relies on item feature similarity.

![KNN Diagram](https://miro.medium.com/max/813/1*OyYyr9qY-w8RkaRh2TKo0w.png)

## Let’s Build A Movie Recommender
## Data
To build a movie recommender, I choose [MovieLens Datasets](https://grouplens.org/datasets/movielens/latest/). It contains 27,753,444 ratings and 1,108,997 tag applications across 58,098 movies. These data were created by 283,228 users between January 09, 1995 and September 26, 2018. The ratings are on a scale from 1 to 5.

First, we need to transform the dataframe of ratings into a proper format that can be consumed by a KNN model. We want the data to be in an m x n array, where m is the number of movies and n is the number of users. To reshape dataframe of ratings, we’ll pivot the dataframe to the wide format with movies as rows and users as columns. Then we’ll fill the missing observations with 0s since we’re going to be performing linear algebra operations (calculating distances between vectors).

![Transformed csv](https://github.com/savss624/Readme-Images/blob/main/Movie%20Recommendation/dataset.png)

Now our training data has a very high dimensionality. KNN’s performance will suffer from curse of dimensionality if it uses “euclidean distance” in its objective function. Euclidean distance is unhelpful in high dimensions because all vectors are almost equidistant to the search query vector (target movie’s features). Instead, we will use cosine similarity for nearest neighbor search.

After we preprocessed the data and transformed the dataframe of ratings into a movie features matrix, we need to configure our KNN model with proper hyper-params:

![model code](https://github.com/savss624/Readme-Images/blob/main/Movie%20Recommendation/model.png)

## Let’s Make Some Movie Recommendations
![testing](https://github.com/savss624/Readme-Images/blob/main/Movie%20Recommendation/testing.png)

Our recommender system actually works!! Now we have our own movie recommender.

## Summary
We learned about how to prototype an item based collaborative filtering in KNN with only a few steps!
