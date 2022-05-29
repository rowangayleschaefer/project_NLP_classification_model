<div id="top"></div>

<div align="center">
<!-- PROJECT SHIELDS -->

[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![MIT License][license-shield]][license-url]
[![LinkedIn2][linkedin-shield]][linkedin-url]</div>
<br />
<br />

<h1 align="center"> Reddit NLP Classification Project </h1>
<div align="center"><img src="https://www.kindpng.com/picc/m/3-32823_house-drawing-png-transparent-png.png" height=100 width=180> </div>

  <p align="center">
    Completed for General Assembly DSI Immersive
    <br />
  </p>
</div>



<!-- ABOUT THE PROJECT -->
# About The Project

### Executive Summary

The goal of this project was to correctly classify posts as either belonging to subreddit 1 or subreddit 2, using machine learning classification models and NLP libraries in Python.
<br /><p>
<br />
  
  
### Research Questions
* Which classification models and hyperparameters lead to the highest accuracy score in classifying text posts?
* Which posts are most frequently misclassified?

<br /><p>
  
  
### Software Requirements

Note that some formatting for tables and vizualizations will not render unless you run this on your local machine, rather than viewing project via github.

To run this code, you will need python installed (3.8.0 or higher recommended). <br />

Libraries used include:
* Pandas
* NumPy
* MatPlotLib
* Seaborn
* SciKitLearn

<p></p>
<br />

### Data
Data was scraped from two subreddits, <code>r/learnpython</code> and <code>r/learnsql</code>, using Reddit's PushShift API.

<code>r/learnpython</code> is a subreddit for people who are learning python, mostly filled with resources and questions. <code>r/learnsql</code> is similar, except for people who are learning sql. Both subreddits are fairly active, but r/learnpython is much more popular; it has 613k subscribers, compared to 17.7k subscribers for r/learnsql.




<p align="right">(<a href="#top">back to top</a>)</p>
<br /><p>


### Data Acquisition/Cleaning
Reddit's API is pretty easy to use, but it does limit 60 requests per minute and 100 rows of data per request. 
  
In order to avoid pulling duplicate rows of data, I wrote a function to make requests using unique UTC timestamp ranges. 
I found that I had to pull additional data for r/sql in order to avoid unbalanced data, due to differences in activity levels between the two subreddits.

During data cleaning nulls were handled appropriately for each column, repetetive posts were limited, and the title and selftext (body) of the post were concatenated. Later in preprocessing, text was converted to all lowercase, special characters were filtered, and I tested multiple methods of vectorizing text. 
  
I also removed instances of "giveaway" words that I thought would make class prediction too straightforward.


### Exploratory Analysis
The exploratory analysis notebook contains some initial EDA on post text, body text, and additional columns, including number of commenters and top commenters per subreddit. 
  
I also did an analysis of post length and word count to see if these would be meaningful features in determining class membership.


### Modeling
* For this particular problem, it wasn't necessary to minimize false negatives or false posistives, so I used accuracy, precision, and f1_score as metrics.
  
* My baseline model had an accuracy score of 50.1 (seeing as the classes in my dataset had a slight imbalance.)

* I tried using both countvectorizer and TfidfVectorizer to vectorize text; models using countvectorizer consistently performed better than TfidfVectorizer. 

* My top performing models were a multinomial bayes, a random forest, and a logistic regression. I made a grid search for each of these models, and used VotingClassifier to make an ensemble model.

* My final model had an accuracy score of 99.2% on the training set, and 92.4% on the test set. 



### Conclusions:
Overall, the votingclassifier returned my best model, essentially pulling in the positives of each model it was comprised of. However, it made the results and feature importances uch more difficult to interpret. 

VotingClassifier actually performed similarly to my original model (without "giveaway" words removed) so I did actually reach my goal of improving my score back to this standard, without inclusion of common stopwords. 

I looked through posts that the model misclassified and found that many of them dealt with technologies or concepts that are shared by both python and SQL, a noteable mention being regex. Other common misclassifications were posts about learning resources/free classes, and general database questions. 
  
Overall, my model did

### Next Steps
  
**Taking a look at preliminary models, there are a couple steps I could take next, given more time to complete the project:**
* Take a deeper look into settings for TfidfVectorizer to improve performance: although I did spend some time on this, I had limited knowledge of NLP at the time I completed this project.
* Limiting features/words used to classify posts - for code-heavy posts, it should theoretically be possible to build a model that uses a negligable number of  features, but still classifies with high accuracy (with the exception of Regex questions.)
* Taking a deeper look at misclassifications, and attempting to prevent common misclassifications by adjusting preprocessing steps.
* Seeing if model performance improves when using SpaCy or alternative Natural Language Processing libraries
* Trying a neural net model for classification.
  
**Additionally, here some other ideas that I could explore for this dataset:**
* Classifying "flavors" of SQL within the r/sql subreddit (this could potentially be done using only special characters and a few keywords.)
* Analysis of most common issues that users ask for help with in each subreddit 
* Sentiment analysis could be tough for this data, since a large amount of it is code blocks, but it would still be interesting to look into.


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

