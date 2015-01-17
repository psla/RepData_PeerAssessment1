# Reproducible Research: Peer Assessment 1

```
## Loading required package: plyr
```

## Loading and preprocessing the data

```r
activity = read.csv("activity/activity.csv")
activity_complete = activity[complete.cases(activity),]
```

## What is mean total number of steps taken per day?

```r
steps_per_day = ddply(activity_complete, c("date"), summarize, total_steps = sum(steps))
hist(steps_per_day$total_steps, main = "Histogram of steps taken per day", xlab = "Total steps per day")
```

![](PA1_template_files/figure-html/unnamed-chunk-3-1.png) 

```r
avg_steps_per_day = mean(steps_per_day$total_steps)
rounded_avg_steps_per_day = round(avg_steps_per_day, 0)
median_steps_per_day = median(steps_per_day$total_steps)
```
Average total number of steps taken per day is 1.0766\times 10^{4}.
The median is 10765 steps.

## What is the average daily activity pattern?

```r
steps_per_interval = ddply(activity_complete, c("interval"), summarize, avg_steps = mean(steps))
with(steps_per_interval, plot(interval, avg_steps, type = "l"))
```

![](PA1_template_files/figure-html/unnamed-chunk-4-1.png) 

```r
max_steps_per_interval = steps_per_interval[which.max(steps_per_interval$avg_steps), ]
```

The most steps (``206.1698113``) were taken at interval ``835``

## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
