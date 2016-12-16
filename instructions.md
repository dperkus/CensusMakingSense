# Acquiring the data
##Census web site "American Factfinder"
* http://factfinder.census.gov/faces/nav/jsf/pages/index.xhtml
* Determine which tables contain the information that you need
** Start with the "popular tables"
** You can also try "Guided Search" and "Advanced Search"

## How to download census tables in csv format:
Here is the list of tables that I used: S1501, DP02, DP03, DP04, DP05

* http://factfinder.census.gov/faces/nav/jsf/pages/download_center.xhtml
* click on "I know the dataset or tables that I want to download"
* click "next"
* select a program: "American Community Survey"
* select a dataset: "2015 ACS 5-year estimates"
* click "Add to your Selections"
* click "next"
* Select a geographic type: "Census Tract= 140" or "5-Digit Zip Code Tabulation Area - 860"
* Select all
* click "Add to your Selections"
* click "next"
* select each of the the tables that you want to download.  S1501 will be on the 1st or 2nd page.  The DP tables will be on the last page 
* click "next"
* click "OK"
* it may take several minutes for your download files to be assembled
* click download
* unzip

# Prepping the data
## Which columns to use?  
It depends . . .

Most of the columns will not be useful.

Here is the list of columns that I used for my project 
https://github.com/dperkus/CensusMakingSense/blob/master/census_import_metadata.csv

## Pseudocode
```
for csvfile in csvfiles
  read csvfile
  keep only the "useful fields"
       if field_name contains 'Percent' or 'PERCENT' or 'POVERTY RATE':
           # its a percentage; convert to decimal value
       if 'Estimate' in field_name:
           # strip out '+' or '-'
       if not a number:
          #replace with null value
# Combine the "useful" fields from your csv files into a single table with 1 row per zip code (or census tract)
```
