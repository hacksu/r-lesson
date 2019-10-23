Taught 10/22.  
Notes if taught again:  
-Downloads and loading a data set took awhile. 
-Challenges were too challenging. 

1. Download R Studio.
https://rstudio.com/products/rstudio/download/
  
  2 What is R?
  Open source language used a lot in stats and for graphing data
Derived from S
Data manipulation language

But what do I use it for? 
  -Stats
-Deep Learning
-connect APIs
-build and host interactive web apps
-big data processing with Apache Spark
-more, more, more

3. Clone this github to get the CSV files.

4. Connect repository to R Studio. File > New Project > Existing Directory


Moving on...
Basic data types in R:
  char, numeric, integer, logical, complex

Smallest data set you can create is a vector.
> c(1,2,3)

In R, you can do math with with vectors without needing a for loop
> 2 * c(1,2,3)


  
  ------------IMPORTING CUSTOM DATASETS & DOING BASIC VISUALIZATIONS---------
  Let’s learn how to import our own dataset and create some basic visualizations with it. Grab “apps.csv” from GitHub.
Import KHE CSV
Go to files tab > apps.csv > import dataset
Make sure the box contains a grid of the data "school", "shirt", "demo", etc.; if not, cancel and click 'import dataset' again
Press import

Dataset should be visible for you to browse. Double-check environment tab on right for variable name. 

Let’s see what our column names are. 
>	colnames(apps)

Ask if this returned column names.

If not, it looks like we are not totally done importing the data. Let’s fix this. 
>	read.csv(“apps.csv”)
Call for the column names again and we’ll be able to see them.
>	colnames(apps)

If you have a long filename, we could store the data source in our own variable. We’re using “<-” which is an assignment operator.
>	t<- read.csv(“apps.csv”)

There is some n/a data entries. We want to clean these out.  
>	apps=na.omit(apps)


Next, let’s get the number of t-shirts by size.
>	table(apps$shirt)

Let’s put this into a bar-chart.  
>	barplot(table(apps$shirt))

But I find blue boring so let’s change into a color. 
>	barplot(table(apps$shirt), col="purple")

I want to find out the age of attendees and this would be best represented by a boxplot.
>	boxplot(apps$age)

CHALLENGE 1: FIGURE OUT HOW TO MAKE IT A BOXPLOT WHERE THE OUTLIERS ARE A TRIANGLE SHAPE AND MAKE THE MIDDLE LINE BLUE
>	boxplot(apps$age, medcol="blue",bg="red",outpch=6)  

Let's make a line chart of when accounts were created:
  plot(table(apps$created), line="l")
  
It should show the dates out of order on the x-axis. We can convert these string values into a date by saving it as a new local global value.

Use this to convert into dates
 >	dates <- as.Date(apps$created, "%m/%d/%Y")

IF THERE’S TIME, FIGURE OUT HOW TO MAKE THESE DATES NEW TO OLD
  
Now call to see the new graph:
>	plot(table(dates), type="l")
  
--------------------------R STUDIO DATA SETS & SOME STATS---------------------------------
Moving on to some other R capabilities...  
Let's say you want to easily import a given data set. R Studio has many data sets sitting in a package that downloads with the software.
>	data()              and press enter

A list of available datasets will show up. Enter the name inside that parenthesis.
Call dataset by given name. Let's use:
>	mtcars

Name Descriptions:
mpg: Miles/(US) gallon
cyl: Number of cylinders
disp: Displacement (cu.in.)
hp: Gross horsepower
drat: Rear axle ratio
wt: Weight (1000 lbs)
qsec: 1/4 mile time
vs: V/S
am: Transmission (0 = automatic, 1 = manual)
gear: Number of forward gears
carb: Number of carburetors
http://www.sthda.com/english/wiki/r-built-in-data-sets

Let’s plot this.
 >	plot(mtcars)

There's a lot of data here. Maybe we're only interested in a few columns. 
>	plot(mtcars[c(1,3,8)])

I’d like to know the average mpg. 
>	mean(mtcars$mpg)

CHALLENGE 2: FIND THE FIVE NUMBER SUMMARY USED IN STATS ON JUST MTCARS MPG
> 	summary(mtcars$mpg)

CHALLENGE 3: CREATE A LINEAR REGRESSION LINE USING MPG AND CYL, THEN PLOT IT. 
Challenge to find linear relationship or something.  
> plot(lm(mtcars$mpg~mtcars$cyl, data=mtcars))

--------------------------------------------HEATMAP----------------------------------------------------------
Next, let’s create a heatmap using gradebook.csv file. Import gradebook dataset. 
Put the dataset in a var. I’m going to also save the dataset into something easier to work with.
>	 grades <- gradebook

Let’s have it print out the student ID instead of the row number, but we’re going to save that in a new var
> 	row.names(grades) <- grades$`Student ID`

CHALLENGE 4: FIGURE OUT HOW TO INPUT THE DATA IN NAMES INTO A MATRIX. 
>	g_matrix <- data.matrix(grades)

Create the heatmap
>	heatmap(g_matrix, Rowv=NA, Colv=NA, col = cm.colors(256), scale="column", margins=c(5,10))


--------------------------------------------------------------------------------------------------------------------
Helpful shortcuts:
clear - ctrl-l or Option + Command + L

Find installed libraries
installed.packages(lib.loc = NULL, priority = NULL,
                   noCache = FALSE, fields = NULL,
                   subarch = .Platform$r_arch,)
