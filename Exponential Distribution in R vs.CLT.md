---
Author: "Suresh Babu Kumpati"
Date: "November 21, 2015"
Output: pdf_document
Title: "Exponential Distribution in R  vs. Central Limit Theorem"
---
#Project Description:
In this project you will investigate the exponential distribution in R and compare it with the Central Limit Theorem. The exponential distribution can be simulated in R with rexp(n, lambda) where lambda is the rate parameter. The mean of exponential distribution is 1/lambda and the standard deviation is also 1/lambda. Set lambda = 0.2 for all of the simulations. You will investigate the distribution of averages of 40 exponentials. Note that you will need to do a thousand simulations.
Illustrate via simulation and associated explanatory text the properties of the distribution of the mean of 40 exponentials. You should
1.	Show the sample mean and compare it to the theoretical mean of the distribution.
2.	Show how variable the sample is (via variance) and compare it to the theoretical variance of the distribution.
3.	Show that the distribution is approximately normal.

#Project Simulation

#Sample Mean vs Theoretical Mean

 	Firstly analyze the sample mean and compare it to the theoretical mean

# Theoritcal mean comparison 
```{r}
set.seed(1)
lambda <- 0.2 
nexp <- 40 
nsim <- 1000 
mns <- NULL  
for (i in 1 : nsim) mns <- c(mns, mean(rexp(40,lambda)))
hist(mns,col="light green",main="Distribution of Means of rexp")
```
 
As we observe the histogram, with a mean – { mean(mns)  ## [1] 4.9900252} , we can compare to {1/lambda ( ## [1] 5) }, we observed the distribution of means is centred in the theoretical mean. 

# Sample Variance vs Theoretical Variance
```{r}
# lambda <- 0.2 # Set lambda as per instructions (does not change)
# nexp <- 40 # number of distributions (does not change)
# nsim <- 1000 # number of simulations (does not change)
varxp <- ((1/lambda)^2)/nexp # theoretical variance
varmean <- var(mns) # variance of the means
```
And we see that the theoretical variance is 0.625 (varxp <- ((1/lambda)^2)/nexp), whereas the variance of the means is 0.6111165 (var(mns)), which they can be compared.
Comparing to a Normal Distribution

According to the histogram which is similar to a normal distribution (i.e. what the Central Limit Theorem states “In probability theory, the central limit theorem (CLT) states that, at any given certain conditions, the arithmetic mean of a sufficiently large number of iterates of independent random variables, each with a well-defined expected value and well-defined variance, will be approximately normally distributed, regardless of the underlying distribution”)

```{r}
library(ggplot2)
plotdata <- data.frame(mns)
plot1 <- ggplot(plotdata,aes(x = mns))
plot1 <- plot1 +geom_histogram(aes(y=..density..), colour="black",fill="green")
plot1<-plot1+labs(title="Distribution of Means of rexp", y="Density")
plot1<-plot1 +stat_function(fun=dnorm,args=list( mean=1/lambda, sd=sqrt(varxp)),color = "red", size = 1.0)
plot1<-plot1 +stat_function(fun=dnorm,args=list( mean=mean(mns), sd=sqrt(varmean)),color = "black", size = 1.0)
print(plot1)
```
 
## stat_bin: binwidth defaulted to range/30. Use 'binwidth = x' to adjust this.
So we see it can compare to a Normal distribution (Black represents the calculated Normal Distribution, and Red represents the theoretical one)
With a bigger number of simulations, let’s say 100000:

# Example for a bigger number
```{r}
set.seed(1)
lambda <- 0.2 # Set lambda as per instructions
nexp <- 40 # number of distributions
nsim <- 100000 # number of simulations
mns <- NULL  # set msn to null 
for (i in 1 : nsim) mns <- c(mns, mean(rexp(40,lambda)))
varxp <- ((1/lambda)^2)/nexp # theoretical variance
varmean <- var(mns) # variance of the means

library(ggplot2)
plotdata <- data.frame(mns)
plot1 <- ggplot(plotdata,aes(x = mns))
plot1 <- plot1 +geom_histogram(aes(y=..density..), colour="black",fill="green")
plot1<-plot1+labs(title="Distribution of Means of rexp", y="Density")
plot1<-plot1 +stat_function(fun=dnorm,args=list( mean=1/lambda, sd=sqrt(varxp)),color = "red", size = 1.0)
plot1<-plot1 +stat_function(fun=dnorm,args=list( mean=mean(mns), sd=sqrt(varmean)),color = "black", size = 1.0)
print(plot1)
```
 
## stat_bin: binwidth defaulted to range/30. Use 'binwidth = x' to adjust this.

