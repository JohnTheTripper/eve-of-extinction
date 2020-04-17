# Eve of Extinction

## Project Sumarry

This project aims to train a classification model that can predict a given animal species' extinction risk based on its characteristics and habitat. Eight countries were selected for the study based on availability of data. The dataset used for training was scraped from the National Red List, a subset of IUCN Red List, which asigns thousands of species across the world with an IUCN status from least concern to extinct. We then gathered deforestation data and Paris climate action commitment ratings on the ten countries used in the study along with green house gasses emissions data. By using this data and applying novel methods of combining species' attributes and respective countrys' environmental statistics, we attempted to explore the importance of various characteristics of the species and their environment and assess which factors were the most significant when predicting risk of extinction.


# Repository

This repository contains a notebook with the following contents:
1. Data cleaning
2. EDA
3. Feature engineering
4. Modeling

## Data Cleaning and EDA

Data cleaning and EDA can be viewed in detail in the jupyter notebook.

## Feature Engineering

Several additional features were added and engineered, some relating to the countries in which the species live and others relating to the species themselves:

### Country Features:
 - Commitment rating (0-5) - Assigned by Climate Action Tracker which takes into account a wide variety of national statistics on    everything from aviation, meat consumption, to political tendencies for positive environmental policy.
 - Deforestation - The amount of forest land cover as a proportion of forest land cover present in 1990.
 - Green House Gas Emissions - The amount of green house gasses emitted by a country divided by their respective land area.
![forest](https://github.com/JohnTheTripper/eve-of-extinction/blob/master/images/forest.png)
![country](https://github.com/JohnTheTripper/eve-of-extinction/blob/master/images/country.png)
![country emissions](https://github.com/JohnTheTripper/eve-of-extinction/blob/master/images/country%20emissions.png)


### Species Features:
 - Taxonomic Ranks - Phylum and Class
 - Class Forest Dependence (0-3) - Ranking that defines the importance of forestry for individual taxonomic classes
 - Class Emission vulnerability (0-3) - Ranking that defines the level of impact carbon emissions have on individual classes.
 - IUCN threat level
![hist](https://github.com/JohnTheTripper/eve-of-extinction/blob/master/images/hist.png)
![extinct](https://github.com/JohnTheTripper/eve-of-extinction/blob/master/images/extinct.png)


### Interaction Features
 - Country Deforestation x Class Forest Dependence
 - Country Green House Gas Emission x Class Emission Vulnerability
 
## Models

We evaluated several classifier models, starting with the basic logistic classifier, going up to Grid Searches of advanced ensemble models. We used Grid Search to chose a Gradient Boost classifier. As part of our testing of country x class interactions, we evaluated this model on both the independent and interaction dataframes.

Both models performed pretty similarly, neither seemingly having an advantage over the other.

They both had an accuracy of about 50%, though it's worth a reminder that this is a multi-class classification exercise with six classes. The confusion matrix provides a nice overview of how items were (mis-)classed. With a scale of 0-5, 0 being the best ("least concern") and starting in the top-left corner, the majority of misclassifications came below the diagonal, meaning the classifiers were optimistic and ranked species lower than they actually are. This may have been caused by the class imbalance - the histogram of extinction/endangerment ranks skewed toward the lower end of the scale. It's also notable that most misclassifications were only off by 1 - a 1 predicted as a 0, a 2 predicted as a 1, etc.

This exercise experimented with the combination of features from two separate domains: country enviornmentalism and taxonomy-based species vulnerabilities. Further improvements could include the addition of more of these types of interaction-based features, more countries, and/or more species classes.

## Key Features

Birds, insects, country emissions, emissions vulnerability, country deforestation, and forest dependence were all key features.
![feature_imp](https://github.com/JohnTheTripper/eve-of-extinction/blob/master/images/feature_imp.png)

# Impact of Study Findings

From our limited features and species/country data, the best conclusions we can draw are as follows:

Conservation organizations should prioritize birds and insects for conservation efforts as they are the most affected by the correlated country characteristics. Countries should focus on cutting down carbon emissions and limiting deforestation. 

More interaction features between animal characteristics and their respective nations’ environmental policies, pollution, etc. would result in a better model and more concrete conclusions/recomendations. 



