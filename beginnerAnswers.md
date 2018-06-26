# Key to Beginner Test

Note that these are my asnwers, in many cases there may be more than one way to correctly performa in operation in R. What is important isn't that you used the exact same code, but that you produce the same outputs.

1) What class of object is ````mtcars````? What function did you use to find out?

````r
> class(mtcars)
[1] "data.frame"
````

2) Is ````precip```` defined as a 1-dimensional array or a vector? How did you find out?

````r
> is(precip,"vector")
[1] TRUE

> length(precip)
[1] 70

> names(precip)
````

3) How would you convert the data.frame ````trees```` into a matrix?

````r
# You can use various versions of the as( ) function
> NewMatrix<-as(trees,"matrix")
> NewMatrix<-as.matrix(trees)
> NewMatrix<-data.matrix(trees)

# Or you could create a new matrix/array
> NewMatrix<-matrix(c(trees[,"Girth"],trees[,"Height"],"trees[,"Volume"]),nrow=nrow(trees),ncol=ncol(trees))
> NewMatrix<-array(c(trees[,"Girth"],trees[,"Height"],"trees[,"Volume"]),dim=c(nrow(trees),ncol(trees)))
````

4) What is the name of the 14th city in the ````precip```` dataset?

````r
> precip[14]
````

5) What function would you use if you wanted to combine all three data sets into a single object?

````r
> MyList<-list(precip,trees,mtcars)
````

6) Does precip consist of **numeric** data? How did you find out?

````r
> is(precip,"numeric")
[1] TRUE

# Remember that double is equivalent to numeric
> typeof(precip)
[1] "double"
`````

7) Code four different ways to subscript the 2nd row and 7th column of ````mtcars```` using bracket notation - i.e., 17.02.

`````r
> mtcars[2,7]
[1] 17.02

> mtcars["Mazda RX4 Wag",7]
[1] 17.02

> mtcars["Mazda RX4 Wag","qsec"]
[1] 17.02

> mtcars["Mazda RX4 Wag",][7]
               qsec
Mazda RX4 Wag 17.02

> mtcars[,"qsec"][2]
[1] 17.02
````

8) How would you change the precipitation values of "Juneau", "Phoenix", and "Sacramento" to 23, 46, and 12 in the precip dataset. (Hint: You will need to use subscripts and the <- operator).

````r
> precip[c("Juneau","Phoenix","Sacramento")]<-c(23,46,12)
# or
> precip[which(names(precip)=="Juneau" | names(precip)=="Phoenix" | names(precip)=="Sacramento")]<-c(23,46,12)
````

9) Are there **any** ````trees```` in the ````trees```` dataset with more girth than volume? How did you find out?

````r
> any(trees[,"Girth"]>trees[,"Volume"])
[1] FALSE
````

10) Take the sum of all elements in column height of the trees dataset, call this value A. Take the sum of all elements in row Valiant of the mtcars dataset, call this value B. Take the sum of the first 8 elements of the precip dataset, call this value C. Divide C by B and add A. What is your final answer?

````r
> A<-sum(trees[,"Height"])
> B<-sum(mtcars["Valiant",])
> C<-sum(precip[1:8])
> (C/B)+A
[1] 2356.633
````

