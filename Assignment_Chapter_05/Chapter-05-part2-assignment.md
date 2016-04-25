# Chapter-05-part2-assignment
# Statistical Rethinking Chapter 4 problems

__Name:__Sharon Gray


# For 04/18/2016 (4/25/2016)

## 5M2
Plant biomass is affected positively by elevated atmospheric CO2 concentrations and is affected negatively by elevated atmospheric ozone concentrations. In terms of analyzing historical datasets, these two could be correlated, as urbanization increases both pollutants in the atmosphere. 


## 5H1
```
{r}
library(rethinking)
data(foxes)
#body weight as a linear function of territory size
m5H1A <- map( alist(
weight ~ dnorm( mu , sigma ) , 
mu <- a + b*area , 
a ~ dnorm( 0.6 , 10 ) , 
b ~ dnorm( 0 , 1 ) , 
sigma ~ dunif( 0 , 10 )
),
data=foxes)
precis( m5H1A)
#plot pred mean + interval
np.seq <- 0:100 
pred.data <- data.frame( area=np.seq )
mu <- link( m5H1A , data=pred.data , n=1e4 ) 
mu.mean <- apply( mu , 2 , mean ) 
mu.PI <- apply( mu , 2 , PI )
plot( weight ~ area , data=foxes , col=rangi2 ) 
lines( np.seq , mu.mean ) 
lines( np.seq , mu.PI[1,] , lty=2 ) 
lines( np.seq , mu.PI[2,] , lty=2 )

#body weight as a linear function of group size
m5H1B <- map( alist(
weight ~ dnorm( mu , sigma ) , 
mu <- a + b*groupsize , 
a ~ dnorm( 0.6 , 10 ) , 
b ~ dnorm( 0 , 1 ) , 
sigma ~ dunif( 0 , 10 )
),
data=foxes)
precis( m5H1B)
#plot pred mean + interval
np.seq <- 0:100 
pred.data <- data.frame( groupsize=np.seq )
mu <- link( m5H1B , data=pred.data , n=1e4 ) 
mu.mean <- apply( mu , 2 , mean ) 
mu.PI <- apply( mu , 2 , PI )
plot( weight ~ groupsize , data=foxes , col=rangi2 ) 
lines( np.seq , mu.mean ) 
lines( np.seq , mu.PI[1,] , lty=2 ) 
lines( np.seq , mu.PI[2,] , lty=2 )
```
Neither of these variables has a strong correlation with fox body weight.

## 5H2
```
{r}
library(rethinking)
data(foxes)
m5H2 <- map( alist(
  weight ~ dnorm( mu , sigma ) , 
  mu <- a + ba*area + bg*groupsize , 
  a ~ dnorm( 5 , 1 ) , 
  ba ~ dnorm( 0 , 1 ) , 
  bg ~ dnorm( 0 , 1 ) , 
  sigma ~ dunif( 0 , 1 )
), 
data=foxes)
precis(m5H2)

mean.group.size <- mean(groupsize)
np.seq <- 0:100 
pred.data <- data.frame( weight=np.seq, groupsize=mean.group.size)
mu <- link( m5H2 , data=pred.data , n=1e4 ) 
mu.mean <- apply( mu , 2 , mean ) 
mu.PI <- apply( mu , 2 , PI )
plot( weight ~ area , data=foxes , type="n" ) 
lines( np.seq , mu.mean ) 
lines( np.seq , mu.PI[1,] , lty=2 ) 
lines( np.seq , mu.PI[2,] , lty=2 )

mean.area <- mean(area)
np.seq <- 0:100 
pred.data <- data.frame( weight=np.seq, area=mean.area)
mu <- link( m5H2 , data=pred.data , n=1e4 ) 
mu.mean <- apply( mu , 2 , mean ) 
mu.PI <- apply( mu , 2 , PI )
plot( weight ~ groupsize , data=foxes , type="n" ) 
lines( np.seq , mu.mean ) 
lines( np.seq , mu.PI[1,] , lty=2 ) 
lines( np.seq , mu.PI[2,] , lty=2 )
## 5H3
