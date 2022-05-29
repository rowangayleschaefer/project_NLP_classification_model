<div id="top"></div>

<div align="center">
<!-- PROJECT SHIELDS -->

[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![MIT License][license-shield]][license-url]
[![LinkedIn2][linkedin-shield]][linkedin-url]</div>

<!-- PROJECT LOGO -->
<br />
<div align="center">
  </a>

<h1 align="center"> Reddit NLP Classification Project </h1>


  <p align="center">
    Completed for General Assembly DSI Immersive
    <br />
  </p>
</div>
<br /></p>


<!-- ABOUT THE PROJECT -->
# About The Project
<div aligh="center"><a href=https://www.icloud.com/keynote/075rfgAkDG4ixyrlDc87q_9Sg#project3%5Fpres%5F><img src="./images/reddit.png"></a></div>
<br /><p>

The goal of this project was to correctly classify posts as either belonging to subreddit 1 or subreddit 2, using machine learning classification models and Natural Language Processing.
<br /><p>
<br />
  
  
### Research Questions
* Which classification models and hyperparameters classify reddits posts with the highest accuracy/precision?
* What topics are most frequently misclassified? Which subreddits are most frequently misclassified?

<br /><p>
  
  
### Software Requirements

Note that some formatting for tables and vizualizations will not render unless you run this on your local machine, rather than viewing project via github. Charts generated with plotly are displayed as images, and code is included in the appendix of the notebook.

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

## Process
  
### Data Acquisition/Cleaning
Reddit's API is pretty easy to use, but it does limit 60 requests per minute and 100 rows of data per request. 
  
In order to avoid pulling duplicate rows of data, I wrote a function to make requests using unique UTC timestamp ranges. 
I found that I had to pull additional data for r/sql in order to avoid unbalanced data, due to differences in activity levels between the two subreddits.

During data cleaning nulls were handled appropriately for each column, repetetive posts were limited, and the title and selftext (body) of the post were concatenated. Later in preprocessing, text was converted to all lowercase, special characters were filtered, and I tested multiple methods of vectorizing text. 
  
I also removed instances of "giveaway" words that I thought would make class prediction too straightforward. The data acquisition process is located in [notebook 1](https://github.com/rowangayleschaefer/project_NLP_classification_model/blob/main/Rowan_Proj3_Part1.ipynb).

<br /><p>
  
### Exploratory Analysis
The [exploratory analysis notebook](https://github.com/rowangayleschaefer/project_NLP_classification_model/blob/main/Rowan_Proj3_Part2.ipynb) contains some initial EDA on post text, body text, and additional columns, including number of commenters and top commenters per subreddit. 
  
I also did an analysis of post length and word count to see if these would be meaningful features in determining class membership. 


 <br /><p>
### Modeling
Preprocessing steps and modeling for this project are located in [notebook 3](https://github.com/rowangayleschaefer/project_NLP_classification_model/blob/main/Rowan_Proj3_Part3.ipynb). 
   
* For this particular problem, it wasn't necessary to minimize false negatives or false posistives, so I used accuracy, precision, and f1_score as metrics.
  
* My baseline model had an accuracy score of 50.1 (seeing as the classes in my dataset had a slight imbalance.)

* I tried using both countvectorizer and TfidfVectorizer to vectorize text; models using countvectorizer consistently performed better than TfidfVectorizer. 

* My top performing models were a multinomial bayes, a random forest, and a logistic regression. I made a grid search for each of these models, and used VotingClassifier to make an ensemble model.

* My final model had an accuracy score of 99.2% on the training set, and 92.4% on the test set. 

<br /><p>

### Conclusions:
Overall, the ensemble of multinomial bayes, random forest, and logistic regression was my best model, essentially pulling in the positives of each model it was comprised of. However, it made the results and feature importances much more difficult to interpret.  

I looked through posts that the model misclassified and found that many of them dealt with technologies or concepts that are shared by both python and SQL, a noteable mention being regex. Other common misclassifications were posts about learning resources/free classes, and general database questions. 
  
<br /><p>
  
<p align="right">(<a href="#top">back to top</a>)</p>
<br /><p>

### Next Steps
  
**Taking a look at preliminary models, there are a couple steps I could take next, given more time to complete the project:**
* Take a deeper look into settings for TfidfVectorizer to improve performance: although I did spend some time on this, I had limited knowledge of NLP at the time I completed this project.
* Limiting features/words used to classify posts - for code-heavy posts, it should  be possible to build a model that uses a negligable number of  features, but still classifies with high accuracy.
* Taking a deeper look at misclassifications, and attempting to account for these by adjusting preprocessing steps.
* Testing model performance with SpaCy or alternative Natural Language Processing libraries
* Trying a neural net model for classification
<br /><br />
  
**Additionally, here some other ideas that I could explore using this dataset:**
* Classifying "flavors" of SQL within the r/sql subreddit (this could potentially be done using only special characters and a few keywords.)
* Analysis of most common issues that users ask for help with in each subreddit 

  
<p align="right">(<a href="#top">back to top</a>)</p>
<br /><p>


<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/rowangayleschaefer/project_NLP_classification_model.svg?style=for-the-badge
[contributors-url]: https://github.com/rowangayleschaefer/project_NLP_classification_model/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/rowangayleschaefer/project_NLP_classification_model.svg?style=for-the-badge
[forks-url]: https://github.com/rowangayleschaefer/project_NLP_classification_model/network/members
[stars-shield]: https://img.shields.io/github/stars/rowangayleschaefer/project_NLP_classification_model.svg?style=for-the-badge
[stars-url]: https://github.com/rowangayleschaefer/project_NLP_classification_model/stargazers
[issues-shield]: https://img.shields.io/github/issues/rowangayleschaefer/project_NLP_classification_model.svg?style=for-the-badge
[issues-url]: https://github.com/rowangayleschaefer/project_NLP_classification_model/issues
[license-shield]: https://img.shields.io/github/license/rowangayleschaefer/project_NLP_classification_model.svg?style=for-the-badge
[license-url]: https://github.com/rowangayleschaefer/project_NLP_classification_model/blob/master/LICENSE.txt
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://linkedin.com/in/rowanschaefer

