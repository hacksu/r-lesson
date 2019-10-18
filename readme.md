
1. Download R Studio.
  https://rstudio.com/products/rstudio/download/
  
2 What is R?
    Open source language used a lot in stats and for graphing data
    Derived from S
    Data manipulation language
    
Smallest data set you can create is an vector.
  > c(1,2,3)

In R, you can do math with with vectors without needing a for loop
  > 2 * c(1,2,3)
  
  2, 4, 6
  
Import KHE CSV
  Go to files tab > apps.csv > import dataset
  Make sure the box contains a grid of the data "school", "shirt", "demo", etc.; if not, cancel and click     'import dataset'again
  Press import
TO DO CHANGE CSV TO APP.CSV
  
Dataset should visible for you to browse. Double-check environment tab on right for variable name. 
  
There is some n/a data entries. We want to clean these out.  
Call
  apps=na.omit(apps)
  
Call 
  table(apps$shirt)
  
Call  
  barplot(table(apps$shirt))

Call  
  boxplot(apps$age)  
  
Let's look call 
  plot(table(apps$created), line"l")
  
It should show the dates out of order on the x-asix. We can convert these string values into a date, save it a new local global value. 

Use this to convert into dates
  dates <- as.Date(apps$created, "%m/%d/%Y")
  
Now call to see the new graph:
  plot(table(dates), type="l")