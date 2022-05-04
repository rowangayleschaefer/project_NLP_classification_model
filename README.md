<div id="top"></div>

<h1 align="center"> Reddit NLP Classification Project </h3>
  <img src="./images/houses9.png"> 

  <p align="center">
    Completed for General Assembly DSI Immersive
    <br />
  </p>
</div>



<!-- ABOUT THE PROJECT -->
# About The Project

Executive Summary
The goal of this analysis is to classify text posts as either belonging to one subreddit or another, using NLP.

Success will be evaluated using the model's accuracy score in correctly classifying the posts, with a second goal of trying many models to obtain the highest accuracy score possible.


### Data
Data was scraped from two subreddits, rlearnpython and r/learnsql, using Reddit's PushShift API.
r/learnpython is a subreddit for people who are learning python, mostly filled with resources and questions. r/learnsql is similar, except for people who are learning sql. Both subreddits are fairly active, but r/learnpython is much more popular; it has 613k subscribers, compared to 17.7k subscribers for r/learnsql.


### Research Questions
* What preprocessing steps are best for creating a classification model with high accuracy?
* Which classification models and hyperparameters lead to the highest accuracy score?
* After remov ing stopwords, which posts are most frequently misclassified?



### Data Acquisition/Cleaning
Reddit's API limits to 60 requests per minute and 100 rows of data per request. In order to pull data effectively and avoid duplicate rows, I wrote generated UTC timestamp ranges for the before:after filters on the date field, and then passed those ranges into my API function.  
During data cleaning nulls were handled appropriately for each column, repetetive posts were limited, and the title and selftext (body) of the post were concatenated. Later in preprocessing, text was converted to all lowercase, special characters were filtered, and the text was vectorized using both CountVectorizer and TfidfVectorizer. I also removed instances of "giveaway" words that I thought would make things too easy on my model.


### Exploratory Analysis
During exploratory analysis I briefly looked into additional columns I had pulled along with post text and body text, including number of commenters and top commenters per subreddit. I also did an analysis of post length and word count to see if these would be meaningful features in determining class membership.


### Modeling
For this project I focused on the metrics of accuracy precision, since I didn't care about the minimization of either false negatives or false posistives in particular. 
My baseline model had an accuracy score of 50.1 (seeing as the classes was ajust slightly off balance.)
I tried multiple different models with multiple different preprocessing steps; early on I learned that my countvectorizer worked better than tfidfvectorizer regardless of how I changed the hyperparams on both. My top performing models were a multinomial bayes, a random forest, and a logistic regression, I made a grid search for each and then passed the best performing version into VotingClassifier. 
My final model had an accuracy score of 99.2% on the training set, and 92.4% on the test set. The precision was 93%.



### Conclusions:
Overall, the votingclassifier returned my best model, essentially pulling in the positives of each model it was comprised of. However it made the results and feature importances uch more difficult to interpret. 
VotingClassifier actually performed similarly to my original model (without "giveaway" words removed) so I did actually reach my goal of improving my score back to this standard, without inclusion of common stopwords. 

I looked through posts that the model misclassified and found that many of them dealt with technologies or concepts that are shared by both python and SQL, a noteable mention being regex. Other common misclassifications were posts about learning resources/free classes, and general database questions. 

For someone else performing a similar anlysis, differences could be looked into between "flavors" of sql (by filtering names of flavors from title/body text, dropping rows with multiple flavors listed,  and using the newly engineered column as the independent variable.)

Note that for this notebook, charts generated with plotly are displayed as images, and code is included in the appendix of the notebook.


<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/github_username/repo_name.svg?style=for-the-badge
[contributors-url]: https://github.com/github_username/repo_name/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/github_username/repo_name.svg?style=for-the-badge
[forks-url]: https://github.com/github_username/repo_name/network/members
[stars-shield]: https://img.shields.io/github/stars/github_username/repo_name.svg?style=for-the-badge
[stars-url]: https://github.com/github_username/repo_name/stargazers
[issues-shield]: https://img.shields.io/github/issues/github_username/repo_name.svg?style=for-the-badge
[issues-url]: https://github.com/github_username/repo_name/issues
[license-shield]: https://img.shields.io/github/license/github_username/repo_name.svg?style=for-the-badge
[license-url]: https://github.com/github_username/repo_name/blob/master/LICENSE.txt
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://linkedin.com/in/linkedin_username
[product-screenshot]: images/screenshot.png

