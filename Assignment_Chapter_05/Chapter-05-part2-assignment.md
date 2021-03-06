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
  a ~ dnorm( 10 , 10 ) , 
  ba ~ dnorm( 0 , 1 ) , 
  bg ~ dnorm( 0 , 1 ) , 
  sigma ~ dunif( 0 , 10 )
), 
data=foxes)
precis(m5H2)
plot(precis(m5H2))
mean.group.size <- mean(foxes$groupsize)
np.seq <- 0:100 
pred.data <- data.frame( area=np.seq, groupsize=mean.group.size)
mu <- link( m5H2 , data=pred.data , n=1e4 ) 
mu.mean <- apply( mu , 2 , mean ) 
mu.PI <- apply( mu , 2 , PI )
plot( weight ~ area , data=foxes , type="n" ) 
lines( np.seq , mu.mean ) 
lines( np.seq , mu.PI[1,] , lty=2 ) 
lines( np.seq , mu.PI[2,] , lty=2 )

mean.area <- mean(foxes$area)
np.seq <- 0:100 
pred.data.2 <- data.frame( groupsize=np.seq, area=mean.area)
mu <- link( m5H2 , data=pred.data.2 , n=1e4 ) 
mu.mean <- apply( mu , 2 , mean ) 
mu.PI <- apply( mu , 2 , PI )
plot( weight ~ groupsize , data=foxes , type="n" ) 
lines( np.seq , mu.mean ) 
lines( np.seq , mu.PI[1,] , lty=2 ) 
lines( np.seq , mu.PI[2,] , lty=2 )
```
## 5H3
```
{r}
library(rethinking)
data(foxes)
m5H3 <- map( alist(
  weight ~ dnorm( mu , sigma ) , 
  mu <- a + ba*avgfood + bg*groupsize , 
  a ~ dnorm( 10 , 10 ) , 
  ba ~ dnorm( 0 , 1 ) , 
  bg ~ dnorm( 0 , 1 ) , 
  sigma ~ dunif( 0 , 10 )
), 
data=foxes)
precis(m5H3)
plot(precis(m5H3))

#now with all 3

m5H3 <- map( alist(
  weight ~ dnorm( mu , sigma ) , 
  mu <- a + bf*avgfood + bg*groupsize + ba*area , 
  a ~ dnorm( 10 , 10 ) , 
  ba ~ dnorm( 0 , 1 ) , 
  bg ~ dnorm( 0 , 1 ) , 
  bf ~ dnorm( 0, 1),
  sigma ~ dunif( 0 , 10 )
), 
data=foxes)
precis(m5H3)
plot(precis(m5H3))
```
area is a better predictor since CI does not cross zero.
Average food and area are probably positively correlated, as more area should contain more food. They are correlated, with a r value of 0.88
```
{r}
cor(foxes$avgfood, foxes$area)
plot(foxes$avgfood, foxes$area)
```

#for May 2, 2016


#5E3
b1=slope parameter for funding 
b2=slope parameter for lab size

time ~ dnorm( mu , sigma ) , 
  mu <- a + b1*funding + b2*size  , 
  a ~ dnorm( 6 , 6 ) , 
  b1 ~ dnorm( 0 , 1 ) , 
  b2 ~ dnorm( 0 , 1 ) , 
  sigma ~ dunif( 0 , 10 )
  
IN the multiple regression model, b1 and b2 would both be positive. If either were evaluated in a single regression, there slopes would not be significantly different from zero.


#5E4
1 and 3


#5M5
#here I would expect b1 to be negative
obesity ~ dnorm( mu , sigma ) , 
  mu <- a + b1*gasprice   , 
  a ~ dnorm( 6 , 6 ) , 
  b1 ~ dnorm( 0 , 1 ) , 
  b2 ~ dnorm( 0 , 1 ) , 
  sigma ~ dunif( 0 , 10 )


#here i would expect b1 to be negative  
obesity ~ dnorm( mu , sigma ) , 
  mu <- a + b1*walking   , 
  a ~ dnorm( 6 , 6 ) , 
  b1 ~ dnorm( 0 , 1 ) , 
  b2 ~ dnorm( 0 , 1 ) , 
  sigma ~ dunif( 0 , 10 )

#here i would expect b2 to be positive 
obesity ~ dnorm( mu , sigma ) , 
  mu <- a + b2*restaurant.meals   , 
  a ~ dnorm( 6 , 6 ) , 
  b1 ~ dnorm( 0 , 1 ) , 
  b2 ~ dnorm( 0 , 1 ) , 
  sigma ~ dunif( 0 , 10 )
  
m5.16_alt <- map( alist(
kcal.per.g ~ dnorm( mu , sigma ) , 
mu <- a[clade_id] ,
a[clade_id] ~ dnorm( 0.6 , 10 ) , 
sigma ~ dunif( 0 , 10 )
), data=d )
precis( m5.16_alt )
