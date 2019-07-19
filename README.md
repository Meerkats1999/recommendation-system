# Movie Recommendation
A Python based movie recommendation system that uses Demographic and Content Based Filtering to recommend movies to users.

# Installation
1. Install Jupyter Notebooks through Anaconda from the link https://www.anaconda.com/distribution/ for Python 3.7
2. Install Pandas and Numpy if not installed by default.

# Demographic Filtering
It provides recommendations based on movie popularity and/or genre. The System recommends the same movies to users with similar demographic features. The basic idea behind this system is that movies that are more popular and critically acclaimed will have a higher probability of being liked by the average audience.

1. We need a metric to score or rate movie
2. Calculate the score for every movie
3. Sort the scores and recommend the best rated movie to the users

I have used the average ratings of the movie as the score but using this won't be fair enough since a movie with 8.9 average rating and only 3 votes cannot be considered better than the movie with 7.8 as as average rating but 40 votes. So, I'll be using IMDB's weighted rating (wr) which is given as :-

wr = ((v/(v+m)).R) + ((m/(v+m).C)

where,

v is the number of votes for the movie;
m is the minimum votes required to be listed in the chart;
R is the average rating of the movie; And
C is the mean vote across the whole report

# Content Based Filtering
It provides similar items based on a particular item. This system uses item metadata, such as genre, director, description, actors, etc. for movies, to make these recommendations. The general idea behind these recommender systems is that if a person liked a particular item, he or she will also like an item that is similar to it.

I have compute pairwise similarity scores for all movies based on their plot descriptions and recommend movies based on that similarity score. The plot description is given in the overview feature of our dataset.
Now we'll compute Term Frequency-Inverse Document Frequency (TF-IDF) vectors for each overview.
Term Frequency: Relative Frequency of a word in a document.
Inverse Document Frequency: The relative count of documents containing the term.

This will give us a matrix where each column represents a word in the overview vocabulary (all the words that appear in at least one document) and each column represents a movie, as before.This is done to reduce the importance of words that occur frequently in plot overviews and therefore, their significance in computing the final similarity score.

Fortunately, scikit-learn gives us a built-in TfIdfVectorizer class.

With this matrix in hand, we can now compute a similarity score. I have used the cosine similarity.

After this I have followed the following steps:
1. Get the index of the movie given its title.
2. Get the list of cosine similarity scores for that particular movie with all movies. Convert it into a list of tuples where the 3. first element is its position and the second is the similarity score.
4. Sort the aforementioned list of tuples based on the similarity scores; that is, the second element.
5. Get the top 10 elements of this list. Ignore the first element as it refers to self (the movie most similar to a particular
movie is the movie itself).
6. Return the titles corresponding to the indices of the top elements.
