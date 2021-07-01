## Section 3: Fundamentals of R

Tip: Double quotation marks and single quotations marks can both represent a character in R, like both of them working for strings in Python.

### 3.1 Vector
its indices are 1, 2, 3, ...

Note the indices of a vextor in many of other languages start with zero: 0, 1, 2, ...; e.g. Python
### 3.2 Create some vectors

seq(start, stop, step)
#by dafault, start=1, stop=ending (included), step=1
compare seq(1, 5) with 1:5

Note that in Python, a similar code is range(start, stop, step), where by default start=0, stop=ending (not included), step=1; 
e.g. range(5) means 0, 1, 2, 3, 4 with indices 0, 1, 2, 3, 4

rep()
### 3.3 Using the \[\] brackets

\[\] brings a vector to indices

Note that in Python, a similar code is `range(start, stop, step)[index]`

Q: if inputting an unavailable index in \[\], does R give an 'IndexError' or similar?
Vectorised operations

### 3.4 Vectorised operations
vector arithmetics

= entry by entry arithmetics

arithmetics between a longer vector and a shorter: 
Recycling of vectors
in the shorter vector

if longer (length0 is multiple of shorter
if not, warning

function
vector can be input or output
 even a single number is a vector, as vector is the most basic building block in R
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

[The biggest webpage for comprehensive R resources](https://cran.r-project.org)


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
1. What is a vector? Only one type of variables in one vector
2. Created some vectors: c(), seq(), rep()
3. Check types: is.numeric(), is.character()
4. Using \[\] brackets, vector\[index vector\]; even one number is a 1-element vector
5. Vectorised operations
6. Power of vectorised operations; R-specific, taking i as elements of vectors (faster in R) and conventional for loop, taking j as indices
7. Functions in R, 'blender'; ?function() to see guide
8. Packages in R

Homework: Financial statement analysis

Quiz
