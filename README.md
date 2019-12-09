# SDAM Project Workflow for analyzing the EDH datase

Perhaps this repository will serve us as a template for our future collaborative research projects.

Here we will put together our scripts in R and Python for manipulating and anylizing the EDH dataset.

The EDH dataset can be obtained in two ways:
a) via the XML files downloaded;
b) via the web API.

The data via the API are easily accessible and have been extracted by means of R and Python in a rather straigtforward way. To obtain the whole dataset of circa 72,000 inscriptions into a Python dataframe takes about 12 minutes (see the respected Python notebook).

However, the dataset from the API is a simplified one, primarily to be used for queries in the web interface. For instance, the API data encode the whole information about dating by means of two variables: "not_before" and "not_before". This makes us curious about how the data translate dating information like "around the middle of the 4th century CE." etc. Therefore, we also started to explore the original XML files, which also including some additional variables.
