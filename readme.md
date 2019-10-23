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

=================================================================

_Moving on..._

_Basic data types in R:_

_char, numeric, integer, logical, complex_

_Smallest data set you can create is a vector._

_  \&gt; c(1,2,3)_

_In R, you can do math with with vectors without needing a for loop_

_  \&gt; 2 \* c(1,2,3)_

_ _

_  2, 4, 6_

_ _

_Or we could do this via a pointer._

_y \&lt;- 1:5_

_y_

_======================================================================_





------------IMPORTING CUSTOM DATASETS &amp; DOING BASIC VISUALIZATIONS---------

Let&#39;s learn how to import our own dataset and create some basic visualizations with it. Grab &quot;apps.csv&quot; from GitHub.

Import KHE CSV

- Go to files tab \&gt; apps.csv \&gt; import dataset
- Make sure the box contains a grid of the data &quot;school&quot;, &quot;shirt&quot;, &quot;demo&quot;, etc.; if not, cancel and click &#39;import dataset&#39; again
-  Press import

Dataset should be visible for you to browse. Double-check environment tab on right for variable name.

Let&#39;s see what our column names are.

\&gt;        colnames(apps)

Ask if this returned column names.

If not, it looks like we are not totally done importing the data. Let&#39;s fix this.

\&gt;        read.csv(&quot;apps.csv&quot;)

Call for the column names again and we&#39;ll be able to see them.

\&gt;        colnames(apps)

If you have a long filename, we could store the data source in our own variable. We&#39;re using &quot;\&lt;-&quot; which is an assignment operator.

\&gt;        t\&lt;- read.csv(&quot;apps.csv&quot;)

There is some n/a data entries. We want to clean these out.

\&gt;        apps=na.omit(apps)



Next, let&#39;s get the number of t-shirts by size.

\&gt;        table(apps$shirt)

 Let&#39;s put this into a bar-chart.

\&gt;        barplot(table(apps$shirt))

But I find blue boring so let&#39;s change into a color.

\&gt;        barplot(table(apps$shirt), col=&quot;purple&quot;)

I want to find out the age of attendees and this would be best represented by a boxplot.

\&gt;        boxplot(apps$age)

**CHALLENGE 1: FIGURE OUT HOW TO MAKE IT A BOXPLOT WHERE THE OUTLIERS ARE A TRIANGLE SHAPE AND MAKE THE MIDDLE LINE BLUE**

\&gt;        boxplot(apps$age, medcol=&quot;blue&quot;,bg=&quot;red&quot;,outpch=6)

Let&#39;s make a line chart of when accounts were created:

  plot(table(apps$created), line=&quot;l&quot;)

It should show the dates out of order on the x-axis. We can convert these string values into a date by saving it as a new local global value.

Use this to convert into dates

 \&gt;        dates \&lt;- as.Date(apps$created, &quot;%m/%d/%Y&quot;)

_IF THERE&#39;S TIME, FIGURE OUT HOW TO MAKE THESE DATES NEW TO OLD_

Now call to see the new graph:

\&gt;        plot(table(dates), type=&quot;l&quot;)

--------------------------R STUDIO DATA SETS &amp; SOME STATS---------------------------------

Moving on to some other R capabilities...

Let&#39;s say you want to easily import a given data set. R Studio has many data sets sitting in a package that downloads with the software.

\&gt;        data()              and press enter

A list of available datasets will show up. Enter the name inside that parenthesis.

Call dataset by given name. Let&#39;s use:

\&gt;        mtcars

Name Descriptions:

1. mpg: Miles/(US) gallon
2. cyl: Number of cylinders
3. disp: Displacement (cu.in.)
4. hp: Gross horsepower
5. drat: Rear axle ratio
6. wt: Weight (1000 lbs)
7. qsec: 1/4 mile time
8. vs: V/S
9. am: Transmission (0 = automatic, 1 = manual)
10. gear: Number of forward gears
11. carb: Number of carburetors

[http://www.sthda.com/english/wiki/r-built-in-data-sets](http://www.sthda.com/english/wiki/r-built-in-data-sets)

Let&#39;s plot this.

 \&gt;        plot(mtcars)

There&#39;s a lot of data here. Maybe we&#39;re only interested in a few columns.

\&gt;        plot(mtcars[c(1,3,8)])

I&#39;d like to know the average mpg.

\&gt;        mean(mtcars$mpg)

**CHALLENGE 2: FIND THE FIVE NUMBER SUMMARY USED IN STATS ON JUST MTCARS MPG**

\&gt;         summary(mtcars$mpg)

**CHALLENGE 3: CREATE A LINEAR REGRESSION LINE USING MPG AND CY, THEN PLOT IT.**

Challenge to find linear relationship or something.

\&gt; plot(lm(mtcars$mpg~mtcars$vs, data=mtcars))

--------------------------------------------HEATMAP----------------------------------------------------------

Next, let&#39;s create a heatmap using gradebook.csv file.

Put the dataset in a var. I&#39;m going to also save the dataset into something easier to work with.

\&gt;        grades \&lt;- gradebook.csv

Let&#39;s have it print out the student ID instead of the row number, but we&#39;re going to save that in a new var

\&gt;         row.names(grades) \&lt;- grades$`Student ID`

**CHALLENGE 4: FIGURE OUT HOW TO INPUT THE DATA IN NAMES INTO A MATRIX.**

\&gt;        g\_matrix \&lt;- data.matrix(grades)

Create the heatmap

\&gt;        heatmap(g\_matrix, Rowv=NA, Colv=NA, col = cm.colors(256), scale=&quot;column&quot;, margins=c(5,10))

**CHALLENGE 5: FIGURE OUT HOW TO GET VARIABLES ON X AXIS TO BE HORIZONTAL**

\&gt;        heatmap(g\_matrix, Rowv=NA, Colv=NA, col = cm.colors(256), scale=&quot;column&quot;, margins=c(5,10), srtCol=35)

Make a key for the heatmap.

\&gt;        heatmap.2(g\_matrix, Rowv=NA, Colv=NA, col = cm.colors(256), scale=&quot;column&quot;, margins=c(5,10))



--------------------------------------------------------------------------------------------------------------------

Helpful shortcuts:

clear - ctrl-l or Option + Command + L

Find installed libraries

installed.packages(lib.loc = NULL, priority = NULL,

                   noCache = FALSE, fields = NULL,

                   subarch = .Platform$r\_arch,)
