# SDAM Project Workflow for accesing and analyzing the EDH dataset

This repository contains scripts for accesing and analysing epigraphic datasets from the API of the Epigraphic Database Heidelberg (https://edh-www.adw.uni-heidelberg.de/data/api).
The repository will serve as a template for SDAM future collaborative research projects in accesing and analysing large digital datasets.

## Dataset 
The EDH dataset can be obtained in two ways:

a) via the XML files downloaded https://edh-www.adw.uni-heidelberg.de/data/export

b) via the web API https://edh-www.adw.uni-heidelberg.de/data/api

The workflow is designed so we can access the dataset via API, tranform it into JSON and then save it in the SDAM project repository in Sciencedata.dk. If we are unable to access the Sciencedata.dk, please contact us at sdam.cas@list.au.dk.

The data via the API are easily accessible and have been extracted by means of R and Python in a rather straigtforward way. To obtain the whole dataset of circa 72,000 inscriptions into a Python dataframe takes about 12 minutes (see the respected Python notebook).

However, the dataset from the API is a simplified one, primarily to be used for queries in the web interface. For instance, the API data encode the whole information about dating by means of two variables: "not_before" and "not_before". This makes us curious about how the data translate dating information like "around the middle of the 4th century CE." etc. Therefore, we also started to explore the original XML files, which also including some additional variables.

## Scripts
Primarily we use Python to access the API (in Google Colab notebooks) and then R and Python to analyse the data. The scripts can be found in the folder ```scripts```.






