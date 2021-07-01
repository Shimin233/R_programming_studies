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



Functions in R

Packages in R

Recap of Section 3

Homework: Financial statement analysis

Quiz
