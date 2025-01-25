# SpringboardCapstoneTwo

## Project Overview

Add your project details here.

This project aims to build a machine learning model to predict phishing url from a dataset containing both 
phishing and legitimate urls. It tries to achieve this by exploiting the inherent characteristics (url len,
top level domain similarity, obfuscation status, entropy of domain etc.) of a phishing url rather than 
extracting information (robot_text, css values, WHOISE information etc.) from the internet. 

In search for a comprehensive dataset containing both phishing and legitimate urls, previously we came across 
some datasets that has many useful features. But one of the dataset contained the problem of encoding. Most 
probably the problem was due to a data corruption which may occure during the data scraping phase. There was 
another dataset with no clear indication of how some of the features are generated. This dataset that we are 
working with is added a year ago in the Kaggle the author made a good effort to make this comprehensive.