## Section 6: GGPlot2

### 6.1 Project brief: Movie ratings

### 6.2 Grammar of graphics - GGPlot2

```r
## e.g: a single graph showig six types of data 
##  by splitting them into different layers

# Seven Layers of information in a chart, are: (from abstract to basic)
# Theme
# Coordinates
# Facets
# Statistics
# Geometrics
# Aesthetics
# Data

#e.g. Movie budget distribution, it has
# data: movie name, budget, and genre
# aesthetics: budget as s-axis, genre making the fill (colour)
# geometrics: bar chart i.e. histogram
# statistics: combined with geometrics, histogram showing number of movies
# facets: histograms in different years
# coordinates: number of movies as y axis, budget as x axis
# theme: 'Movie Budget Distribution', Genre, #movies v.s. budgets

```

### 6.3 What is a factor

```r
# We talk about the layer of Data today
 
setwd()
getwd()
 
movies <- read.csv('sec6-Movie-Ratings.csv')
head(movies)
colnames(movies) <- C('Film', 'Genre', 'CriticRating', 'AudienceRating', 'BudgetMillions', 'Year')

head(movies)
tail(movies)
str(movies) #R conunts all the possible character values (factors), and number them in structure of data frame
summary(movies)

#now we want years to be factors rather than numbers
factor(movies$Year)
movies$Year <- factor(movies$Year)

summary(movies) #can see Year becomes factors

```

### 6.4 Aesthetics
```r
#Aesthetics: how data are mapped to graph

library(ggplot2) #previously we used qplot(), for 'quick plot'

ggplot(data=movies, aes(x=Critical Rating, y=AudienceRating))
#output is an empty plot, only has x and y-axis names

#add geometry
ggplot(data=movies, aes(x=Critical Rating, y=AudienceRating))+
  geom_point()
  #output is scatterpoint
  
#add colour  
ggplot(data=movies, aes(x=Critical Rating, y=AudienceRating, 
                        colour=Genre))+
  geom_point()
  
#add size 
ggplot(data=movies, aes(x=Critical Rating, y=AudienceRating, 
                        colour=Genre, size=Genre))+
  geom_point()

#add size - better way
ggplot(data=movies, aes(x=Critical Rating, y=AudienceRating, 
                        colour=Genre, size=BudgetMillions))+
  geom_point()
  
#>>> This is #1 (will improve it)
  
```

### 6.5 Plotting with layers
```r
#Geometries

p <- ggplot(data=movies, aes(x=Critical Rating, y=AudienceRating, 
                        colour=Genre, size=BudgetMillions))
#create a variable p, which is a list of 9
p #output is an empty plot, as geometry is not set yet

#Geometries can be set as:
#point
p + geom_point()

#lines
p + geom_line() #can seelines are not suitable here

#multiple layers
p + geom_line()+ geom_point() 
#first plot line and plot point above them

```

### 6.6 Overriding aesthetics
```r
#Back to Aesthetics 

q <- ggplot(data=movies, aes(x=CriticRating, y=AudienceRating,
            colour=Genre, size=BudgetMillions))

#add geom layer
q + geom_point()

#overriding aes
#eg1
q + geom_point(aes(size=CriticRating))
#eg2
q + geom_point(aes(colour=BudgetMillions))
#q itself remains the same
q + geom_point() 

#eg3
q + geom_point(aes(x=BudgetMillions))
#but the x-axis name remains to be Critic Rating, improve like this: 
q + geom_point(aes(x=BudgetMillions)) + 
    xlab('Budget Millions $$$')
 #>>> 2nd chart
    
#eg4
q + geom_line() + geom_point()
#reduce line sizes
q + geom_line(size=1) + geom_point()
#Remark, can see mapping(size=CriticalRating) v.s. setting (size=1) in the definition of sizes

```

### 6.7 Mapping vs Setting

```r
#Aesthetics again

#>>> 2nd chart
q + geom_point(aes(x=BudgetMillions)) + 
    xlab('Budget Millions $$$')
 #can save plot and insert it into slides, etc.
 
r <- ggplot(data=movies, aes(x=Critical Rating, y=AudienceRating))
r + geom_point()

#add colour
#1. Mapping (what we've done so far)
r + geom_point(aes(colour=Genre))
#2. Setting
r + geom_point(colour='DarkGreen') #not using aes(); outputs no legend
#Error: 
# r + geom_point(aes(colour='DarkGreen'))

#a. Mapping
r + geom_point(aes(size=BudgetMillions))
#2. Setting
r + geom_point(size=10) #no legend
#Error:
#  r + geom(aes(size=18)) #has a legend; much smaller than true size 10, as 10 is recognised as a category; 
# and R just assign one certain size (like 3 or 4) to all the points of this '10' category

```

