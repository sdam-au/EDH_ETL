[![License: CC BY-NC-SA 4.0](https://licensebuttons.net/l/by-nc-sa/4.0/80x15.png "Creative Commons License CC BY-NC-SA 4.0")](https://creativecommons.org/licenses/by-nc-sa/4.0/)
![Project_status](https://img.shields.io/badge/status-in__progress-brightgreen "Project status logo")


# SDAM Project Pilot Workflow for accesing and analyzing the EDH dataset ('quantitative epigraphy in 2020')
This repository contains scripts for accesing and analysing epigraphic datasets from the API of the [Epigraphic Database Heidelberg](https://edh-www.adw.uni-heidelberg.de/data/api).
The repository will serve as a template for SDAM future collaborative research projects in accesing and analysing large digital datasets.

## Dataset 
The EDH dataset can be obtained in two ways:

a) via the Epidoc XML files available at https://edh-www.adw.uni-heidelberg.de/data/export

b) via the web API available at https://edh-www.adw.uni-heidelberg.de/data/api

The current workflow combines the contents of JSON, XML files and geospatial data from EDH (GeoJSON, https://edh-www.adw.uni-heidelberg.de/download/edhGeographicData.json) and is saved as JSON.

The workflow is designed so we can access the dataset via API, tranform it into JSON and then save it in the SDAM project repository in Sciencedata.dk. If we are unable to access the Sciencedata.dk, please contact us at sdam.cas@list.au.dk. A separate Python package ```sddk``` was created specifically for this purpose, see https://github.com/sdam-au/sddk. If you want to save the dataset in your preferred location, scripts need to be modified.

## Scripts

### Data accessing scripts
Primarily we use Python to access the API (in Google Colab notebooks) and then R and Python to analyse the data. The scripts can be found in the folder ```scripts```.

The data via the API are easily accessible and have been extracted by means of R and Python in a rather straigtforward way. To obtain the whole dataset of circa 80,000 inscriptions into a Python dataframe takes about 12 minutes (see the respective [script 1_1](https://github.com/sdam-au/edh_workflow/blob/master/scripts/1_1_py_EXTRACTION_edh-inscriptions-from-web-api.ipynb)). We have decided to save the dataframe as JSON for interoperability reasons between Python and R.

However, the dataset from the API is a simplified one (when compared with the records online and in XML), primarily to be used for queries in the web interface. For instance, the API data encode the whole information about dating by means of two variables: "not_before" and "not_before". This makes us curious about how the data translate dating information like "around the middle of the 4th century CE." etc. 

Therefore, we decided to enrich the JSON created from the API files with data from the original XML files, which also including some additional variables (see [script 1_2](https://github.com/sdam-au/edh_workflow/blob/master/scripts/1_2_py_EXTRACTION_edh-xml_files.ipynb)).

To enrich the JSON with geodata available via EDH, we have used the following script, so the epigraphic dat acontains also a geospatial information (see [script 1_3](https://github.com/sdam-au/edh_workflow/blob/master/scripts/1_3_py_MERGING_API_GEO_and_XML.ipynb)).

### Data analyzing scripts 
Figures and exports with the outputs of analysed dataset that were produced by the scripts below are stored in the folder ```reports```.

2. Diachronic study (Quantitative chronological analysis of inscriptions, under development
[script_2_Temporal in Python](https://github.com/sdam-au/edh_workflow/blob/master/scripts/2_py_TEMPORAL-ANALYSIS_research.ipynb))

3. Geospatial study (Quantitative spatial analysis of inscriptions, under development
[script_2_Spatial in Python](https://github.com/sdam-au/edh_workflow/blob/master/scripts/2_py_SPATIAL-ANALYSIS_research.ipynb))

# Script accessing workflow (internal SDAM project):

## Offline scenario

1. Download scripts from Github and run locally in Jupyter Notebook, but check the dependencies and libraries. 
2. The documentation needs further tests and elaboration.

## Online scenario

1. Go to Google Colab & sign in with your Google email account. 
2. Create a new notebook, select Github tab.
3. Paste in the URL of the notebook on Github (choose from dropdown menu, if you are using the same email account for Github and for Google).
4. Ingest and save to your own Goodle drive into Google Colab folder (it may be done automatically).
5. Google Colab includes all basic libraries but requires an install of unusual libraries once per session.
6. Committing any changes back to Github has to be further tested.








