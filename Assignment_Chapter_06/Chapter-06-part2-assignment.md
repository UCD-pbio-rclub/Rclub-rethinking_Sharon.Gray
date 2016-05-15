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


# For 05/16/2016

## 6M1: Write down and compare the definitions of AIC, DIC, and WAIC. Which is most general? Which assumptions are required to transform a more general criterion into a less general one?

AIC is the deviance of the training set + 2*the number of free parameters estimated in the model
DIC is the average of the posterior distribution of deviance + expected difference between deviance in sample and deviance out of sample
WAIC is equal to -2*(log-pointwise-predictive-density - effective number of parameters)

AIC is reliable only when the priors are flat. However, flat priors are not usually the most informative, so DIC and WAIC may be better. DIC is similar to AIC, except that it is "aware of informative priors". WAIC, a point-wise estimate of deviance, is often more accurate than DIC, and does not require the assumption of a gaussian posterior.

## 6M5: Provide an informal explanation of why informative priors reduce overfitting.

Using a very narrow prior on the slope (beta) trains the model to be very skeptical of values that are outside of the narrow range that you define as probable. This means that extreme values (above or below 2 SD) will only be assigned a very low plausability, and these extreme values therefore won't have a strong influence on model predictions.


## 6M6: Provide an information explanation of why overly informative priors result in underfitting.

The training deviance always gets worse with tighter priors. This happens because a really narrow prior keeps the model from learning from the test data, as 'extreme' values are assigned a low probability. The best way around this is to split data into training and testing subsets, and testing multiple priors, and selecting the one that gives the smallest test deviance.
 
## 6J1--explain how code block 6.16 works 
This code measures log-likelihood of each observation at each sample from the posterior
line 1: set n_samples variable equal to 1000.
line 2: to calculate log-likelihood, apply the function to 1-1000 datapoints
line 3: the functions to calculate mu (from the posterior estimate of alpha + beta * speed)
line 4: gives the density distribution for car$dist variable, with mean mu, and standard deviation sigma from the map function; provides p values as log-transformed p-values.
