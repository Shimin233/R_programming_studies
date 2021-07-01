## Section 3: Fundamentals of R

Tip: Double quotation marks and single quotations marks can both represent a character in R, like both of them working for strings in Python.

### 3.1 Vector
A vector (in R) is an ordered collection of items, where items can be numerics or characters.
Particularly in R, 
its indices are 1, 2, 3, ...

(Note the indices of a vextor in many of other languages start with zero: 0, 1, 2, ...; e.g. Python)

```r
c(2, 3, 7) #a numeric vector
c('A', '2', '3', '7', 'seven', 'Ab') #a character vector
4 #note even one single number, is a one-element vector in R

```

Remark that a vector in R can only contain __one type__ of variables. 
If inputting numeric(s) with characters to build a vector, R will automatically turn the numeric(s) to character(s) by 
enclosing it (them) by "".
```r
v <- c('A', 2, 7, 'seven', 'Ab') #note input has 7 being numeric, while the others characters
v #automaticallt turns to c('A', '2', '7', 'seven', 'Ab')
typeof(v) #output is "character": v is a vector of characters
```
### 3.2 Create some vectors
Three functions are usually used to create vectors in R: `c()`, `seq()` and `rep()`. We can also check the variable types of vectors.
```r
v1 <- c(3, 45, 56, 732)
v1
is.numeric(v1) #TRUE; indeed it is a vector of numerics
is.integer(v1) #FALSE; since below:
is.double(v1) #TRUE; R automatically treats inputted numerics as doubles even they do not always have decimal places

v2 <- c(3L, 45L, 56L, 732L) #can specify integers when inputting, to create a vector of integers
v2
is.double(v2) #FALSE, note now it is NOT double when it is an integer-vector
is.integer(v2) #TRUE

typeof(v2) #can also check type like this;this outputs "double"
typeof(v2) # this outputs "integer"
```
```r
seq(from, to, by)
#by dafault, from=1, to=1 (the ending point; included in resulting vector, except when not reachable due to step length), by=1 (step-length)

#compare seq(1, 5) with 1:5, the latter one only outputs vector from 1 to 5 with step 1; but seq() can have different step-lengths

seq(5) #1, 2, 3, 4, 5; same as seq(1, 5) ; actually even seq(1:5) results the same thing, though not recommended to code so
seq(2, 15, 2) #2, 4, 6, 8, 10, 12, 14; 15 is not included because of the step being 2
```
Note that in Python, a code similar to `seq()` is `range(start, stop, step)`, where by default start=0, stop=ending (not included), step=1; 
e.g. range(5) means 0, 1, 2, 3, 4 with indices 0, 1, 2, 3, 4

```r
rep(item, n)
#replicate an item (numeric/character/vector) by n times

v <- c('A', '2', '7', 'seven', 'Ab')
rep(v, 3)
```
Note that there are other functions creating vectors as we have seen so far, like: 
```r
m <- rnorm(n, mean, sd) #creates a n-element vector by sampling from Normal(mean, sd^2)
```
### 3.3 Using the \[\] brackets

The brackets `[]` brings a vector to indices

```r
#Recap the functions from last time
x <- c(1, 123, 534, 13, 4) #combine
y <- seq(201, 250, 11) #sequence
z <- rep('Hi!', 3) #replicate

w <- c('a', 'b', 'c', 'd', 'e')
w

w[1]
w[2]

w[-1] #"b" "c" "d" "e"

#basically the above vector[SingleNumeric] can be generalised to vector[vector] as below
w[1:3] #"a" "b" "c"
w[4:5] #"d" "e"
w[c(1, 3, 5)] # "a" "c" "e"
w[c(-1, -3)] #"b" "d" "e"
w[-3:-5] #"a" "b", that is removing 3, 4, 5-th entries; 
#note that minus sign '-' just means 'removing', the '-a:-b' still refers to the indices 'a, ...(ascending), b'
w[-4:-19] # "a" "b" "c"; the out-of-range indices do not cause Error, they just cannot remove anything from the vector w

#for any of the above, can also assign the resulting vector to a variable
v <- w[1:3]
v #"a" "b" "c"


```
Note that in Python, a similar code is `range(start, stop, step)[index]`, used to pick elements from a vector.

Q: if inputting an unavailable index in \[\], does R give an 'IndexError' or similar? Not always cause an Error.
```r
w[0] #character(0); not sure what it means
w[19] #NA; this is kind of R-version "IndexError" 
w[-4:-19] # "a" "b" "c"; the out-of-range indices do not cause Error, they just cannot remove anything from the vector w
w[-34] #"a" "b" "c" "d" "e"; this does not give any Error, index 34 just can remove nothing form the vector
```
Next time, 
Vectorised operations

