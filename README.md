### Naive Byes Classification with R
### Libraries
library(naivebayes)

library(dplyr)

library(ggplot2)

library(psych)

data<-read.csv("binary.csv",header=T)

str(data)

xtabs(~admit+rank,data)

data$rank<-as.factor(data$rank)

data$admit<-as.factor(data$admit)

### visualisation
pairs.panels(data[-1])

![image](https://user-images.githubusercontent.com/70443251/123532915-132bbb80-d72f-11eb-8fc5-076cd0668b7b.png)

