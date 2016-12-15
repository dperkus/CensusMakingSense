# Acquiring the data
##Census web site "American Factfinder"
* http://factfinder.census.gov/faces/nav/jsf/pages/index.xhtml

## How to download census tables in csv format:

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
* click "next"S1501, DP02, DP03, DP04, DP05
* select the tables that you want to download.  S1501 will be on the 1st or 2nd page.  The DP tables will be on the last page 
* click "next"
* click "OK"
* it may take several minutes for your download files to be assembled
* click download
* unzip

# Prepping the data
## Which columns to use?  
It depends . . .

Here is the list of columns that I used for my project 
https://github.com/dperkus/CensusMakingSense/blob/master/census_import_metadata.csv

## Pseudocode
for csvfile in csvfiles
  read csvfile
  keep only the "useful fields"
       if 'Percent' in field_name or \
          'PERCENT' in field_name or \
          'POVERTY RATE' in field_name:
           # its a percentage; convert to decimal value
       else :
           if 'Estimate' in field_name:
                                    if '+' in val or '-' in val :
                                        warn = 'WARNING: TRUNCATING + or - ', \
                                            fid, field_name, val
                                        warnings[warn] +=1
                                        val = val.rstrip('+-').replace(',','')
                                    if '.' in val :
                                        v = round(float(val), 2)    
                                    else :
                                        # it should be an integer
                                        v = int(val)
            else :
                 v = val
                        except :
                            # not a number
                            warn = 'WARNING: EXPECTED A NUMBER; REPLACED BY \'\'', \
                                   fid, field_name, val
                            warnings[warn] +=1
                            v = ''
                        ret_row.append(v)
