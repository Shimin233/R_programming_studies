## Section 5: Data frames
In real life, data may include more than numerics: characters, logical values, or a mixture of them and numerics. 
Data frames are used for such mixed data, of the form similar to a matrix.

### 5.1 Project brief: Demographic analysis
Q: Work on a project to analyse the World's demographic trends. 
Produce a scatterplot to illustrate Birth Rate and Internet Usage statistics by Country. 
The scatterplot needs to also be categorised by Countries' Income Groups. 

see table here R_programming_studies/sec5-Demographic-Data.csv

### 5.2 Importing data into R

```r
?read.csv()

#method 1: select the file namually
stats <- read.csv(file.choose()) #a window pops out and you can choose csv manually there
stats

#method 2: set WD (working directory) and read data
getwd() #see what is the curretn WD

#set your WD, different ways for Windows/Mac
#Windows
setwd("C:\\Users\\Kirill\Desktop\\R programming") 
#Mac
setwd("/Users/kirilleremenko/Desktop/R programming")

getwd() #indeed WD is changed
rm(stats) #remove stats from environment
stats <- read.csv("sec5-Demographic-Data.csv")
stats #again import this csv, but having directory determined beforehand, so only need filename

```

### 5.3 Exploring your dataset


```r
#use stats imported last time
stats
nrow(stats) 
ncol(stats)
#imported 195 rows; 
# check number of rows/cols to keep track with what we are doing

head(stats) #look at the heading five rows with column names
tail(stats) #look at the bottom six rows
#tell 'head-tail' (like a fox) in R from 'top-(tail?)' in SQL

head(stats, n=10) #heading 10 rows
tail(stats, n=8)
str(stats) #column names and possible values: 
#  num (numerics), Factor w/ k levels (various character words with k possible values, 
#  like country names, 'High income'/'Low income')
#Note tell str() in R, meaning structure, from str() in other languages like Python meaning string
# Similarly, runif() in R means random uniform sampling, but not 'run if'

summary(stats)
#some brief break-down of the table, like min, max, numbr of countries with Low income, etc.

```

### 5.4 Using the $ sign

```r
stats #same as last time
head(stats)
stats[3, 3] #45.984 at 3rd row, 3rd col
stats[3, 'Birth.rate']

#the following is not allowed
stats['Angola', 3] #giving NA; since Angola is just the content of one cell, not name of a row

#data frame, has rows' name being numbers, and only possible to have names for columns (like in Excel)

stats$Internet.users #returns a huge vector
stats$Internet.users[2] #returns the 2nd row of column 'Internet.users', i.e.contents in one cell
stats[, 'Internet.users'] #equivalent expression as stats$Internet.users

levels(stats$Income.Group) #returns four possible values in that column, 
#  which might be omited due to insufficient space in str(stats)

```

### 5.5 Basic operations with a data frame

```r
stats[1:10,] #same as head(stats, n=10), heading 10 rows
stats[3:9,]
stats[c(4, 100),]
#note the name(numbering) of rows are preserved as 4 and 100, not changed to 1, 2

#Remenber how [] works
is.data.frame(stats[1,]) #TRUE
#recall picking one row from a matrix, it auto becomes a vector; data frame is preserved instead

is.data.frame(stats[1,]) #FALSE
is.data.frame(stats[,1,drop=F]) #TRUE, drop=F makes data frame preserved

#multiply and add up columns (even not make sense for some contents)
head(stats)
stats$Birth.rate * stats$Internet.users
stats$Birth.rate + stats$Internet.users

#add a new column
head(stats)
stats$MyCalc <- stats$Birth.rate * stats$Internet.users   
#name new col as if it exits; so it is created

#test of knowledge
stats$xyz <- 1:5 #1:4 not working below as 195, number of total rows is not multiple of 4
head(stats, n=12) #can see a new column like 12345123...5(recycling)

#remove a column
head(stats)
stats$MyCalc <- NULL
stats$xyz <- NULL

```

### 5.6 Filtering a data frame

```r
head(stats)
filter <- stats$Internet.users < 2 #output a vector of TRUE's and FALSE's
stats[filter,] #only outputs rows with TRUE in the vector, filter
stats[stats$Birth.rate > 40,]
stats[stats$Birth.rate > 40 & stats$Internet.users <2,]
stats[stats$Income.Group == 'High income',]
levels(stats$Income.Group)

stats[stats$Country.Name == 'Malta',]

```

