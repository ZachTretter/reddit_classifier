## Reddit Natural Language Processing Reddit (Project 3)
### Zach Tretter, April 2020
General Assembly, Data Science Immersion Cohort 11, Boston

-----

### Project Folder Structure
* CODE Folder
  * 'Reddit_Data_Extraction.ipynb' (Pulls data from reddit and creates csv)
  * 'Reddit_NLP_Model.ipynb' (Imports CSV, processes and models data)
* DATA Folder
  * 'subreddit_data.csv' (CSV of data used in final model)
* Instructions Folder
  * 'README.md' (Instructions for Project)
  * 'Requirements.txt' (Requirements for Project)
* 'README_RedditNLP_Submission.md' (This readme file)
* 'Tretter  Project 3 - 24 Apr 2020' (Presentation)

--------

# Executive Summary

### Problem Statement
Explore the power of binary classification models to differentiate between two subreddits.

### Project Methodology
Two subreddits were considered : r/conservative and r/libertarian.  These subreddits were chosen because there is enough overlap between them to be interesting but still enough to distinguishable.  They are of comparable size (~350K users) and both advertise themselves as the "the place for __ on reddit". Additionally, other political subreddits have insane post volume that would have limited analysis to the past couple weeks.

Data Extraction consisted of pulling 100K posts from each subreddit and then filtering for only those with more than 10 upvotes (i.e. score).  Upvoted content reflects that which is "representative" of a subreddit.  Over 2/3 of all posts on these subreddits received no upvotes.  A random sample of 5K was taken from each subreddit to maintain balanced classes.  The independent variable is submission title due to the prevalence of image and meme posts that are not yet interpretable for this analyst's machine learning abilities.

Text Preprocessing consisted principaly of lemmatizing.  Numbers were kept in as "2020" and "16" have strong political meaning.  The subreddit names were removed as filtering based on these would not be interesting

### Model Performance

Baseline : 50%

| Model                   | Train Score | Test Score | Test F1 Score |
|-------------------------|-------------|------------|---------------|
| Logistic CVEC           | 0.809733    | 0.7240     | 0.739623      |
| Logistic TFIDF          | 0.832800    | 0.7292     | 0.735856      |
| Multinomial Bayes CVEC  | 0.793200    | 0.7160     | 0.719589      |
| Multinomial Bayes TFIDF | 0.797333    | 0.7164     | 0.719874      |
| Support Vector CVEC     | 0.928400    | 0.7112     | 0.713264      |
| Support Vector TFIDF    | 0.910000    | 0.6924     | 0.702284      |
| Random Forest CVEC      | 0.858000    | 0.6744     | 0.709907      |
| Random Forest TFIDF     | 0.858000    | 0.6744     | 0.709907      |

### Principal Findings

* All Models performed similarly on test data (~70%)
    * SVCs and Random Forests particularly suffered from overfit
    * TFIDF performed marginally better than Count Vectorizer for Logistic/Bayes/SVC
        * Reverse performance with Random Forest
    * Consistently more inaccurate predictions of conservative than of libertarian


* Findings from Grid Searches (Text Vectorizer Parmaters)
    * Max Features : Models almost always select for more features
    * Max_df : Consistently selected to be between 0.2 and 0.4
    * Min_df : Not impactful, default chosen
    * StopWords: Logistic selected for English, other classifiers selected none
    * n-grams: Length 1,1 almost always selected


#### These models show we can be ~40% more accurate than a random guess!