### 3.4 Vectorised operations
Vector arithmetics = entry by entry arithmetics, and the output is a vector. Arithmetics including =, -, *, `/`

(and `//`, `%`?) 

Arithmetics between a longer vector and a shorter: 
Recycling of vectors 
in the shorter vector, 
when the longer vector's length is multiple of shorter. 
However, if not multiple, warning!

For functions in R, 
a vector can be input or output.
Recall that even a single number is a vector, as vector is the most basic building block in R; 
 and thus function will treat a vector as a whole (but not like building arrays i.e. vectors in C)


### 3.5 The power of vectorised operations

```R
x <- rnorm(5)
x #actually is a vector of five entries

#R specific programming loop 
#(i itself is each entry, instead of index in conventional version below)
for(i in x){
    print(i)
}

#equivalently
print(x[1])
print(x[2])
print(x[3])
print(x[4])
print(x[5])

#iteration: do same thing repeatedly

#conventional programming loop
for(j in 1:5){
    print(x[j])
}

#----------2nd part for today-----------

N <- 100
a <- rnorm(N)
b <- rnorm(N)
#vectorised approach
c <- a * b

#de-vectorised approach
d <- rep(NA, N) #logical, empty vector
for(i in 1:N){
    d[i] <- a[i] * b[i]
}
#c and d are identical; but vectorised approach is more efficient 
#and actually faster in R, seen by increasing N to large like 1000000

#remark: a low-level language like C, splitting into pieces will make it faster, in contrary with the case above
#R is high-level language, performing vectorised version faster
#The reason of such a phenomenon is that R knows we do not mix types of variables in a vector, i.e. only doubles
are in the a and b, so that it can only tell once its underlying low-level language such as C what to do; 
for the non-vectorised approach R has to tell N times its underlying language, which takes more time.

```



### 3.6 Functions in R
Functions are similar to blenders; we input fruits (data) into it and it outputs smoothie.

Recall all the functions we have used: 
```R
rnorm(n, mean, sd)

c(item1, item2, ...)#combine items to be a vector
seq(from, to, by)
rep(n, item)

print(item)

typeof()
is.numeric()
is.integer()
is.double()
is.character()

sqrt()
paste()

?rnorm() #adding '?' in front of a function will gives guides on it on the lower right window

#Not inputting an argument means taking the default value
#Can name the parameters when inputting the values of them, which allows swapping them in order
#or not naming, but now we must input them in the default order

seq(from, to, by)
seq(from=10, to =20, length.out=100) #length.out=number of items to output, generating by=(to-from)(length.out-1)
x <- c('a', 'b', 'c')
seq(from=10, to=20, along.with=x) #providing number of items to output by equating it to the length of the vector given; 
#equivalently length.out=3 here


?rep()
rep(5, times=10)
rep(5:6, times=10)
rep(5:6, each=10) #each entry in vector 5:6 = c(5, 6) is replicated ten times, 5 first and 6 afterwards
x <- c('a', 'b', 'c')
rep(x, times=5)
rep(x, each=5)


A <- seq(from=10, to=20, along.with=x)
B <- sqrt(A)
B

```



### 3.7 Packages in R
Packages contain blenders (functions), and possibly some fruits (data)

designed for specific aims, like graphs, charts, data frames, etc.

__Packages__ are collections of R functions, data and compiled code in a well-defined format. 
The directory where packages are stored is called the __library__.

Look at the lower right window and click 'packages', the installed packages can be seen, activated and de-activated (checking or de-checking)there.
Or delete a package from your computer by clicking the cross on the right end

The biggest webpage for comprehensive R resources is [cran](https://cran.r-project.org)


```R
#in R script
install.packages('ggplot2')
#then can see its installation to computer in the console

#but now it is not activated yet
?qplot()
?ggplot()
?diamonds

library(ggplot2)
#now package of ggplot2 is activated by the library()
#and now we can use functions provided by ggplot2
?qplot()
?ggplot()
?diamonds

#later we will use ggplot2 like this: 
qplot(data=diamonds, carat, price, colour=clarity, facets=.~clarity)

```

### Recap of Section 3
1. What is a vector? Only one type of variables in one vector; otherwise, R automatically turns all numerics to integers by adding '' to them
2. Created some vectors: c(), seq(), rep()
3. Check types: is.numeric(), is.character()
4. Using \[\] brackets, vector\[index vector\]; even one number is a 1-element vector
5. Vectorised operations
6. Power of vectorised operations; R-specific, taking i as elements of vectors (faster in R) and conventional for loop, taking j as indices
7. Functions in R, 'blender'; ?function() to see guide
8. Packages in R

Homework: Financial statement analysis

Quiz
Vector arithmetics: entry-by-entry
Vector has one single type: turning numerics into characters automatically if mixing
install.package('') to install a package from Internet, and then activate it by library()
