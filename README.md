# Vaccinitaly Topic Analysis
The code in the repository performs data collection, data filtering, data cleaning, and topic analysis on the tweets shared by users pre-classified as no-vax.
To run the code, the following collections are required:
- a collection of all the tweets about the vaccines collected through the "Golden Hashtags" method (i.e., a complete collection),
- a collection of the tweets classified by the no-vax classifier built within the Vaccinitaly project (i.e., a labeled collection).

The code is organized in modules that are all included within the "Topic Analysis Pipeline.ipynb".
The task achieved by each of the modules is explained below.

## Module 1
The first module has three different sub-modules.

### Sub-module 1.1
The first submodule associates the correct user to all the labeled tweets by looking at the tweets within the complete collection.

### Sub-module 1.2
The second submodule collects the users for each labeled tweet whose user wasn't found in the complete collection using the tweepy library to query the Twitter APIs.

### Sub-module 1.3
The third submodule creates a collection of the users whose tweets contains at least one hashtag among the ones we identified as "no-vax-related hashtags". Those users will be the subjects of the following analyses.
