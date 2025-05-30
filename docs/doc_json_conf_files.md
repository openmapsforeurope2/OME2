# How to fill a json configuration file for the model conversion tool?

### General parameters
The first step consists in filling the general parameters of the transformation:
~~~
    "country_code": "fi",
    "source_srid": "3067",
    "target_srid": "3035",
    "target_country_field": "country",
~~~

* country_code refers to the one used in the configuration file name, which is usually the "main" country code of the country to be processed. If the dataset contains several country codes (e.g. France and its overseas territories), please see below how to proceed.
* source_srid refers to the EPSG number of the Spatial Reference Identifier (SRID) or coordinate system used in the source tables provided by the country. It can usually be determined in pgAdmin with a simple SQL query:
  ~~~
  SELECT Find_SRID('<schema name>','<table name>','<geometry column name>');
  ~~~
  If the query does not work, it is possible to open the table in QGIS and check which SRID is detected.
* target_srid refers to the coordinate reference system of the OME2 database. It is set to 3035 and must not be modified.
* target_country_field indicates which field is used to store country codes in the OME2 database. It must not be modified.

##### Particular case: dataset with several country codes and SRIDs
~~~
    "country_code": "fr",
    "country_code_list": ["fr","gf","gu","gp","mq","re","yt","bl","mf","pm"],
    "source_srid": "CASE gcms_territoire WHEN 'FXX' THEN 2154 WHEN 'GLP' THEN 4559 WHEN 'GUF' THEN 2972 WHEN 'H_T' THEN 4326 WHEN 'MTQ' THEN 4559 WHEN 'MYT' THEN 4471 WHEN 'REU' THEN 2975 WHEN 'SPM' THEN 4467 END",
    "target_srid": "3035",
    "target_country_field": "country",
~~~
