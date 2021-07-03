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

### 4.8 Subsetting

### 4.9 Visualising subsets

### 4.10 Creating your first function

### 4.11 Basketball insights

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
