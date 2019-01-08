# Project 3: Reddit API
# Binary Classification of Reddit Posts - Lord of the Rings and Game of Thrones
### Edith Iyer-Hernandez

# Executive Summary

## Introduction
Reddit.com is a website that serves a variety of purposes ranging from close knit communities, fandom specific groups, news content to heated political discussions and advice forums. These niche, online communities are called subreddits and each has a specific focus, set of guidelines, and moderators. Some subreddits are private, and some are public. Users can submit posts as well as upvote and comment on other posts. Due to the content specificty of each subreddit, it is possible that we can utilize natural language processing to build a classification model.  
<br>
In this notebook we seek to answer the question: Can we build a classification model to distinguish between two subreddits using natural language processing?

__________

Throughout this notebook, we explore the creating a model to distinguinsh between the __[Game of Thrones subreddit](http://reddit.com/r/asoiaf/)__ subreddit and the  __[Lord of the Rings subreddit](http://reddit.com/r/lotr/)__. Both are fantasy series with a large cult following and boast large online communities. While they share many similar motifs, eg. a quest for the true king, and dragons, they are distinct and are in fact at vastly different stages in fandom. A Song of Ice and Fire is awaiting its final installment whereas Lord of the Rings had all three books in its trilogy released by October 1955.

____________

**Data Description**
<br>
<br>
Data was collected via Reddit's API. A loop was created to pull 25 .json posts every two seconds using the requests library and an independent user agent designated as 'headers'. The .json files are automatically converted to a dictionary from which we can pull columns and rows for a dataframe containing an observation for each post, including, but not limited to, downvotes, number of comments, the text post, the text title, and the subreddit. We were mainly interested in the title, posts text, number of comments, and subreddit, our target variable. All the models to date have been created solely utilizing the post titles as features.
<br>

|Variable   |Description   |
|---        |---           |
|headers    |user agent created to ensure connection to API|
|lotr   |Dictionary from .json data from the LOTR API   |
|asoiaf   |Dictionary from .json data from the ASOIAF API   |
|asoiaf_df|DataFrame created from asoiaf|
|lotr_df|DataFrame created from lotr|
|df|DataFrame from combined asoiaf_df and lotr_df|

____________________
***Natural Language Preprocessing***
<br>
<br>
We proceeded with natural language processing 3 different ways.
1. CountVectorization, removing english stop words
> We utilized this method initially to see how a model would behave with very little adjustment to the title text except removing stop words.
2. Lemmatization, removing non letter characters, the subreddit names, series title words, and english stop words
> This method allowed us to look at all words except 'lotr', 'lord', 'rings', 'asoiaf', 'game', 'thrones' and english stop words.
3. Lemmatization, removing non letter characters, the subreddit names, series title words, top ranking words, and english stop words.
>Upon inspection, we found that two additional words, 'spoilers' and 'extended' were extremely high indicators of classifiying a subreddit as asoiaf. Removing these two words, allowed for a more nuanced tuning of the models.

________________

***Model Selection***
<br>
<br>
Five models were tested on the text features:
1. Logistic Regression
2. Bagging Classifier
3. Decision Tree Classifier
4. Random Forest Classifier
5. AdaBoost Classifier
<br>
___________________

***Model Evaluation***
<br>
<br>
This classification problem is one that does not value one outcome over the other, it is merely one that should have the highest possible accuracy score or a low misclassification rate.
<br>
The models all performed exceedingly well on the first two NLP methods, all with accuracy scores of over .99 on the testing data.
<br>
On the third preprocessed dataframe, the models saw lower training and testing accuracy scores.
<br>
While Logistic Regression had the highest accuracy score, we decided to use GridSearchCV to utilize optimization of hyper parameters on the RandomForest Classifier, the Bagging Classifier, and the AdaBoost Classifier.
__________________
***Findings and Recommendations***
<br>
The final model recommendation is Logistic Regression. This is not only interpretable, but also has consistently higher accuracy scores.
<br>
Further investigation into features selection might change the recommended model; incorporation of numeric featuers such as title length, number of comments and score may change accuracy of each model.
