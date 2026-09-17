# observatory profile
The profiles for the RO-Crates for the various "observatory-{obsid}-crate" repositories.

## jinja templates (for pysembench)
[templates](https://github.com/emo-bon/observatory-profile/tree/feature/sequenceinfo_extension/templates) The folder containing the templates used to convert the CSV format logsheets into turtle

## Logsheet schema
[logsheet schema](https://github.com/emo-bon/observatory-profile/blob/feature/sequenceinfo_extension/logsheet_schema_extended.csv) describes the schema of the logsheets, i.e. what the columns are, their data types, their semantic links. This is input to the quality control action (for py-data-rules) and the templates

The metadata included in this spreadsheet are the following:
* An column that tells us if all the information for the column has been found, or comments to keep an eye on (for internal management use only)
* The column name in the EMO BON logsheets
* The data type (xsd) that the cells should be filled with i the google sheets
* The data type that the these items should be formatted as in the json/ttl files to be created from the logsheets
* Notes regarding the formatting of those columns which contain multi-value entries (;-separated)
* The observable property URL (or NA if not applicable)
* The unit for the column (or NA)
* The unit URL (or NA)
* The particular type of logsheet this applies to - being currently water, soil, or water;soil. (The hard-bottom still need to be added)
* The tab of the googlesheet (which are the source of the logsheets) that the column will be found in
* The optional/mandatory requirement
* The definition of the column
* An example
* A yes if we need to define this particular column ourselves, in our own vocab (blank if not)
* Comments (for internal management use only)

## Workflow configuration
In [workflows](https://github.com/emo-bon/observatory-profile/blob/main/.github/workflows/workflow.yml) are files to control the workflows (actions) that run on observatories. 
