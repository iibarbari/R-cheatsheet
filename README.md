# R Cheatsheet

## Table Of Contents

1. [Get and Set Directories](#Get-and-Set-Directories)
1. [Vectors](#Vectors)
1. [Relational and Logical Operators](#Relational-and-Logical-Operators)
1. [if/else, switch](#if/else,-switch)
1. [Strings](#Strings)
1. [Factors](#Factors)
1. [Data Frames](#Data-Frames)
1. [Loops](#Loops)
1. [Matrices](#Matrices)
1. [Multidimensional Arrays](#Multidimensional-Arrays)
1. [Functions](#Functions)
1. [Error Handling](#Error-Handling)
1. [Read Data](#Read-Data)

## Get and Set Directories

```r
getwd()
setwd('~/Desktop/learnR')
```

## Vectors

```r
numbers <- c(10, 22, 4, 1, 8)
numbers

numbers[1]

# Vector length
length(numbers)

# Last Value
numbers[length(numbers)]
numbers[-1]
tail(numbers,1)

# First two values
numbers[c(1, 2)]
head(numbers, 2)

# Replace values
numbers[c(1, 2)] = 2
numbers

# Sort values
sort(numbers)
sort(numbers,decreasing = T)

# Create Ranges
oneToTen <- c(1:10)
oneToTen

# Create sequences
add3 = seq(from=5, to=25, by=3)
add3

evens = seq(from=0, by=2, length.out = 10)
evens

# Repeat elements
rep(x=2, times=5, each=2)
rep(x=c(1, 2, 3), times=5, each=3)
```

## Relational and Logical Operators

```r
# Relational Operators
4 == 5
4 != 5
4 > 5
4 >= 5
4 < 5
4 >= 5

oneToTwenty <- c(1:20)

# map
isEven <- oneToTwenty %% 2 == 0
isEven

# filter
justEvens = oneToTwenty[oneToTwenty %% 2 == 0]
justEvens

# Logical Operators
T && T
T && F
T || T
T || F
!T
```

## if/else, switch

```r
# if/else
age = 18

if(age >= 18) {
  print('vote')
} else if (age >= 16){
  print('drive')
} else {
  print('wait')
}

# switch
grade = 'C'

switch(grade,
       'A' = print('Grape'),
       'B' = print('COOL'),
       'C' = print('COOLER'),
       'D' = print('COOLEST'),
       'F' = print('Oops'),
       print('mmm'))
```

## Strings

```r
#https://www.youtube.com/watch?v=ZNb7fyKvtEE&ab_channel=BrendanO
exampleStr = 'Let me entertain you'

# Number of characters
nchar(exampleStr)

# alphabetically checks strings (later letters are greater (z>a))
'betty' > 'midler'
'betty' < 'midler'
'betty' >= 'midler'
'betty' <= 'midler'

# merge
str1 = paste('let me','make you smile', sep =' ')
str1

# subtract
substr(x = str1, start = 5, stop = 6)

# substitute first match
sub(pattern='smile', replacement ='feel good', x=str1)

# substitute all matches
gsub(pattern='you', replacement ='me', x='Do you? Oh, you do')

# split string to vector
strVect = strsplit('gipsy is a great musical', ' ')
strVect
```

## Factors

```r
# Create a factor vector
direction = c('up', 'right', 'down', 'left', 'left', 'down')
factorDir = factor(direction)

# Check if it's a Factor
is.factor(factorDir)

# A Factor object contains levels which store all possible values
levels(factorDir)

# sort factors
dow <- c('mon', 'tues', 'wed', 'thurs', 'fri', 'sat', 'sun')
wDays <- c('fri', 'wed', 'mon')
wdFact <- factor(x = wDays, levels = dow, ordered = T)
wdFact
```

## Data Frames

```r
millenialPop = data.frame(name = c('black eyed peas', 'justin timberlake', 'missy elliot'),
                          coolness = c(10, 15, 25),
                          stringsAsFactors = F)

millenialPop

#get second column
millenialPop[2]

#get first row two columns
millenialPop[1,1:2]

#get first row second column
millenialPop[1,2]

# get by column name
millenialPop$coolness

#dimension
dim(millenialPop)

# add new data
newData = data.frame(name = 'amy winehouse', coolness = 30)
millenialPop = rbind(millenialPop, newData)
millenialPop

# add new column
depressed = c(1, 5, 0, 20)
millenialPop = cbind(millenialPop, depressed)
millenialPop

# filter data
danceable = millenialPop[millenialPop$depressed < 5,]
danceable
```

## Loops

```r
num = 15

# repeat
repeat {
  print(num)

  num = num + 1

  if (num > 10) {
    break
  }
}

# while
while (num> 0) {
  num = num - 1

  if (num %% 2 == 0) {
    next
  }

  print(num);
}

# for loop
oneToFive = 1:5

for (i in oneToFive) {
  print(i)
}
```

## Matrices

```r
# define matrix
matrix1 = matrix(data = c(1, 2, 3, 4))
matrix1

matrix2 = matrix(data = c(1, 2, 3, 4), nrow = 2, ncol = 2)
matrix2

# fill matrix by row
matrix3 = matrix(data = c(1, 2, 3, 4), nrow = 2, ncol = 2, byrow = T)
matrix3

# dimension
dim(matrix3)

# get values
matrix3[,2]
matrix3[1,2]
matrix3[1,]

matrix4 = rbind(1:3, 4:6, 7:9)
matrix4[2:3,]
matrix4[,2:3]

# change values
matrix4[1,1] = 0
matrix4[,2] = c(10, 20, 30)
matrix4
```

## Multidimensional Arrays

```r
array1 = array(data = 1:8, dim=c(2, 2, 2))
array1
array1[1,2,2]
```

## Functions

```r
sum = function (num1 = 0, num2 = 0) {
  num1 + num2
}

print(sum(1, 2))
print(sum())

makeList = function (str = '') {
  return (strsplit(str, ' '))
}

makeList('mamini mamini microphone showw')

# handle missing arguments
missingArgs = function(x) {
  if (missing(x)) {
    return ('please pass x')
  }

  return (x)
}

missingArgs()

# spread arguments
getSumMore = function (...) {
  numList = list(...)

  sum = 0

  for (i in numList) {
    sum = sum + i
  }

  return (sum)
}

getSumMore(1, 2, 3, 4, 5)
getSumMore()

# anonymous functions
numList = 1:10
dblList = (function (x) x*2)(numList)
dblList

# closures
power = function(exp) {
  function(x) {
    x ^ exp
  }
}

cubed = power(3)
cubed(2)

cubed(1:5)
```

## Error Handling

```r
divide = function(dividend, divisor) {
  tryCatch(
    dividend / divisor,
    error = function(e) {
      if(is.character(dividend) || is.character(divisor)) {
        return ('Can\'t divide strings')
      }
    }
  )
}

divide('1','2')
```

## Read Data

```r
## csv
data <- read.csv('./reddit.csv')
```
