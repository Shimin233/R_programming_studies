## Section 4: Matrices

### 4.1 Project brief: basketball trends


open and execute all the script of s4-BasketballData.R, and actually 
we can use same environment (i.e variables and data inside it currently) in different scripts.
So create a new R script, and 
try this to see an example of matrix
```r
Salary #can see a matrix of all salaries
```

### 4.2 Matrices

indexation of a matrix
```r
A #a matrix
A[3, 4] #Matrix[row, column]

#row m for a matrix A: A[m,]
#(do not need to put space for column part, same for below)
#column n for a matrix A: A[,n]

#Matrix in R can only contain one type of variables, 
#and turning every element into characters automatially when mixing numerics and characters, 
#just like vector
```

### 4.3 Building your first matrix

```r
#try to see more examples of matrices
Salary
Games
MinutesPlayed

matrix()
rbind() 
cbind()

?matrix #to see guides
my.data <- 1:20
my.data

#matrix(x, nrow=1, ncol=1, byrow=FAULT)
A <- matrix(my.data, nrow=4, ncol=5) #allocate my.data to col 1, col 2...up to down
A
A[2, 3]

B <- matrix(my.data, nrow=4, ncol=5, byrow= T) #same as: byrow=TURE; 
B  #here allocate data to row1, row2, ...left to right
B[2, 5]

#rbind(), combine rows to a matrix
r1 <- c('I', 'am', 'happy')
r2 <- c('What', 'a', 'day')
r3 <- c(1, 2, 3)
C <- rbind(r1, r2, r3)
C  #numerics turned to characters automatically

#cbind(), combine columns to a matrix
c1 <- 1:5
c2 <- -1:-5  # -1, -2, -3, -4, -5 (consequent numbers with ascending absolute values, added with minus sign '-'
D <- cbind(c1, c2)
D

c1 <- c('I', 'am', 'happy')
c2 <- c('What', 'a', 'day')
c3 <- c(1, 2, 3)
E <- cbind(c1, c2, c3)
E  #again, numerics turned to characters automatically

```

### 4.4 Naming dimensions

```r
#the default name of a row is like Matrix[m,]; a row is Matrix[,n]
#now we are going to re-name row or columns (i.e. dimensions) so that can use them like Matrix['RowName',]
#A new name for a dimension can be an arbitrary character or a character version of a number, e.g. '7' (but not 7 numeric itself)
#can mix uses of artificially-assigned name and the default numbering, like Matrix['RowName', 4]
#can equivalently, use either the artifically-assigned name or the default numbering, 
#e.g.  M['d'] equivalent to M[4] when columns of M turned to 'a', 'b', 'c', 'd'

#Treat a m-element vector as a 1*m matrix, same rules as above appply
```
### 4.5 Colnames() and Rownames()

```r
#named vectors
Charlie <- 1:5
Charlie

#give names
names(Charlie) #this returns NULL
names(Charlie) <- c('a', 'b', 'c', 'd', 'e')
Charlie #names with corresponding elements 1, ...5
Charlie['d'] #d with 4
names(Charlie) #now it is 'a', 'b', 'c', 'd', 'e'

#clear names
names(Charlie) <- NUL
Chaelie #back to original vector without artificial name

#naming matrix dimension 1
temp.vec <- 
  rep(c('a', 'B', 'zZ'), times=3)
 
temp.vec <- 
  rep(c('a', 'B', 'zZ'), each=3)
temp.vec

Bravo <- matrix(temp.vec, 3, 3)
Bravo
#currently Bravo is a non-named matrix

rownames(Bravo) <- c('How', 'are', 'you?')
Bravo

colnames(Bravo) <- c('X', 'Y', 'Z')
Bravo

Bravo[2, 2]
Bravo['are', 'Y'] 
Bravo['are', 'Y'] <- 0

rownames(Bravo)

rownames(Bravo) <- NULL
Bravo

```

### 4.6 Matrix operations
```r
Games #from BasketballData.R
rownames(Games)
colnames(Games)
Games['LeBronJames', '2012']

FieldGoals

round(FieldGoals / Games, 1)  #entry-by-entry arithmetics

round(MinutesPlayed / Games)

```

### 4.7 Visualising with Matplot()

```r
#matplot(x, y, type='pl')
# where x, y are vectors of matrices of data; or by default 1:n, y
# type = a character or vector of characters for the type of each column of y, 'pl': points and lines
# lty = vector of line types; lwd = vector of line widths; lend = vector of line styles 
# pch = a character or vector of characters for plotting character
# ...see others in ?matplot()

FieldGoals #we want to plot each row rather than column
t(FieldGoals) #thus transpose this matrix

matplot(t(FieldGoals))

matplot(t(FieldGoals), type='b', pch=15:18, col=c(1:4, 6))
legend('bottomleft', inset=0.01, legend=Players, col=c(1:4, 6), pch=15:18, horiz=F) 
#inset = how far from coner of chart; horiz= F means vertical legend
#this 'legend' is to add a box at bottom left for explanations (a legend) of symbols and colours

#matplot: as we set here, same colours 'col' and symbols 'pch', which is inconvenient if we want to have colours matched; 
#more powerful tool for colour and symbol matching later

#particularly for this FieldGoals example, it does not show other information like injury

#another way to analyse
matplot(t(FieldGoals/Games), type='b', pch=15:18, col=c(1:4, 6))
legend('bottomleft', inset=0.01, legend=Players, col=c(1:4, 6), pch=15:18, horiz=F) 

#a third way to analyse
matplot(t(FieldGoals/FieldGoalAttempts), type='b', pch=15:18, col=c(1:4, 6))
legend('bottomleft', inset=0.01, legend=Players, col=c(1:4, 6), pch=15:18, horiz=F) 
#can see Dwight Howard has the best accuracy

```

