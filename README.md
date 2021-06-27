# naive_bayes_example
Naive Bayes Machine Learning Model

> ## Naive Byes Classification with R
> ##Libraries
> library(naivebayes)
> library(dplyr)
> library(ggplot2)
> library(psych)
> data<-read.csv("binary.csv",header=T)
> str(data)
'data.frame':	400 obs. of  4 variables:
 $ admit: int  0 1 1 1 0 1 1 0 1 0 ...
 $ gre  : int  380 660 800 640 520 760 560 400 540 700 ...
 $ gpa  : num  3.61 3.67 4 3.19 2.93 3 2.98 3.08 3.39 3.92 ...
 $ rank : int  3 3 1 4 4 2 1 2 3 2 ...
> xtabs(~admit+rank,data)
     rank
admit  1  2  3  4
    0 28 97 93 55
    1 33 54 28 12
> data$rank<-as.factor(data$rank)
> data$admit<-as.factor(data$admit)
> ## visualisation
> pairs.panels(data[-1])
http://127.0.0.1:38951/graphics/b3fcb89f-01ab-4341-8ece-39a642d78528.png
