# Key to Intermediate Test

Note that these are my asnwers, in many cases there may be more than one way to correctly performa in operation in R.

#### Section 1 Questions
<span>1.</span> What does the ````REPLACE=```` argument of the ````sample( )```` function do?
 
* The arguement 'repalce' tells the ``sample()`` function to replace the numbers drawn at randome back in the poll of possible numbers. This allows us to randomly sample each number more than one time.

<span>2.</span> Using````as(MyMatrix,"numeric")```` will not convert ````MyMatrix```` to numeric data! Can you think of a property of logicals that you can use to convert the logicals to 0's and 1's other than the ````as( )```` function?

````r
> MyMatrix*1 # mathematical operations on logicals treats them as 0s and 1s.
````

<span>3.</span> If you wanted to check if **all** of the elements in each row are true, how would you do this?

````r
# this returns a vector of logicals, one for each row. If true, then all values in a row are true.
> apply(MyMatrix, 1, sum) == ncol(MyMatrix)
````

#### Section 2 Questions

1. How many times does the number 7 occur in ````MyMatrix````?

````r
> mySevens <- MyMatrix[MyMatrix == 7] # a vector that contains all of the 7s 
> length(mySevens) # count the length of mySevens
````

<span>2.</span> How do you find the sum of each column?

````r
> apply(MyMatrix, 2, sum) # this is one way
> colSums(MyMatrix) # does the same thing
````
<span>3.</span> How do you find the product of each column?

````r
> apply(MyMatrix, 2, prod) # sadly there's no shorcut function for this one
````

<span>4.</span> How would you change every instance of the number 10 to 12?

````r
> MyMatrix[MyMatrix == 10] <- 12
````

<span>5.</span> How many values in ````MyMatrix```` are greater than 3 and less than 8?

````r
length(MyMatrix[which(MyMatrix > 3 & MyMatrix < 8)])
[1] 33
````

<span>6.</span> How do you change the elements of column 12 into **character data**, while keeping columns 1- 11 as numeric data??

````r
# for this one you want to convert your matrix to a data frame first. A data frame is useful because it can contain values with different object types (e.g., characters, logicals, numerics).
> MyDataFrame <- as.data.frame(MyMatrix)
> MyDataFrame[,12] <- as.character(MyDataFrame[,12])
````

<span>7.</span> Find which rows of MyMatrix have a sum >70. Make a *new* version of MyMatrix where the 13th column is a set of ````TRUE```` and ````FALSE```` values denoting which rows have a sum >70. (Hint: What type of object allows you to store both logical and numeric data at once?)

````r
# we already created a data frame for the question above, which allows multiple multiple data types!
MySums <- rowSums(MyMatrix)
MyDataFrame$V13 <- MySums > 70 # the right hand-side of the quation creates a list of logicals corresponding to the arguement
````