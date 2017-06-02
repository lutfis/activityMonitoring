# Single R Markdown



## Assignment Summary
This assignment makes use of data from a personal activity monitoring device. This device collects data at 5 minute intervals through out the day. The data consists of two months of data from an anonymous individual collected during the months of October and November, 2012 and include the number of steps taken in 5 minute intervals each day.
The data for this assignment can be found in the directory

## Loading the Data

```r
activitydata <- read.csv("activity.csv")
str(activitydata)
```

```
## 'data.frame':	17568 obs. of  3 variables:
##  $ steps   : int  NA NA NA NA NA NA NA NA NA NA ...
##  $ date    : Factor w/ 61 levels "2012-10-01","2012-10-02",..: 1 1 1 1 1 1 1 1 1 1 ...
##  $ interval: int  0 5 10 15 20 25 30 35 40 45 ...
```

## Data Check and Processing

```r
mean(is.na(activitydata$steps))
```

```
## [1] 0.1311475
```
13% of the data in "steps" colomn is NA.

For the "date" and "interval" colomns, we have to reformat them into one POXIT formatted variable. it should start with "2012-10-01 00:00" and continue as "2012-10-01 00:05", "2012-10-01 00:10", "2012-10-01 00:15" and so on.

```r
library(dplyr)
```

```
## 
## Attaching package: 'dplyr'
```

```
## The following objects are masked from 'package:stats':
## 
##     filter, lag
```

```
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```r
activitydata <- mutate(activitydata, hour = interval %/% 100, minute = interval %% 100)
```

