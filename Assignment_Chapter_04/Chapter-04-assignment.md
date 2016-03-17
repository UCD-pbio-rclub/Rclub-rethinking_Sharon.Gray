# Statistical Rethinking Chapter 4 problems

__Name:_Sharon Gray_


# For 03/17/16

## 4E1
The first line is the likelihood. yi~Normal(mu, sigma)

## 4E2
The posterior distribution includes 2 parameters: the mean (mu) and the standard deviation (sigma).

## 4E3
Pr(mu, sigma | y)= Normal(yi|mu, sigma)Normal(mu|0,10)Uniform(sigma|0,10)/
(integral(Normal(hi|mu, sigma)Normal(mu|0,10)Uniform(sigma|0,10)))d(mu)d(sigma)

## 4M1

```r
library(rethinking)
```

```
## Loading required package: rstan
```

```
## Warning: package 'rstan' was built under R version 3.2.3
```

```
## Loading required package: ggplot2
```

```
## Warning: package 'ggplot2' was built under R version 3.2.3
```

```
## rstan (Version 2.9.0, packaged: 2016-01-05 16:17:47 UTC, GitRev: 05c3d0058b6a)
## For execution on a local, multicore CPU with excess RAM we recommend calling
## rstan_options(auto_write = TRUE)
## options(mc.cores = parallel::detectCores())
## Loading required package: parallel
## rethinking (Version 1.58)
```

```r
sample_mu <- rnorm( 1e4 , 0 , 10 ) 
sample_sigma <- runif( 1e4 , 0 , 10 ) 
prior_h <- rnorm( 1e4 , sample_mu , sample_sigma ) 
dens( prior_h )
```

![](Chapter-04-assignment_files/figure-html/unnamed-chunk-1-1.png) 

```r
prior_h <- as.data.frame(prior_h)
```
## 4M2

```r
library(rethinking)
data(Howell1)
d <- Howell1
d2 <- d[ d$age >= 18 , ]
flist <- alist(
  height ~ dnorm( mu , sigma ) , 
  mu ~ dnorm( 0 , 10 ) , 
  sigma ~ dunif( 0 , 10 )
)
m4.1 <- map( flist , data=d2 )
precis( m4.1 )
```

```
##         Mean StdDev   5.5%  94.5%
## mu    154.33   0.41 153.68 154.99
## sigma   7.74   0.29   7.27   8.20
```
# For 03/24/16

## 4E4

## 4E5

## 4M3

## 4M4

## 4M5

## 4M6

# For 03/31/16

## 4H1

## 4H2

## 4H3
