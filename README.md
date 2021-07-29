# Vaccinitaly - Topic Analysis
The code in the repository performs data collection, data filtering, data cleaning, and topic analysis on the last 100 tweets shared by users pre-classified as no-vax with the objective of detecting the most discussed topics within the no-vax community.
The code is organized in modules that are all included in "Topic Analysis Pipeline.ipynb".
The task performed by each of the modules is explained below.

# Setup
To run the code it is necessary to
- own a Twitter Developer Account able to access Twitter API v2 (e.g., an Academic account),
- own a subscription to Botometer (available at https://botometer.osome.iu.edu/),
- setup an environment with all the required libraries (in this project Anaconda has been used to manage the environment and run the Jupyterlab code),
- setup a MongoDB installation with the following collections
  - a collection of all the tweets about the vaccines collected through the "Golden Hashtags" method (i.e., a complete collection),
  - a collection of the tweets classified by the no-vax classifier built within the Vaccinitaly project (i.e., a labeled collection).

See References at the bottom to better understand more about the project and the data collection phase.

## Module 1 - Data Organization
The first module has three different sub-modules.

### Sub-module 1.1
The first submodule associates the correct user to all the labeled tweets by looking at the tweets within the complete collection.

### Sub-module 1.2
The second submodule collects the users for each labeled tweet whose user wasn't found in the complete collection using the tweepy library to query the Twitter API.

### Sub-module 1.3
The third submodule creates a collection of the users whose labeled tweets contains at least one hashtag among the ones we identified as "no-vax-related hashtags".
From this point on, whenever users will be mentioned, we will only refer the ones extracted at this step.

## Module 2 - Data Collection
The second module uses the request library to query the Twitter API and collect the last 100 tweets shared by the users.
The amount of tweets collected is configurable. We advice to keep at least 100 to ensure a rich data collection step.

### Submodule 2.1
This submodule collects the original tweets associated with the retweets collected by the second module.
When collecting the data from Twitter, most of the times a retweet is collected. Twitter APIs do not return the whole text of a tweet when a retweet is collected, therefore to access the full text we need to downlad the original tweet.

## Module 3 - Botometer Integration
The third module integrates the bot scores returned by Botometer.
Botometer APIs are queried to collect the bot scores associated with each user.

## Module 4 - Data Filtering
The fourth module derives some metrics that will be used to filter the considered users.
In the process, we ignored the users (and their tweets) with the following features
- users with no shared tweets
- verified users
- users with a bot score > 0.5
- users with a tweet frequency per minute greater than 2
- users with a percentage of no-vax tweets shared less than 0.6

## Module 5 - Data Cleaning
The fifth module cleans the data and generates the data useful in the topic analysis task.
In particular, we derived different tokenized versions of the text of the tweet to be (eventually) used in the following analysis.

## Module 6 - Topic Analysis
The last module performs the topic analysis.
In particular, we considered only the Italian tweets which contained at least two tokens.
The topic analysis is performed many times to identify the model with the highest coherence value.

## Submodule 6.1
The final submodule must be configured by the user to identify the model with the best coherence value.
It associate a topic to each tweet and help the user in defining the name for each one of the topics.
The submodule displays the results of the topic analysis through three representation
- graphical, positioning the topics within a graph
- textual, displaying the top N words associated with each topic
- exemplify, extracting the top T tweets that best represent a topic

# References
## About the Labeling
M. Di Giovanni, L. Corti, S. Pavanetto, F. Pierri, A. Tocchetti, and M. Brambilla. “A Content-based Approach for the Analysis and Classification of Vaccine-related Stances on Twitter: the Italian Scenario”. doi:10.36190/2021.52. url: http://workshop-proceedings.icwsm.org/pdf/2021_52.pdf.

## About the Project
F. Pierri, A. Tocchetti, L. Corti, M. Di Giovanni, S. Pavanetto, M. Brambilla, and S. Ceri. “VaccinItaly: monitoring Italian conversations around vaccines on Twitter”. doi:10.36190/2021.11. arXiv:2101.03757. url: https://arxiv.org/pdf/2101.03757.pdf.
