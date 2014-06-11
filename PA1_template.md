# Reproducible Research: Peer Assessment 1
This markdown file analyzes the data provided for Peer Assessment 1 of the Coursera
Reproducible Research course. The data comes from a personal activity monitoring device,
collected at 5 minute intervals throughout the day. This was done for an anonymous individual
over 2 months in October and November of 2012. The data includes the number of steps the
individual took throughout each 5 minute interval.

## Loading and preprocessing the data
The data set first needs to be unzipped. It can then be loaded into a data frame.
The variable classes for each column are set manually to avoid confusion, as is
the presence of a header line.

```r
unzip("activity.zip")
activity<-read.csv("activity.csv",header=TRUE,colClasses=c("numeric","Date","numeric"))
```

## What is mean total number of steps taken per day?
In order to avoid the effect of NA values in the data set, we first define a utility function
that will perform the sum over non-NA inputs.

```r
noNAsum <- function (x) { sum(x, na.rm = TRUE) }
```

We then use this to sum the number of steps taken each day by treating the activity$date
variable as a factor.

```r
stepSum <- tapply(activity$steps,factor(activity$date),noNAsum)
```

A histogram shows the distribution of the number of steps each day.

```r
hist(stepSum,breaks=10,xlab="Number of Steps per Day",
     main="Distribution of Daily Sum of Steps")
```

![plot of chunk step_histogram](figure/step_histogram.png) 

The mean and median number of total steps per day can also be computed.

```r
meanSteps <- mean(stepSum)
medSteps <- median(stepSum)
```
We find that the mean is 9354.2295 steps/day and the median is 1.0395 &times; 10<sup>4</sup> steps/day.

## What is the average daily activity pattern?
To look at the average daily activity pattern, we will first define a utility
function much like we did for the sum, only now to perform the mean while
ignoring any NA values.

```r
noNAmean <- function (x) { mean(x, na.rm = TRUE) }
```

We can then apply this to the original data and treat the 5-minute interval as a
factor. This will provide us with the average number of steps taken in each time
interval over all days in the data set.

```r
stepMean <- tapply(activity$steps,factor(activity$interval),noNAmean)
```

A line plot provides us with a visualization of this average trend over the day.

```r
plot(unique(activity$interval), stepMean, type="l", xlab="5-Minute Interval",
     ylab="Avg Number of Steps", main="Mean Number of Steps Taken Per Interval")
```

![plot of chunk steps_avg_plot](figure/steps_avg_plot.png) 

## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
