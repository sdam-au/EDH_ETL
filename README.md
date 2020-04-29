[![License: CC BY-NC-SA 4.0](https://licensebuttons.net/l/by-nc-sa/4.0/80x15.png "Creative Commons License CC BY-NC-SA 4.0")](https://creativecommons.org/licenses/by-nc-sa/4.0/)
![Project_status](https://img.shields.io/badge/status-in__progress-brightgreen "Project status logo")


# SDAM Project Pilot Workflow for accesing and analyzing the EDH dataset ('quantitative epigraphy in 2020')
This repository contains scripts for accesing and analysing epigraphic datasets from the [Epigraphic Database Heidelberg](https://edh-www.adw.uni-heidelberg.de/data/api). The repository will serve as a template for SDAM future collaborative research projects in accesing and analysing large digital datasets.

The scripts  access the dataset via API, tranform it into a JSON, merge these data  with some other data, and save the outcome to SDAM project directory in sciencedata.dk. If you are unable to access the sciencedata.dk, please contact us at sdam.cas@list.au.dk. A separate Python package ```sddk``` was created specifically for this purpose, see https://github.com/sdam-au/sddk. If you want to save the dataset in your preferred location, the scripts need to be modified.

## Data
**The final dataset** produced by the scripts in this repo is called `EDH_utf8.json` and is located in our project datastorage on `sciencedata.dk`. To access this file, you either need a sciencedata.dk account and an access to `SDAM_root` folder (owned by Vojtěch Kaše), or you have to rerun all scripts on your own. Here is a path to the file on sciencedata.dk: 

`SDAM_root/SDAM_data/EDH/EDH_utf8.json`

Alternatively, you can also use `SDAM_root/SDAM_data/EDH/EDH_inscriptions_rich.json`. It is the same, just using a different encoding.

To upload these data into python as a pandas dataframe, you can use this (using th [sddk](https://pypi.org/project/sddk/) package):

```python
!pip install sddk
import sddk
auth = sddk.configure_session_and_url("SDAM_root", "648597@au.dk")
EDH_utf8 = sddk.read_file("SDAM_data/EDH/EDH_utf8.json", "df", auth)
```

**The original data** from the scripts come from two sources:

a) the Epidoc XML files available at https://edh-www.adw.uni-heidelberg.de/data/export

b)  the web API available at https://edh-www.adw.uni-heidelberg.de/data/api (inscriptions and findspots)

The scripts merge data from these sources into on pandas dataframe, which is then exported into one JSON file for further usage

## Scripts

### Data accessing scripts
Primarily we use Python to access the API (in Google Colab notebooks) and then R and Python to analyse the data. The scripts can be found in the folder ```scripts```.

The data via the API are easily accessible and have been extracted by means of R and Python in a rather straigtforward way. To obtain the whole dataset of circa 80,000 inscriptions into a Python dataframe takes about 12 minutes (see the respective [script 1_1](https://github.com/sdam-au/edh_workflow/blob/master/scripts/1_1_py_EXTRACTION_edh-inscriptions-from-web-api.ipynb)). We have decided to save the dataframe as JSON for interoperability reasons between Python and R.

However, the dataset from the API is a simplified one (when compared with the records online and in XML), primarily to be used for queries in the web interface. For instance, the API data encode the whole information about dating by means of two variables: "not_before" and "not_before". This makes us curious about how the data translate dating information like "around the middle of the 4th century CE." etc. 

Therefore, we decided to enrich the JSON created from the API files with data from the original XML files, which also including some additional variables (see [script 1_2](https://github.com/sdam-au/edh_workflow/blob/master/scripts/1_2_py_EXTRACTION_edh-xml_files.ipynb)).

To enrich the JSON with geodata available via EDH, we have used the following script, so the epigraphic dat acontains also a geospatial information (see [script 1_3](https://github.com/sdam-au/edh_workflow/blob/master/scripts/1_3_py_MERGING_API_GEO_and_XML.ipynb)).


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








