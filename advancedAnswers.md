# Key to Advanced Test

Note that these are my asnwers, in many cases there may be more than one way to correctly performa in operation in R. What is important isn't that you used the exact same code, but that you produce the same outputs.


1) Write a function that returns the phrase "Hello, World."

````r
> greetWorld<-function(Message) {
      print(Message)
      }
> greetWorld("Hello, World.")
[1] "Hello, World."

# or

> greetWorld<-function(Message) {
      return(Message)
      }
> greetWorld("Hello, World.")
[1] "Hello, World."

# or 

> greetWorld<-function( ) {
      return("Hello, World.")
      }
> greetWorld()
[1] "Hello, World."
````

2) Load the ````iris```` dataset we used in the earlier tests. Write a function that takes ````iris```` as its argument, and returns three subsets of the data.frame split by the three different types of species (saved as a single object).

````r
# An easy version
IrisFunction<-function(iris) {
  Setosa<-iris[which(iris[,"Species"]=="setosa"),]
  Virginica<-iris[which(iris[,"Species"]=="virginica"),]
  Versicolor<-iris[which(iris[,"Species"]=="versicolor"),]
  return(list(Setosa,Virginica,Versicolor)
  }

# A difficult, but more versatile version that will accept any dataset (not just iris) 
# and split it by the unique categories in the column
IrisFunction<-function(Dataset,Column) {
  Categories<-unique(Dataset[ ,Column])
  BlankList<-list()
  for (i in 1:length(Categories)) {
      BlankList[[i]]<-Dataset[which(Dataset[,Column]==Categories[i]),]
      }
  return(BlankList)
  }
> IrisFunction(iris,"Species")
````

3) Write a function that takes ````iris```` as its argument. The function should, for each row, add Sepal.Length and Petal.Length if Sepal.Width is > 3.1. It should substract Petal.Length from Sepal.Length if Sepal.Width is <3.1. The answer should be returned as a vector.

````r
# Using if/else version
# Roughly how I intended for you to do it.
IrisFunction<-function(iris) {
  # Create an array to store the ouptut
  AnswerVector<-array(NA,dim=dim(iris)[[1]])
  # Create a for( ) loop that runs through every row of hte iris dataset
  for (index in 1:dim(iris)[[1]]) {
    # Use an if statement to isolate rows where Sepal.width is >3.1
    if (iris[index,"Sepal.Width"]>3.1) {
      # Add Petal Length and Sepal width
      AnswerVector[index]<-iris[index,"Petal.Length"]+iris[index,"Sepal.Length"]
       }
    # Use an else if statement to isolate rows where Sepal.width is >3.1
    else if (iris[index,"Sepal.Width"]<3.1) {
      # Subtract Petal Length and Sepal Length
      AnswerVector[index]<-iris[index,"Sepal.Length"]-iris[index,"Petal.Length"]
      }
    }
  return(AnswerVector)
  }
````

4) Load the ````mtcars```` dataset we used in the earlier tests. Write a function that takes a number of cylinders as its argument. Have the function return the average miles per gallon (column mpg) for all cars with that many cylinder (column cyl).

````r
findMPG<-function(NumCylinders) {
  # Subset the mtcars dataset to just rows where cyl is equal to NumCylinders
  CylinderSubset<-mtcars[which(mtcars[,"cyl"]==NumCylinders),]
  # Find the mean of the mpg column in the subset
  Answer<-mean(CylinderSubset[,"mpg"])
  return(Answer)
  }
````

5) Write a function that simulates 1,000,000 powerball drawings. A powerball drawing takes a random sample of 5 numbers (without replacement) from 1 through 69, plus one powerball number ranging from 1 through 26. The function should return a single object recording all of your draws.

````r
PowerballDraw<-function(NumDrawings) {
  # Create a matrix to store the output
  # You want 6 columns, one for each lottery number.
  DrawsMatrix<-matrix(NA,nrow=NumDrawings,ncol=6)
  # Create a for( ) loop that repeats the drawing process
  for (draw in 1:NumDrawings) {
    DrawsMatrix[draw,1:5]<-sample(c(1:69),5,replace=FALSE)
    DrawsMatrix[draw,6]<-sample(c(1:26),1,replace=FALSE)
    }
  return(DrawsMatrix)
  }
  
> PowerballDraw(1000000)
````

6) Write a function that take a single set of lottery numbers (as a vector) as its argument. As before, write a function that simulates 1,000,000 powerball drawings. Have the function return a TRUE or FALSE value if you won any of the drawings.

````r
# Make a function that takes a vector of lottery numbers
PowerballDraw<-function(MyNumbers) {
  # Create a matrix to store the output
  # You want 6 columns, one for each lottery number.
  DrawsMatrix<-matrix(NA,nrow=1000000,ncol=6)
  # Create a for( ) loop that repeats the drawing process
  for (draw in 1:1000000) {
    DrawsMatrix[draw,1:5]<-sample(c(1:69),5,replace=FALSE)
    DrawsMatrix[draw,6]<-sample(c(1:26),1,replace=FALSE)
    }
  # Next test if any of the 1000000 draws is equal to MyNumbers
  # Create a vector to store your tests in
  TestForMatch<-array(NA,dim=1000000)
  for (test in 1:1000000) {
    TestForMatch[test]<-all(DrawsMatrix[test,]==MyNumbers)
    }
  # See if any of your tests got a postive result - i.e., TRUE
  Result<-any(TestForMatch)
  return(Result)
  }
````
