# book-reviews-recommender-system

Recommender system to make book preferences and category prediction based on text-based Goodreads book reviews.

## Dataset descriptions 

- train_Interactions.csv.gz: 200,000 ratings to be used for training
  - userID:  The ID of the user. This is a hashed user identifier from Goodreads
  - bookID: The ID of the book. This is a hashed book identifier from Goodreads
  - rating: The star rating of the user’s review
- train Category.json.gzL Training data for the category prediction task
  - n_votes: The number of ‘likes’ this review has received
  - review_id: A hashed identifier for this review
  - user_id: A hashed identifier for the user
  - review_text:  Text of the review
  - rating_Rating: of the book
  - genreID: A numeric label associated with the genre
  - genre: A string version of the genre
- test_Category.json.gz: Test data associated with the category prediction task.
- pairs_Category.csv: Pairs (userID and reviewID) on which you are to predict the category of a book
- pairs_Read.csv: Pairs on which you are to predict whether a book was read

## Output files descriptions 

- predictions_Read.csv: Given a (user,book) pair from ‘pairs Read.csv’, this file contains predictions of whether the user
would read the book (0 or 1)
- predictions_Category.csv: Predictions of the category of a book from a review. Five categories are used for these predictions: Children’s, Comics/Graphic Novels, Fantasy, Mystery/Thriller, and Romance

## Methodologies 

Part 1: 
- looped over potential thresholds to find the best one
- created a list of the most popular books using that threshold
- looped over all the data in the test set, and if the given book was in the list of the most popular books, classified it as popular or not in a temporary data frame
- using that temporary data frame, I created an sklearn preprocessor and pipeline
- used that pipeline to predict the popularity of the books in pairs_Read.csv

Part 2:
- collected all of the data from the training dataset
- inputted data in a TfidfVectorizer and fit it and transformed it using TfidfVectorizer's methods
- created a pipeline model that transforms the data using TfidfVectorizer and LinearSVC transformers
- fit the x training data through that pipeline model
- looped through the testing data and extracted all of the reviews
- predicted y valid values using the pipeline model
- matched all of the predicted y valid values with the user IDs and review IDs in the test_Category file
  
