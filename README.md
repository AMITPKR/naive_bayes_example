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

data%>%
  ggplot(aes(x=admit,y=gpa,fill=admit))+
  geom_boxplot()+
  ggtitle("BOX PLOT")
  
 ![image](https://user-images.githubusercontent.com/70443251/123533112-64887a80-d730-11eb-93e0-8cc53bed7203.png)
 

data%>%
  ggplot(aes(x=gre,fill=admit))+
  geom_density(alpha=0.8,color='black')+
  ggtitle("DENSITY PLOT")
  
  ![image](https://user-images.githubusercontent.com/70443251/123533117-71a56980-d730-11eb-949b-9d0eed8516a1.png)


## data partition
library(rsample)

??rsample  ## Know about Rsample


initials<-initial_split(data)

train<-training(initials)

test<-testing(initials)

## naive bayes's model
model<-naive_bayes(admit~.,train)

model

train%>%
  filter(admit=='1')%>%         ## student those are not admitted
  summarise(mean(gre),sd(gre))           

plot(model)
![image](https://user-images.githubusercontent.com/70443251/123533134-93065580-d730-11eb-86ae-f5a24691a076.png)


##Predict 
p<-predict(model,train,type='prob')

p

head(cbind(p,train))

## confusion matrix for train data

p1<-predict(model,train)

tab1<-table(predicted=p1,actual=train$admit)

tab1

1-sum(diag(tab1))/sum(tab1) # % of misclassification of training data
>[1] 0.3133333

## confusion matrix for test data
model1<-naive_bayes(admit~.,test)

p2<-predict(model1,test)

tab2<-table(predicted=p2,actual=test$admit)

tab2

1-sum(diag(tab2))/sum(tab2)
>[1] 0.24