### 5.7 Introduction to qplot

```r
?qplot #nothing occurs before importing and activating package ggplot2
install.package('ggplot2')
library(qqplot2)
?qplot #now see its guide

qplot(data=stats, x=Internet.users) #can still type but not require stats$Internet.users since data=stats
qplot(data=stats, x=Income.Group, y=Birth.rate)
qplot(data=stats, x=Income.Group, y=Birth.rate, size=10)# will be same as size=10, with a legend, need below:
qplot(data=stats, x=Income.Group, y=Birth.rate, size=I(10))

qplot(data=stats, x=Income.Group, y=Birth.rate, size=I(3), colour=I('blue')) #similarly for colours, need I()

qplot(data=stats, x=Income.Group, y=Birth.rate, geom='boxplot')

```

### 5.8 Visualising with qplot: Part I

```r
qplot(data=stats, x=Internet.users, y=Birth.rate)
qplot(data=stats, x=Internet.users, y=Birth.rate, size=I(4)) #we want size mapped to each point, so use I()
qplot(data=stats, x=Internet.users, y=Birth.rate, colour=I('red'))
qplot(data=stats, x=Internet.users, y=Birth.rate, colour=Income.group) #get each colour for each Income.Group with a legend
#suitable to develop some insights from this graph: more internet, less birth
```

### 5.9 Building dataframes

```r
#points coloured/categorised by Countries' Regions

#create a new data frame using existing vectors
mydf <- data.frame(Counties_2012_Dataset, Codes_2012_Dataset, 
                   Regions_2012_Dataset) 
#put names of columns of data frame into this function data.frame()
head(mydf)
columns(mydf) <- c('Country', 'Code', 'Region') #rename columns of data frame

rm(mydf)#re-start with the following, which is equvalent to above: 

mydf <- data.frame(Country=Counties_2012_Dataset, Code=Codes_2012_Dataset, 
                   Region=Regions_2012_Dataset)  #do not need quotaion marks
                   #such convenient re-naming also works for cbind() and rbind()
head(mydf)
tail(mydf)
summary(mydf)


```


### 5.10 Merging Data frames

```r
head(stats)
head(mydf)

#combine contents from mydf to stats
#  noting the Country columns match in mydf and stats

merged <- merge(stats, mydf, ny.x='Country.Code', by.y='Code') 
head(merged)
#equating x col from former data frame and y col from latter 
#still have duplications in Country and Country.Name

merged$Country<-NULL
str(merged)
tail(merged)

```

### 5.11 Visualising with qplot: Part II

```r
# library(ggplot2)
qplot(data=merged, x=Internet.users, y=Birth.rate)
qplot(data=merged, x=Internet.users, y=Birth.rate, 
      colour=Region)

#1 Shapes
qplot(data=merged, x=Internet.users, y=Birth.rate, 
      colour=Region, size=I(5), shape=I(17))
      #search for a list of shapes and their numbers, 1-23
      
#2 Transparency
qplot(data=merged, x=Internet.users, y=Birth.rate, 
      colour=Region, size=I(5), shape=I(19), 
      alpha=I(0.6)) #alpha from 0(transparent) to 1 (intransparent)
      #so that can see overlapped shapes
      
#3 Title
qplot(data=merged, x=Internet.users, y=Birth.rate, 
      colour=Region, size=I(5), shape=I(19), 
      alpha=I(0.6), 
      main='Birth rate vs Internet users') 
      

```

### Recap of Section 5
1. Importing data in to R
2. Exploring datasets: `head(), tail(), summary(), str()`(structure)
3. Using the `$` sign for columns with names
4. Basic operations with data frames: setting col names, factors
5. Filtering a data frame: logical opearation to get a logical vector, to be used as a filter
6. Introduction to qplot
7. Visualising with qplot Part I
8. Building data frames: `data.frame()`, combing vectors to a data frame, re-naming columns
9. Merging data frames: `merge()`
10. Visualising with qplot Part II: shape, alpha, main

### Quiz: Data frames

