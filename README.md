# ETL workflow for quantitative analysis of inscriptions from the EDH dataset
* ETL

[![License: CC BY-NC-SA 4.0](https://licensebuttons.net/l/by-nc-sa/4.0/80x15.png "Creative Commons License CC BY-NC-SA 4.0")](https://creativecommons.org/licenses/by-nc-sa/4.0/)
![Project_status](https://img.shields.io/badge/status-in__progress-brightgreen "Project status logo")

---

## Purpose
This repository contains scripts for accesing, extracting and transforming epigraphic datasets from the [Epigraphic Database Heidelberg](https://edh-www.adw.uni-heidelberg.de/). The repository will serve as a template for SDAM future collaborative research projects in accesing and analysing large digital datasets.

The scripts access the main dataset via a web API, tranform it into one dataframe object, merge and enrich these data with geospatial data and additional data from XML files, and save the outcome to SDAM project directory on sciencedata.dk and the finished product on Zenodo. Since the most important data files are in a [public folder](https://sciencedata.dk/shared/b6b6afdb969d378b70929e86e58ad975), you can use and re-run our analyses even without a sciencedata.dk account and access to our team folder. If you face any issues with accessing the data, please contact us at sdam.cas@list.au.dk.

A separate Python package ```sddk``` was created specifically for accessing sciencedata.dk from Python (see https://github.com/sdam-au/sddk). If you want to save the dataset in a different location, the scripts might be easily modified.

## Authors
* Petra Heřmánková [![](https://orcid.org/sites/default/files/images/orcid_16x16.png)](https://orcid.org/0000-0002-6349-0540) SDAM project, petra.hermankova@cas.au.dk
* Vojtěch Kaše [![](https://orcid.org/sites/default/files/images/orcid_16x16.png)]([0000-0002-6601-1605](https://www.google.com/url?q=http://orcid.org/0000-0002-6601-1605&sa=D&ust=1588773325679000)) SDAM project, vojtech.kase@gmail.com

## License
[CC-BY-SA 4.0](https://github.com/sdam-au/EDH_ETL/blob/master/LICENSE.md)

## How to cite us

### 2022 version 2
DATASET 2022: `Heřmánková, Petra, & Kaše, Vojtěch. (2022). EDH_text_cleaned_2022_XX_XX (v2.0) [Data set]. Zenodo. http://doi.org/10.5281/zenodo.XXXXXX`
[http://doi.org/10.5281/zenodo.XXXXXX](http://doi.org/10.5281/zenodo.XXXXXX)

SCRIPTS 2022: `Heřmánková, Petra, & Kaše, Vojtěch. (2022). sdam-au/EDH_ETL: Scripts (v2.0). Zenodo. https://doi.org/10.5281/zenodo.XXXXXX` [https://doi.org/10.5281/zenodo.XXXXXX](https://doi.org/10.5281/zenodo.XXXXXXX)

The 2022 datasets contains XXX cleaned and streamlined Latin inscriptions from the Epigraphic Database Heidelberg (EDH, https://edh-www.adw.uni-heidelberg.de/), aggregated on 2022/XX/XX, created for the purpose of a quantitative study of epigraphic trends by the Social Dynamics in the Ancient Mediterranean Project (SDAM, http://sdam.au.dk). The dataset contains XX attributes with original and streamlined data. Compared to the 2021 dataset, there are XX,XXX more inscriptions and XX less attributes containing redundant legacy data, thus the entire dataset is approximately the same size but some of the attributes are streamlined (XXX MB in 2022 compared to XXX MB MB in 2021). Some of the attribute names have changed for better consistency, e.g. Material > material, Latitude > latitude; some attributes are no longer available due to the changes in the EDH, e.g. start_yr, notes_dating, inscription_stripped_final; and some new attributes were added due to the streamlining of the ETL process, e.g. clean_text_conservative. For full overview, see the Metadata section.

**Metadata**

[EDH 2022 dataset metadata](XXX) with descriptions for all attributes

### 2022 version 1

DATASET 2021: `Heřmánková, Petra, & Kaše, Vojtěch. (2021). EDH_text_cleaned_2021_01_21 (v1.0) [Data set]. Zenodo. http://doi.org/10.5281/zenodo.4888168`
[http://doi.org/10.5281/zenodo.4888168](http://doi.org/10.5281/zenodo.4888168)

SCRIPTS 2021: `Heřmánková, Petra, & Kaše, Vojtěch. (2021). sdam-au/EDH_ETL: Scripts (v2.0). Zenodo. https://doi.org/10.5281/zenodo.6478243` [https://doi.org/10.5281/zenodo.6478243](https://doi.org/10.5281/zenodo.6478243)


**Metadata**

[EDH 2021 dataset metadata](https://github.com/sdam-au/EDH_ETL/blob/master/EDH_2021_dataset_metadata_SDAM.csv) with descriptions for all attributes.

## Data

### The original raw data
**The original data** come from two sources:

1. the Epidoc XML files available at https://edh.ub.uni-heidelberg.de/data (inscriptions)
1. the web API available at https://edh.ub.uni-heidelberg.de/data/api (inscriptions and geospatial data)

The scripts merge data from these two sources into Pandas dataframe, which is then exported into one JSON file for further usage. A separate Python package ```sddk``` was created specifically for accessing sciencedata.dk from Python (see https://github.com/sdam-au/sddk). If you want to save the dataset in a different location, the scripts might be easily modified. You can access the file without having to login into sciencedata.dk. Here is a path to the file on sciencedata.dk: 
`SDAM_root/SDAM_data/EDH/public` folder on sciencedata.dk or alternatively as `https://sciencedata.dk/public/b6b6afdb969d378b70929e86e58ad975/`

To access the files created in previous steps of the ETL process, you can use the dataset from the public folder, or you have to rerun all scripts on your own.

### The final (streamlined) dataset
is produced by the scripts in this repository is called `EDH_text_cleaned_[timestamp].json` and published on Zenodo in all its versions, for details and links see `How to cite us` section above. 

Additionally, the identical dataset can be accessed via Sciencedata.dk: `SDAM_root/SDAM_data/EDH/public` folder on sciencedata.dk or alternatively as `https://sciencedata.dk/public/b6b6afdb969d378b70929e86e58ad975/`.

## Scripts

### Data accessing scripts

We use Python scripts (Jupyter notebooks) for accessing the API & extracting data from it, parse the XML files for additional metadata and combining these two reseources into one. Subsequently, we use both R and Python for further cleaning and transformming the data. The scripts can be found in the folder ```scripts``` and they are named according to the sequence they should run in.

---

#### [1_0_py_EXTRACTING-GEOGRAPHIES.ipynb](https://github.com/sdam-au/EDH_ETL/blob/master/scripts/1_0_py_EXTRACTING-GEOGRAPHIES.ipynb)

The data via the API are easily accessible and might be extracted by means of R and Python in a rather straigtforward way. 
First we extract the geocordinates from the public API, using the [script 1_0](https://github.com/sdam-au/EDH_ETL/blob/master/scripts/1_0_py_EXTRACTING-GEOGRAPHIES.ipynb). 

_Extracting geographical coordinates_
|| File | Source commentary |
| :---       |         ---: |         ---: |
| input |`edhGeographicData.json`| containting all EDH geographies, loaded from [https://edh.ub.uni-heidelberg.de/data/api](https://edh.ub.uni-heidelberg.de/data/api)
| output | `EDH_geo_dict_[timestamp].json` ||

#### [1_1_py_EXTRACTION_edh-inscriptions-from-web-api.ipynb](https://github.com/sdam-au/EDH_ETL/blob/master/scripts/1_1_py_EXTRACTION_edh-inscriptions-from-web-api.ipynb)

As a next step we access the public API to access and download all the incriptions. To obtain the whole dataset of circa 81,000+ inscriptions into a Python dataframe takes about 12 minutes (see the respective [script 1_1](https://github.com/sdam-au/EDH_ETL/blob/master/scripts/1_1_py_EXTRACTION_edh-inscriptions-from-web-api.ipynb)). We have decided to save the dataframe as a JSON file for interoperability reasons between Python and R.
 
_Extracting all inscriptions from API_
|| File | Source commentary |
| :---       |         ---: |         ---: |
| input| requests to [https://edh.ub.uni-heidelberg.de/data/api](https://edh.ub.uni-heidelberg.de/data/api)||
| output| `EDH_onebyone[timestamp].json`||

#### [1_2_py_EXTRACTION_edh-xml_files.ipynb](https://github.com/sdam-au/EDH_ETL/blob/master/scripts/1_2_py_EXTRACTION_edh-xml_files.ipynb)

However, the dataset from the API is a simplified one (when compared with the records online and in XML), primarily to be used for queries in the web interface.  For instance, the API data encode the whole information about dating by means of two variables: "not_before" and "not_before". This makes us curious about how the data translate dating information like "around the middle of the 4th century CE." etc. Therefore, we decided to enrich the JSON created from the API files with data from the original XML files, which also including some additional variables (see [script 1_2](https://github.com/sdam-au/EDH_ETL/blob/master/scripts/1_2_py_EXTRACTION_edh-xml_files.ipynb)).

_Extracting XML files_
|| File | Source commentary |
| :---       |         ---: |         ---: |
| input| `edhEpidocDump_HD[first_number]-HD[last_number].zip`| [https://edh.ub.uni-heidelberg.de/data/download](https://edh.ub.uni-heidelberg.de/data/download)
| output| `EDH_xml_data_[timestamp].json`||

#### [1_3_py_MERGING_API_GEO_and_XML.ipynb](https://github.com/sdam-au/EDH_ETL/blob/master/scripts/1_3_py_MERGING_API_GEO_and_XML.ipynb)

To enrich the JSON with geodata extracted in the script 1_0, we have developed the following script: [script 1_3](https://github.com/sdam-au/EDH_ETL/blob/master/scripts/1_3_py_MERGING_API_GEO_and_XML.ipynb)).

_Merging geographies, API, and XML files_
|| File | Source commentary |
| :---       |         ---: |         ---: |
| input 1 | `EDH_geographies_raw.json`| [https://edh.ub.uni-heidelberg.de/data/download](https://edh.ub.uni-heidelberg.de/data/download)|
| input 2| `EDH_onebyone[timestamp].json`||
| input 3| `EDH_xml_data_[timestamp].json`|| 
| output| `EDH_merged_[timestamp].json`||
  
#### [1_4_r_DATASET_ATTRIBUTES_CLEANING.Rmd](https://github.com/sdam-au/EDH_ETL/blob/master/scripts/1_4_r_DATASET_ATTRIBUTES_CLEANING.Rmd)

In the next step we clean and streamline the API attributes in a reproducible way in R, (see [script 1_4](https://github.com/sdam-au/EDH_ETL/blob/master/scripts/1_4_r_DATASET_ATTRIBUTES_CLEANING.Rmd)) so they are ready for any future analysis. We keep the original attributes along with the new clean ones.

_Cleaning and streamlining attributes_
|| File | Source commentary |
| :---       |         ---: |         ---: |
| input| `EDH_merged_[timestamp].json`|The current script works with JSON file containing all merged inscriptions.|
| output| `EDH_attrs_cleaned_[timestamp].json`||


#### [1_5_r_TEXT_INSCRIPTION_CLEANING](https://github.com/sdam-au/EDH_ETL/blob/master/scripts/1_5_r_TEXT_INSCRIPTION_CLEANING.Rmd)

The cleaning process of the text of inscriptions is in the [script 1_5](https://github.com/sdam-au/EDH_ETL/blob/master/scripts/1_5_r_TEXT_INCRIPTION_CLEANING.Rmd).

_Cleaning and streamlining of the text of the inscription_
|| File | Source commentary |
| :---       |         ---: |         ---: |
| input| `EDH_attrs_cleaned_[timestamp].json`|The current script works with JSON file containing all inscriptions will their streamlined attributes.|
| output| `EDH_text_cleaned_[timestamp].json` ||

**The following scripts document the basic usage cases for Python and R (they do not change the dataset, only demonstrate the access to the data using both languages)**

#### [2_py_PYTHON_USAGE_TEST.ipynb](https://github.com/sdam-au/EDH_ETL/blob/master/scripts/2_py_PYTHON_USAGE_TEST.ipynb)

Script demonstrating loading the dataset to Python via Sciencedata.dk (with or without credentials), using `sddk` package.

#### [2_r_R_USAGE_TEST.Rmd](https://github.com/sdam-au/EDH_ETL/blob/master/scripts/2_r_R_USAGE_TEST.Rmd)

Script demonstrating loading the dataset to R via Sciencedata.dk (without credentials).

---

## Related publications

Heřmánková, P., Kaše, V., & Sobotkova, A. (2021). Inscriptions as data: Digital epigraphy in macro-historical perspective. _Journal of Digital History_, 1(1), 99. https://doi.org/10.1515/jdh-2021-1004
 - _the article working with version 1, but version 2 follows the same principles. Some attribute names may vary in the version 2 as well as the contents of the dataset (that reflect the changes made by the EDH)._


