# ETL Workflow for the Quantitative Analysis of the EDH dataset
* ETL

[![License: CC BY-NC-SA 4.0](https://licensebuttons.net/l/by-nc-sa/4.0/80x15.png "Creative Commons License CC BY-NC-SA 4.0")](https://creativecommons.org/licenses/by-nc-sa/4.0/)
![Project_status](https://img.shields.io/badge/status-in__progress-brightgreen "Project status logo")
---

## Purpose
This repository contains scripts for accesing and analysing epigraphic datasets from the [Epigraphic Database Heidelberg](https://edh-www.adw.uni-heidelberg.de/data/api). The repository will serve as a template for SDAM future collaborative research projects in accesing and analysing large digital datasets.

The scripts  access the dataset via API, tranform it into a JSON, merge and enrich these data with geospatial data, and save the outcome to SDAM project directory in Sciencedata.dk. If you are unable to access the sciencedata.dk, please contact us at sdam.cas@list.au.dk. A separate Python package ```sddk``` was created specifically for this purpose, see https://github.com/sdam-au/sddk. If you want to save the dataset in your preferred location, the scripts need to be modified.

## Authors
* Petra Heřmánková [![](https://orcid.org/sites/default/files/images/orcid_16x16.png)](https://orcid.org/0000-0002-6349-0540) SDAM project, petra@ancientsocialcomplexity.org
* Vojtěch Kaše [![](https://orcid.org/sites/default/files/images/orcid_16x16.png)]([0000-0002-6601-1605](https://www.google.com/url?q=http://orcid.org/0000-0002-6601-1605&sa=D&ust=1588773325679000)) SDAM project, vojtech.kase@gmail.com

## License
[CC-BY-SA 4.0](https://github.com/sdam-au/EDH_ETL/blob/master/LICENSE.md)


## Data
**The final dataset** produced by the scripts in this repo is called `EDH_cleaned[timestamp].json` and is located in our project datastorage on `sciencedata.dk`. To access this file, you either need a sciencedata.dk account and an access to `SDAM_root` folder (owned by Vojtěch Kaše), or you have to rerun all scripts on your own. Here is a path to the file on sciencedata.dk: 

`SDAM_root/SDAM_data/EDH/EDH_cleaned.json`

Alternatively, you can also use `SDAM_root/SDAM_data/EDH/EDH_inscriptions_rich.json`. It is the same, just using a different encoding.

**The original data** from the scripts come from two sources:

a) the Epidoc XML files available at https://edh-www.adw.uni-heidelberg.de/data/export (inscriptions)

b) the web API available at https://edh-www.adw.uni-heidelberg.de/data/api (inscriptions and geospatial data)

The scripts merge data from these sources into on pandas dataframe, which is then exported into one JSON file for further usage.

## Scripts

### Data accessing scripts
Primarily we use Python scripts (Jupyter notebooks) for accessing the API & extracting data from it, parse the XML files for additional metadata and combining these two reseources into one. Subsequently, we use both R and Python for further cleaning, transformming and analyzing the data. The scripts can be found in the folder ```scripts```.

The data via the API are easily accessible and might be extracted by means of R and Python in a rather straigtforward way. To obtain the whole dataset of circa 80,000 inscriptions into a Python dataframe takes about 12 minutes (see the respective [script 1_1](https://github.com/sdam-au/EDH_ETL/blob/master/scripts/1_1_py_EXTRACTION_edh-inscriptions-from-web-api.ipynb)). We have decided to save the dataframe as a JSON file for interoperability reasons between Python and R.

However, the dataset from the API is a simplified one (when compared with the records online and in XML), primarily to be used for queries in the web interface. ` For instance, the API data encode the whole information about dating by means of two variables: "not_before" and "not_before". This makes us curious about how the data translate dating information like "around the middle of the 4th century CE." etc. `

Therefore, we decided to enrich the JSON created from the API files with data from the original XML files, which also including some additional variables (see [script 1_2](https://github.com/sdam-au/EDH_ETL/blob/master/scripts/1_2_py_EXTRACTION_edh-xml_files.ipynb)).

To enrich the JSON with geodata available via EDH, we have developed the following script: [script 1_3](https://github.com/sdam-au/EDH_ETL/blob/master/scripts/1_3_py_MERGING_API_GEO_and_XML.ipynb)).

Script (see [script 1_4](https://github.com/sdam-au/EDH_ETL/blob/master/scripts/1_4_r_DATASET_CLEANING.Rmd)) cleans the epigraphic text to produce several versions of text of all inscriptions (ready for further text mining, quantitative analysis, NLP analysis etc). Details on the cleaning process and the decision behind individual steps of the model can be found in the repository [epigraphic_cleaning](https://github.com/sdam-au/epigraphic_cleaning). 


* [1_1_py_EXTRACTION_edh-inscriptions-from-web-api.ipynb](https://github.com/sdam-au/EDH_ETL/blob/master/scripts/1_1_py_EXTRACTION_edh-inscriptions-from-web-api.ipynb))
  * input: requests to [https://edh-www.adw.uni-heidelberg.de/data/api/inscriptions/search?](https://edh-www.adw.uni-heidelberg.de/data/api/inscriptions/search?)
  * output: `EDH_onebyone[timestamp].json`
  
* [1_2_py_EXTRACTION_edh-xml_files.ipynb](https://github.com/sdam-au/EDH_ETL/blob/master/scripts/1_2_py_EXTRACTION_edh-xml_files.ipynb)
  * input: `EDH_dump.zip`
  * output: `edh_xml_data_[timestamp].json`

* [1_3_py_MERGING_API_GEO_and_XML.ipynb](https://github.com/sdam-au/EDH_ETL/blob/master/scripts/1_3_py_MERGING_API_GEO_and_XML.ipynb).
  * input1: `EDH_geographies_raw.json`
  * input2: `EDH_onebyone.json`
  * input3: `edh_xml_data_[timestamp].json` (latest verified version: 2020-06-23)
  * output1: `EDH_merged_[timestamp]?.json`
  * output2: `EDH_utf8_sample.json`
  
* [1_4_r_DATASET_CLEANING.Rmd](https://github.com/sdam-au/EDH_ETL/blob/master/scripts/1_4_r_DATASET_CLEANING.Rmd)
  * input: `EDH_merged_[timestamp].json`
  * output: `EDH_cleaned_[timestamp].json` (latest verified version: 2020-06-26)


# Script accessing workflow:

To upload these data into **Python** as a pandas dataframe, you can use this (using th [sddk](https://pypi.org/project/sddk/) package):

```python
!pip install sddk
import sddk
auth = sddk.configure("SDAM_root", "648597@au.dk") # where "648597@au.dk is owner of the shared folder, i.e. Vojtěch
EDH_utf8 = sddk.read_file("SDAM_data/EDH/EDH_cleaned.json", "df", auth)
```

## Data storage: 

`SDAM_root/SDAM_data/EDH` folder on sciencedata.dk

## DOI
[Here will be DOI or some other identifier once we have it]

### References
[Here will go related articles or other sources we will publish/create]

## Screenshots
![Example screenshot](./img/screenshot.png)
TBA