### 4.8 Subsetting

```r
x <- c('a', 'b', 'c', 'd', 'e')
x
x[c(1, 5)] #'a', 'e'
x[1] #'a', which is also a (one-element) vector
# actually we are subsetting the vector x to a vector

#Subset a matrix then USUALLY (but not always) get a matrix
Games
Games[1:3,6:10]
Games[c(1, 10),]
Games[, c('2008', '2009')] #can also use names to pick dimensions

Games[1,]
is.matrix(Games[1,])#FALSE
is.vector(Games[1,])#TRUE, suprising! Actually a named vector

Games[1, 5] 
is.matrix(Games[1, 5]) #FALSE
is.vector(Games[1, 5]) #TRUE , again one entry of a matrix is also a (one-element) vector

#R is guessing what we want; here picking one dimension from a matrix -> it guesses we want a vector!
#to still get a matrix, use the argument 'drop', 
# which by default drop=TRUE, dropping unnecessary dimensions, as above Games[1,] did
Games[1,drop=F] #this is instead a named 1*N matrix
Games[1, 5, drop=F] #this is a named 1*1 matrix

```


### 4.9 Visualising subsets

```r
Data <- MinutesPlayed[1:3,]
Data
matplot(t(Data), type='b', pch=15:18, col=c(1:4, 6))
legend('bottomleft', inset=0.01, legend=Players[1:3], col=c(1:4, 6), pch=15:18, horiz=F) 

#intuitively but wrong way to pick only one player: 
Data <- MinutesPlayed[1,] #not a matrix (as required by matplot later, but a vector)
Data
matplot(t(Data), type='b', pch=15:18, col=c(1:4, 6))
legend('bottomleft', inset=0.01, legend=Players[1], col=c(1:4, 6), pch=15:18, horiz=F) 
#legend uses a vector, so it is ok

#correct way:
Data <- MinutesPlayed[1,drop=F] # a matrix
Data
matplot(t(Data), type='b', pch=15:18, col=c(1:4, 6))
legend('bottomleft', inset=0.01, legend=Players[1], col=c(1:4, 6), pch=15:18, horiz=F) 
```
### 4.10 Creating your first function


```r
#Recall from last time (player chosen is changed) the following; 
Data <- MinutesPlayed[2:3,drop=F] # a matrix
matplot(t(Data), type='b', pch=15:18, col=c(1:4, 6))
legend('bottomleft', inset=0.01, legend=Players[2:3], col=c(1:4, 6), pch=15:18, horiz=F) 

#We are going to create a function to output the same result 
myplot <- function(){
    Data <- MinutesPlayed[2:3,drop=F] # a matrix
    matplot(t(Data), type='b', pch=15:18, col=c(1:4, 6))
    legend('bottomleft', inset=0.01, legend=Players[2:3], col=c(1:4, 6), pch=15:18, horiz=F) 
}

myplot() 


#can set parameters of a function
myplot <- function(rows){
    Data <- MinutesPlayed[rows,drop=F] # a matrix
    matplot(t(Data), type='b', pch=15:18, col=c(1:4, 6))
    legend('bottomleft', inset=0.01, legend=Players[rows], col=c(1:4, 6), pch=15:18, horiz=F) 
}

myplot(1:5)  
#(to be confirmed) due to the variable type requirements of definition of myplot(), 
# myplot(rows) automatically requires rows being a matrix

#add another parameter
myplot <- function(data, rows){
    Data <- data[rows,drop=F] # a matrix
    matplot(t(Data), type='b', pch=15:18, col=c(1:4, 6))
    legend('bottomleft', inset=0.01, legend=Players[rows], col=c(1:4, 6), pch=15:18, horiz=F) 
}

myplot(Salary,  1:5)  

#can set default value for our parameter(s)
myplot <- function(data, rows=1:10){
    Data <- data[rows,drop=F] # a matrix
    matplot(t(Data), type='b', pch=15:18, col=c(1:4, 6))
    legend('bottomleft', inset=0.01, legend=Players[rows], col=c(1:4, 6), pch=15:18, horiz=F) 
}

myplot(Salary)   #taking default value rows=1:10
myplot(MinutesPlayed/Games) #inputting a resulting matrix of arithmetics also works
myplot(MinutesPlayed/Games, 3)

```

### 4.11 Basketball insights

```r
myplot <- function(data, rows=1:10){
    Data <- data[rows,drop=F] # a matrix
    matplot(t(Data), type='b', pch=15:18, col=c(1:4, 6))
    legend('bottomleft', inset=0.01, legend=Players[rows], col=c(1:4, 6), pch=15:18, horiz=F) 
}

myplot(Games)

#analyse data from various perspectives, to see effects of, (e.g.)injury on salaries, FieldGoals, etc
```


### 4.12 Recap of Section 4
1. Project brief: basketball trends
2. Matrices
3. Building your first matrix
4. Naming dimensions
5. Colnames() and Rownames()
6. Matrix operations
7. Visualising with Matplot()
8. Subsetting
9. Visualising subsets
10. Creating your first function
11. Basketball insights


### Homework: Basketball free throws

### Quiz