### 6.8 Histograms and Density charts
```r
# Statistics (and Geometries)

s <- ggplot(data=movies, aes(x=BudgetMillions))#do not need y
s + geom_histogram(binwidth=10)
#outputs a histogram

#add colour
s + geom_histogram(binwidth=10, fill='Green')
s + geom_histogram(binwidth=10, aes(fill=Genre))
#add a bordeer
s + geom_histogram(binwidth=10, aes(fill=Genre), colour='Black')
#>>> 3rd chart (will improve it)

#sometimes you may need density charts:
s + geom_density(aes(fill=Genre))
s + geom_density(aes(fill=Genre), position='stack')

```

### 6.9 Starting Layer Tips
```r
#back to Aesthetics

t <- ggplot(data=movies, aes(x=AudienceRating))
t + geom_histogram(binwidth=10,
                    fill='White', colour='Blue')
                  
#another way to get the same plot:
t <- ggplot(data=movies)
t + geom_histogram(binwidth=10,
                    aes(x=AudienceRating), 
                    fill='White', colour='Blue')
#>>> 4th chart

#advantage of such ggplot() is that, when we have no certain aim,
# we can explore a data set and add elements using ggplot like above

#e.g. update as below
t + geom_histogram(binwidth=10,
                    aes(x=CriticRating), 
                    fill='White', colour='Blue')
#>>> 5th chart
#can see critic ratings are more uniform than audience ratings, maybe because
# critics consider more factors when making a rate

#can even plot empty
t<- ggplot()
```
### 6.10 Statistical transformations
```r
#Statistics

?geom_smooth

u <- ggplot(data=movies, aes(x=CriticRating, y=AudienceRating,
             colour=Genre))
u + geom_point()
u + geom_point() + geom_smooth()
u + geom_point() + geom_smooth(fill=NA) #i.e. removing any fill

#boxplots
u <- ggplot(data=movies, aes(x=Genre, y=AudienceRating,
                              colour=Genre))
u + geom_boxplot()
u + geom_boxplot(size=1.2)
u + geom_boxplot(size=1.2) + geom_point()
#tip/hack:
u + geom_boxplot(size=1.2) + geom_jitter()
  #jitter generates random positions of points each time; but it helps to see distributions

#another way:
u + geom_jitter() +geom_boxplot(size=1.2, alpha=0.5)
   #can see distributions of points and half-transparent boxplots
#>>> 6th chart

#try this and plot boxplots for it: 
v <- ggplot(data=movies, aes(x=Genre, y=AudienceRating,
                              colour=Genre))

```
### 6.11 Using facets
```r
#Facets

v <- gplot(data=movies, aes(x=BudgetMillions))
v + geom_histogram(binwidth=10, aes(fill=Genre), 
                    colour='Black')
#facets
v + geom_histogram(binwidth=10, aes(fill=Genre), 
                    colour='Black')+
  facet_grid(Genre~.)

v + geom_histogram(binwidth=10, aes(fill=Genre), 
                    colour='Black')+
  facet_grid(Genre~., scales='free') #allows different scales for different genres/facets
  
#scatterplots:
w <- ggplot(data=movies, aes(x=CriticalRating, y=AudienceRating,
                              colour=Genre))
w + geom_point(size=3)

#facets
w + geom_point(size=3) +
  facet_grid(Genre~.) #split into horizontal pieces, each for one genre
  
w + geom_point(size=3) +
  facet_grid(.~Year)  #split into vertical pieces, each for one year

w + geom_point(size=3) +
  facet_grid(Genre~Year) #split by genres and years
  
w + geom_point(size=3) +
  geom_smooth()+
  facet_grid(Genre~Year)  
  #smoothen into lines then split by genres and years
  
w + geom_point(aes(size=BudgetMillions)) +
  geom_smooth()+
  facet_grid(Genre~Year)  
#>>> 1st chart (still to be improved)

```
### 6.12 Coordinates
```r
# Coordinates
#Today: limits; zoom

m <- ggplot(data=movies, aes(x=CriticRating, y=AudienceRating,
                              size=BudgetMillions,
                              colour=Genre))
m + geom_point()

m + geom_point() +
  xlim(50, 100) #but this forces to remove some points

m + geom_point() +
  xlim(50, 100) +
  ylim(50, 100)
  
#won't work well always
n <- ggplot(data=movies, aes(x=BudgetMillions))
n + geom_histogram(binwidth=10, aes(fill=Genre), colour='Black')
 
n + geom_histogram(binwidth=10, aes(fill=Genre), colour='Black') +
  ylim(0, 50) #some points cut out; but we want to zoom in instead!

#instead - zoom:
n + geom_histogram(binwidth=10, aes(fill=Genre), colour='Black') +
  coord_cartesian(ylim=c(0, 50)) 
  #points over 50 is not cut just our of vision of this chart, i.e. zoom in!

#improve 1st chart from last lecture: 
w <- ggplot(data=movies, aes(x=CriticalRating, y=AudienceRating,
                              colour=Genre))
w + geom_point(aes(size=BudgetMillions)) +
  geom_smooth()+
  facet_grid(Genre~Year)  
#improve: 
w + geom_point(aes(size=BudgetMillions)) +
  geom_smooth()+
  facet_grid(Genre~Year) + 
  coord_cartesion(ylim=c(0, 100)) 
  #some shade(confidence band) are out of vision, zoom more in points and lines

```
### 6.13 Perfecting by adding themes
```r
# Theme

#will improve 3rd chart
o <- ggplot(data=movies, aes(x=BudgetMillions)) 
h <- o + geom_histogram(binwidth=10, aes(fill=Genre), colour='Black')
h
#axis labels
h + xlab('Money Axis') +
  ylab('Number of Movies') 
  theme(axis.title.x= element_text(colour='DarkGreen', size=30), 
        axis.title.y= element_text(colour='Red', size=30))

#tick mark formatting
h + xlab('Money Axis') +
  ylab('Number of Movies') +
  theme(axis.title.x= element_text(colour='DarkGreen', size=30), 
        axis.title.y= element_text(colour='Red', size=30),
        axis.text.x=element_text(size=20),
        axis.text.y=element_text(size=20))
 
?theme

#legend formatting
h + xlab('Money Axis') +
  ylab('Number of Movies') +
  theme(axis.title.x= element_text(colour='DarkGreen', size=30), 
        axis.title.y= element_text(colour='Red', size=30),
        axis.text.x=element_text(size=20),
        axis.text.y=element_text(size=20),
        
        legend.title=element_text(size=30),
        legend.text=element_text(size=20),
        legend.position= c(1, 1),
        legend.justification = c(1, 1)) 
        #c(1, 1) means top right corner; justification further moves legend into the chart

#title 
h + xlab('Money Axis') +
  ylab('Number of Movies') +
  ggtitle('Movie Budget Distribution') +
  theme(axis.title.x= element_text(colour='DarkGreen', size=30), 
        axis.title.y= element_text(colour='Red', size=30),
        axis.text.x=element_text(size=20),
        axis.text.y=element_text(size=20),
        
        legend.title=element_text(size=30),
        legend.text=element_text(size=20),
        legend.position= c(1, 1),
        legend.justification = c(1, 1)
        
        plot.title = element_text(colour='DarkBlue',
                                  size=40,
                                  family='Courier')
        )
        #family for title sets the font
#>>> our final 3rd chart

```
### Recap of Section 6
1. Grammar of Graphics & GGPlot2: 7 layers, data, aesthetics, geometries, statistcs, facets, coordinates, theme
2. Factors in R: convert into factors `factor()`
3. Aesthetics & `ggplot()`
4. Plotting with layers: (bottom <-)first layer + second layer +... (-> top)
5. Overriding Aesthetics: override in later layers, like in `geom_point()`
6. Mapping vs Setting: `aes(colour=Genre)` versus `colour='Black'`
7. Histograms and Density charts: `geom_histogram()` using only one axis, with `fill`; `geom_density()`
8. Starting layer tips: order layers as you need
9. Statistical transformation: `boxplot()` with scatter points
10. Using facets
11. Coordinates: `xlim`, `ylim`
12. Themes

### Homework: Movie Domestic % Gross

### Quiz
1. Which of the following is NOT one of the seven layers we talked about in Grammar of Graphics?\
  Colours is not.\
  
2. What is wrong in the following code?\
`r <- ggplot(data=movies,  aes(x=CriticRating, y=AudienceRating, colour="Purple"))`\
The colour aesthetic is obviously being set(!) to the colour 'Purple' not mapped to it. 
Therefore, the setting should occur outside of the `aes()` function.\

3. How do you control which layers come closer to the top of your plot and which - closer to the bottom in GGPlot2?\
You control this by rearranging the order in which you add the layers to your plot in your code.\

4. How many variables (columns of a data frame) are required to create a histogram?\
1 (only x=Col)

5. Your dataset has 3 different values in the "Country" column
 and 10 different values in the "Occupation" column. 
P is a plot that uses this dataset and does not yet have a facets layer. 
What kind of facet grid will be created by the following code?\
`P + facet_grid(Country~Occupation)`\
A grid of 3 rows x 10 columns
