[Other resources (cheat sheets, etc.)](https://education.rstudio.com/learn/beginner/)

## Section 1: An initiating example of data science via R: Mispriced diamonds
R is powerful and efficient in analysing data.
Just view the video and we will come back at the end of this course, to summarise the techniques used in this example.

## Section 2: Core_programming_principles
### 2.0 
I think I should explain the parts in the application, R Studio, before learning to code there. Note the following parts of R studio are specified with their default position, and you can move then as you like.
- Script (or shall we also call it "source"?), on the left upper part in R studio by default, showing a file with R codes that are prepared to run in the console (discussed below). 
As far as I am concerned, it is like how the module works for Python.
- Console, on the left lower part, where you have your codes actually run and giving results. I reckon it is like how the shell works for Python.
- Environment, on the right upper, where you can see the variables and their values you defined before.
- Plots, Packages, Files, etc., on the right lower, where you can see the plotted diagrams, the packges you load in your computer, the folders and files in your computer, etc.

### 2.1 Types of variables
create a R script for the coding in this subsection

this instructor uses Mac

5 atomic (basic and important) types of variables

1 integer
 
```R
#integer
x<-2L
typeof(x) #check the type of x
```
command + return

is going to be copied into console and run

2 Double
```R
#double
y<-2.5
typeof(y)
```

```R
#double by default
x<-2
typeof(x)
```
specify the integer type of your variable by adding `L` at the end of your number



3 complex
```R
#complex
z<-3+2i
typeof(z)

#character
a<-"h"
typeof(a) #will get an error if not creating it yet; so run the codes in its desired order, here I mean defining a and then check its type

#logical, or called boolean (TRUE and FALSE)
q1<- T
typeof(q1)
q2<- FALSE
typeof(q2)
```

\# for comments in R

### 2.2 Using variables
save the codes by command + s

clean up the environments with our variables created last time, by simple clicking the button at the top of the environment

create a new R script for this time
```R
A <- 10
B <- 5

C<-A+B #C occurs as 15 in the environment
C #just type the name of the variable,then the value of C will be printed in the console

#variable 1
var1<-2.5
#variable 2  #the comments led by hashtag #, will be omitted when running codes
var2<-4 #highlight the line(s) you want to run together and press command + return

result<- var1/var2
result

answer<-sqrt(var2)
answer

greeting<- "Hello"
name<-"Bob"
message<- paste(greeting, name) #paste: combine characters together
message
```


### 2.3 Logical variables and operators
save the file from previous project by command + s
and create a new R script for this time


```R
#Logical variables are:
#TRUE T
#FALSE F

4<5 #TRUE
10>100 #FALSE
4==5 #FALSE

#Operators which can result in logical variables include: 
#==
#!=,  not equal
#<, >
#<=, >=
#!
#|, or
#&
#isTRUE(x)

result<- 4<5 #store a value containing operator in a vairable
result #TRUE
typeof(result) #logical

result2<- !(5>1) #not TRUE = FALSE
result2 #FALSE

result | result2 #TRUE or FALSE = TRUE
result & result2 #TRUE and FALSE = FALSE

isTRUE(result) #TRUE; since indeed result is TRUE
```

### 2.4 The 'while' loop

 
```R
while(abc){
  xyz
}
# execute the xyz (loop body) as long as abc is TRUE, and stops as soons as the abc becomes FALSE


while(FALSE){
  print("Hello")
} #nothing will be printed, as FALSE is always FALSE

while(TRUE){
  print("Hello")
} #constantly print "Hello"; click esc to stop an infinite loop

counter <- 1
while(counter < 12){
  print(counter)
  conuter <- counter + 1
} #will print 1, 2, ..., 10, 11; a variable called counter occurs as 12 in the environment

```


### 2.5 Using the console


```R
x <- 5
x

```

copied to console and print 5 in the console

can type codes and run it directly in the console, without using the source at all and the codes you typed like this will not be saved in the script part.

### 2.6 The 'for' loop
```R
#compare for loop and while loop side by side
counter <- 1
while(counter < 12){
  print(counter)
  conuter <- counter + 1
} 

for(i in 1:5){
  print("Hello R")
}
#1:5 is acutally a vector (1, 2, 3, 4, 5); here it is used to specify the condition to execute the body of for loop
#see contents of the vector, 1:5, by typing it
1:5

for(i in 5:10){
  print("Hello R")
}
5:10 #it is the vector (5, 6, 7, 8, 9, 10), with six entries
```


### 2.7 Random sampling and the 'if' statement

```R
rnorm(k) #generate k random sample(s) from a normal distribution
rnorm(1) #generate one random sample from a normal distribution

x <- rnorm(1)
if(x > 1){
  answer <- "Greater than 1"
} #if the random sample is no larger than 1, then no vairable called answer is built since the if loop body is not executed

#remove variable 
rm(answer)
x <- rnorm(1)
if(x > 1){
  answer <- "Greater than 1"
} #answer is removed before each execution of these codes, so we can see whether the variable called answer exists in the environment to see whether the if loop body is executed

#if-else
rm(answer)
x <- rnorm(1)
if(x > 1){
  answer <- "Greater than 1"
} else{
  answer <- "Less than 1"
}

#one more case 1: nesting
rm(answer)
x <- rnorm(1)
if(x > 1){
  answer <- "Greater than 1"
} else{

  if(x >= -1){
    answer <- "Between -1 and 1"
  } else{
  answer <- "Less than -1"
  }
  
}

#one more case 2: chaining, else if (this is preferrable than the last method)
rm(answer)
x <- rnorm(1)
if(x > 1){
  answer <- "Greater than 1"
} else if(x >= -1){
  answer <- "Between -1 and 1"
} else{
  answer <- "Less than -1"
}   #basically, if...else if...else... makes three parallel cases


```

__Compaison of these three loops/statements__
- if statement: execute the loop body _once_ when the condition is TRUE, and not execute when condition FALSE 
- while loop: execute the body _(possibly repeatedly)_ as long as the condition is TRUE
- for loop: execute the body for _EACH_ item in the condition
We can note that the two "loops" can execute their body iterately i.e. repeatedly, but the if "statement" either executes only once or not at all.

## Recap of Section 2
1 Five types of variables
2 Using variables: basic operations
3 Logical variables and operators
4 While loop
5 Using the console
6 For loop
7  If statement
8 random sample

## Homework: Law of large number
(See the related file /Users/shiminfu/Desktop/R_programming_studies/Section2-Homework-The-Challenge.pdf)
Q: Test the Law Of Large Numbers for N random normally distributed numbers with mean = 0, stdev = 1:
Create an R script that will count how many of these numbers fall between -1 and 1 and divide by the total quantity of N
You know that E(X) = 68.2%
Check that Mean(X_N) -> E(X) as you rerun your script while increasing N

A: See my solutions here /Users/shiminfu/Desktop/R_programming_studies/Section2hw_LLN.R
Note that the resulting average fluctuates a lot; this is ordinary, the solution according to the instructor's hint also behaves likewise.
It is just the fact that LLN cannot show itself that obviously, though it does hold.

## Quiz
If statement: isolates a block of codes and executes it only when a certain condition holds; executes only once, not iterately 
(but for and while both execute loop body iterately).
