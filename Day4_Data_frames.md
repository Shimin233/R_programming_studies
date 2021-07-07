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

levels(stats$Incom.Group) #returns four possible values in that column, 
#  which might be omited due to insufficient space in str(stats)

```

### 5.5 Basic operations with a data frame

```r


```

### 5.6 Filtering a data frame

### 5.7 Introduction to qplot

### 5.8 Visualising with qplot: Part I

### 5.9 Building dataframes

### 5.10 Merging Data frames

### 5.11 Visualising with qplot: Part II

### Recap of Section 5

### Quiz: Data frames

