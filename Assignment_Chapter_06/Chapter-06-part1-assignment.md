# Statistical Rethinking Chapter 6 problems

__Name:__Sharon Gray


# For 05/09/2016

## 6E1


(1) The variable for measuring uncertainty/entropy should not be a discrete variable, but should instead be continuous; (2) The more possible outcomes there are, the greater the value of the entropy or uncertainty value; (3) The uncertainty for multiple combinations of individual outcomes should be the sum of uncertainties for individual outcomes.


## 6E2



```r
p <- c(0.7, 0.3) 
-sum( p*log(p) )
```

```
## [1] 0.6108643
```


## 6E3



```r
p <- c(0.2, 0.25, 0.25, 0.30) 
-sum( p*log(p) )
```

```
## [1] 1.376227
```


## 6E4



```r
p <- c(0.33, 0.33, 0.33) 
-sum( p*log(p) )
```

```
## [1] 1.097576
```


    
