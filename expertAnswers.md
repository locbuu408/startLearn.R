# Key to Expert Test

Note that these are my asnwers, in many cases there may be more than one way to correctly performa in operation in R. What is important isn't that you used the exact same code, but that you produce the same outputs.

1) What is the mean, median, and standard deviation of precip?

````r
> mean(precip)
[1] 34.91571
> median(precip)
[1] 36.6
> sd(precip)
[1] 13.33442
````

2) Is precip best visualized using a ````barplot( )```` or ````hist( )````? Why?

````hist( )````, because precip is continuous data.

3) Generate a vector of random numbers drawn from a normal distribution with the same mean, standard deviation, and number of elements as in the precip dataset. Name this vector RandomNormal.

````r
RandomNormal<-rnorm(length(precip),mean(precip),sd(precip))
````

4) Write a function that tests, based on the means of each distribution, whether it is likely that RandomNormal and precip were drawn from the same underlying distribution.

````r
comparePrecip<-function(precip,RandomNormal,Iterations=100) {
    # Find the current difference in means between precip and RandomNormal
    MeanDifference<-mean(precip)-mean(RandomNormal)
    
    # Create a hypothetical sampling distribution named barrel 
    # using BOTH the observed Control and Treatment
    Barrel<-c(precip,RandomNormal)

    # Create a 1-dimensional array to store the output of the replications
    ReplicatedMeans<-array(data=NA,dim=Iterations)

    # Create a for( ) loop that repeats the process 100 times.
    for (Counter in 1:Iterations) {

        # Make sure that you sample the same number of specimens for each species
        # as in the original dataset
        NewPrecip<-sample(Barrel,length(precip),replace=TRUE)
        NewRandomNormal<-sample(Barrel,length(RandomNormal),replace=TRUE)

        # Find the means 
        PrecipMean<-mean(NewPrecip)
        RandomMean<-mean(NewRandomNormal)

        # Find the difference of the means and store it in the ReplicatedMeans array
        ReplicatedMeans[Counter]<-RandomMean-PrecipMean

        }
        
    # Find the percentage of differences in Replicated means that are more extreme than what you observe.
    Percentage<-length(which(ReplicationResults>MeanDifference))/Iterations
    return(Percentage)
    }
````

5) Create a density( ) plot of precip and RandomNormal. Is the test you performed above (question 4) a good or bad indicator of whether the two distributions are identical? Why or why not?

Depends, they do both have similar peaks (i.e., medians, modes, and means). However, notice that precip has a second smaller peak around a value of 15, whereas RandomNormal only has the one peak.