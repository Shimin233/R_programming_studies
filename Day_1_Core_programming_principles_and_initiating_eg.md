## Section 1: An initiating example of data science via R: Mispriced diamonds
R is powerful and efficient in analysing data.
Just view the video and we will come back at the end of this course, to summarise the techniques used in this example.

## Section 2: Core_programming_principles
### 2.0 
I think I should explain the parts in the application, R Studio, before learning to code there
source "shell"
console
environment
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

#logical (TRUE and FALSE)
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
#Logical
#TRUE T
#FALSE F

4<5 #TRUE
10>100 #FALSE
4==5 #FALSE

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

can type codes and run it directly in the console, without using the source at all

shell

### 2.6 The 'for' loop

### 2.7 The 'if' loop

## Recap of Section 2 
