# tag_prediction

In this project, we predict tags for the site Stack Overflow. As a part of our project for IBM x SmartInterz's HackChallenge


Dataset: https://www.kaggle.com/datasets/stackoverflow/stacksample

-----------------------------------


We have only used the questions and the tags to implement a tag suggestion system. 

First, we have cleaned the data and done EDA

Second, we have classical classifiers to determine the best model

## PART 1 

### Cleaning Data & EDA

Here we have, 
- Merged both dataframes on the id. 
- Dropped useless Columns such as OwnerUserID etc 
- To make the dataset smaller and of better quality, we have only used the questions with a score greater than 5. 
- For the tags column, we split the multiple tags, into 100 most common tags and then drop the columns with the null values. So that we only keep to the relevant and precise data to make our model work better. 
- For the Body and Title columns, we have used a lot of text processing. 
- Our text processing goals include: removing the html format from them, lowering all the text, transforming the abbreviations, removing punctuations (but keeping words like c#), lemmatizing the words, and removing the stop words. 
- Then for the EDA Part, we used LDA (Latent Dirichlet Allocation) to check if there any patterns in the words or topics.


## PART 2 

### Classical Classifiers

Here, 
- First we prep the data so that it can be put into a classifier. 
- There are only two things to be done here, first is to binarize the tags, and then use a TFIDF for body and title.
- By setting token_pattern=r"(?u)\S\S+" here, we're instructing the TF-IDF process to consider any sequence of two or more non-whitespace characters as a valid token, so that we are preserving terms like "c#" and ".net" without breaking them into smaller parts during the tokenization process. 
- After this we use one vs rest multiclass strategy. This strategy consists in fitting one classifier per class.
- To evaluate our models, we have used jacard score.
- We have used several classifiers, each of which represent a diff algo.
- Classifiers we have used include: DummyClassifier, SGDClassifier, LogisticRegression, MultinomialNB, LinearSVC, Perceptron, and PassiveAggressiveClassifier, MLPClassifier, and Random Forests.
- Here we have found LinearSVC to be the best performing according to the jacard score. 
- Then we used GridSearchCV to search through the best parameter values from the given set of grid of parameters.
- We then have the confusion matrix which helps in performance measurement of the classification.
- Finally we print the top 10 feature names for the tags. 


## CONCLUSION

Though the accuracy and performance is not at its best right now, it can be only be improved with implementation and more training. Using libraries such as Linguist Library which Github itself uses as a tagging system and using IBM Watson's NLP Features as suggested, will certainly help the model in learning and being more accurate. 
