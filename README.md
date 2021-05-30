# Spotify Analysis

## Objective:
Spotify's Popularity index uses an algorithm to evaluate a song, largely based off of the number of plays a song gets. The better the evaluation, the more likely an artist and their music will be recommended to a larger number of viewers. Said simply, the greater a song's Popularity index, the greater its presence in the Spotify community.

The goal of this project will be to determine what features impact the Popularity index of any given song on Spotify. By analyzing various physical features of a song as well as some peripherary features, we look to identify a pattern within how a song garners a successful Popularity index. Using this knowledge, we hope to be able to create a model that can predict the popularity of a song based on on these features.

## Methodology:

### Data Sources

To begin this analysis, we decided to leverage an existing dataset consisting of ~600k tracks from 1922-2021 that was created from the Spotify Web API. The data is divided into various perspectives. For our purpose, we chose to analyze Populalarity in reference to Tracks, Artists and Genres.

#### Tracks
The Tracks dataset examines the physical features of each individual track. This analyses will be focusing on the features listed below. 

* acousticness
* instrumentalness
* speechiness
* danceability
* energy
* valence
* liveness
* temp
* loudness
* explicit

A more detailed description of the features can be found [here](https://developer.spotify.com/documentation/web-api/reference/#endpoint-get-audio-features).

#### Artists
In terms of Artists, we are only concerned with the followers count.

#### Genres
As songs within a genre generally share similar features, gauging Popularity by Genre provides a valuable perspective

The above dimensions look primarily at the properties of the songs themselves. In order to bolster the accuracy of our analysis, it is also important to account for listener behaviour, which we will do be considering the number of times that a song appears on a unqiue playlist. The playlist dataset was taken directly from the [Spotify Research Datasets.](https://research.atspotify.com/datasets/) 

While robust, the datasets require cleaning in order to merge them on the track_id. In order to ensure accuracy and integrity of our analysis, steps were taken to clean the dataset including, but not limited to:

1. Cleaning of null values
2. Removal of duplicate values
3. Streamlining features
4. Creation of artist_popularity and tracks_popularity classifiers
5. Scaling and normalizing of data

The final datasets that will be used for the analysis can be found [here](https://drive.google.com/drive/folders/17HUn1sSz_eTYTjKz1lcZEC0mF0mMt7H9?usp=sharing) 

### Purpose:
* Through analysis of what defines a high Popularity index, we hope to better understand the 'phenomenon' identified by [The Rolling Stones:](https://www.rollingstone.com/pro/news/top-1-percent-streaming-1055005/) why is it that a platform that should theoretically encourage a more even distribution of listeners per track still resulted in the top 1% of artists monopolizing 90% of all streams?

#### Goals

* What features of a song contribute to its overall popularity and which are the most significant?
* In what way does artist popularity impact the performance of their songs?
* Does the frequency at which a song appears on a unique playlist play a factor?

### Model

Preprocessing steps and feature selection:
1. Correlation Anaylsis
2. Describe target statistics and check the frequency distribution
3. Final decision on object features to keep, covert or drop
4. Assign a variable to hold the frequency of artists_name instead of a categorical value
5. Streamline release_date to "year"
6. Drop redundant categorical columns
7. Classify the counts of the genres colum to 10 groups with different frequencies and then encode the categorical data to numeric values
8. Final feature selection and performance analysis using the Random Forest model

Result: Keep All Features

* While some features showed low correlation, this knowledge still contributes to developing sn understanding of what _doesn't_ affect the Populairty index.

Moelling

The following models were examined on two classifiers: artist_popularity and tracks_popularity. Below are summaries for tracks_popularity. For the summaries of both tracks_popularity and artist_popularity, please refert to the [Slides documentation.](https://docs.google.com/presentation/d/11CgZVxAH2_xvv5FXoSW-5RmUFnX69TW4L199me3wOss/edit?usp=sharing)

#### Model 1: Logistic Regression (tracks_popularity)

![lr_summary](https://github.com/halmasieh/Spotify_Analysis/blob/Fiel_Branch/Resources/README_links/logistic_regression.png)

#### Model 2: Easy Ensemble AdaBoost Classifier (tracks_popularity)

![eea_summary](https://github.com/halmasieh/Spotify_Analysis/blob/Fiel_Branch/Resources/README_links/EEA.png)

#### Model 3: Decision Trees (tracks_popularity)

![dt_summary](https://github.com/halmasieh/Spotify_Analysis/blob/Fiel_Branch/Resources/README_links/decision_trees.png)

#### Model 4: Random Forest (tracks_popularity)

![rf_summary](https://github.com/halmasieh/Spotify_Analysis/blob/Fiel_Branch/Resources/README_links/random_forest.png)

#### Model 5: K-Fold Cross Validation (tracks_popularity)
The Median Accuracy Score for the K-Fold cross validation, scuh that k=10, is 0.82 and the ROC curve of all the folds indicates one area. There are no significient changes to the fold accuracy score.

For further details regarding the K-Fold Cross Validation as well as the other models used, please see [here](https://github.com/halmasieh/Spotify_Analysis/blob/Homa_branch/ML_models_target_artists.ipynb)

#### Results (tracks_popularity)

The reported results for both classifiers and accuracy cores show that the Random Forest Classifier is the most compatible with both datasets
![roc_curve](https://github.com/halmasieh/Spotify_Analysis/blob/Fiel_Branch/Resources/README_links/results.png)

### Analysis

With the data cleaned and the model run, the final step is to analyze the findings.

In order to present the information in a coherent and digestible form, we will leverage Tableau to visualize the outcomes and discuss the findings of this analysis.

 [Spotify Analysis Dashboard](https://public.tableau.com/app/profile/ranvir.singh.gill/viz/Spotify_Analysis_16222616687520/Story1)

#### Key Points:

* Popularity by Tracks v Artist - Perhaps unsurprisingly, the trend indicates that the more poplar the artist, the more popular the track. That said, it is also possible that a popular artist will have an unpopular track. (The same is not true for the reverse). From this we know that the popularity of a track is base on more than just artist preference/popularity. There must be other factors at play.

* Drivers of Track Popularity - A comparison of the Popularity of a song relative to its physical features that were previously outlined above. Descriptions of these features provided by the developers of the Spotify Web API can be found [here.](https://developer.spotify.com/documentation/web-api/reference/#endpoint-get-audio-features)

* Track Popularity over the Years - On first glance, the data strongly suggests that the more recently the song was released, the more popular it will be. While Spotify trends can be used to analyze the popularity of songs, it is also an indication of listener behaviour and a descriptor of the listener population. 

### Technologies to be used

Data Hosting
* SQL

ETL & Analysis
* Python / Jupyter Notebooks

Outcome / Dashboard
* Tableau

Presentation
* Google Slides

Communication
* Slack
* Zoom
* Google Meets

## Methods of Communication and Conflict Resolution
Daily communication regarding general discussion and deliverable updates will take place in a private channel in Slack. Group members are expected to participate in an open dialogue to share ideas, concerns and status updates. Rough documents will be uploaded to Slack to for purposes of feedback and all approved raw data will be committed to the Resources folder  in the project repository for quick access. Once group members have completed a deliverable, it will be uploaded to the project repository on GitHub as a new branch where it will be reviewed and committed to the master branch accordingly.

In addition to attending the weekly sessions, additional video conferences may be held on Zoom/Google Meet on an as needed basis. The time and date of said sessions will be decided based on necesseity and group availability. All scheduling will be conducted via Slack to ensure complete transparency.

Conflict resolution will be decided by a majority rule. That said, all group members are expected to maintain an open mind and conduct themselves respecfully and for the purposes of the team objective. 