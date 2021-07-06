## Section 5: Data frames

### 5.1 Project brief: Demographic analysis

table

### 5.2 Importing data into R

```r
?read.csv()

#method 1: select the file namually
stats <- read.csv(file.choose())
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

stats <- read.csv("DemographicData.csv")
stats

```

### 5.3 Exploring your dataset


```r

```

### 5.4 Using the $ sign

### 5.5 Basic operations with a data frame

### 5.6 Filtering a data frame

### 5.7 Introduction to qplot

### 5.8 Visualising with qplot: Part I

### 5.9 Building dataframes

### 5.10 Merging Data frames

### 5.11 Visualising with qplot: Part II

### Recap of Section 5

### Quiz: Data frames

