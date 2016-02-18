#R club homework due 2/11/16 and 2/18/16—Sharon Gray
##2E1: 
(2)
##2E2: 
(2)
##2E3: 
(1)
##2E4: 
This statement means that, on any given toss, the probability of observing water is 0.7.
One could make the argument that it doesn't have an objective reality because it's inference
space is the toss that is occurring at that moment.

##2M1:
I attempted to do this problem starting with R code 2.3, but I don’t understand how to incorporate these observations into the computation of the posterior 

##2M2:
The code would be same as above, but rather than this line of code
prior <- rep(1, 20)
being used to specify a flat prior, this line of code
prior <- ifelse(p_grid <0.5, 0, 1)
would be used to specify a prior that has a 0 probability of success in the first half of the trials and a probability of 1 of success in the second half of the trials.


##2M3:
Pr(p|w)=Pr(w|p)*Pr(p)/Pr(w)
Pr(Earth|land)=Pr(land|earth)*Pr(earth)/Pr(land)
Pr(Earth|land)=0.3*0.5/0.65
Pr(Earth|land)=0.23

##2M4:
card 1: black & black
card 2: black & white
card 3: white & white

outcome: black side is facing up
card 1: 2 ways to produce the outcome; plausability = 2/3=0.66
card 2: 1 way to produce the outcome; plausability = 1/3=0.33
card 3: 0 ways to produce the outcome; plausability = 0/3=0.00

Plausability of [card with 2 black sides] after seeing one black side = 
number of ways that [card with 2 black sides] can produce the one black side outcome
*
prior plausability of [card with 2 black sides]

Plausability of [card with 2 black sides] after seeing one black side = 2 * 1/3 = 2/3

##2M5:
card 1: black & black
card 2: black & white
card 3: white & white
card 4: black & black

outcome: black side is facing up
card 1: 2 ways to produce the outcome; 
card 2: 1 way to produce the outcome; 
card 3: 0 ways to produce the outcome; 
card 4: 2 ways to produce the outcome; 

Plausability of [card with 2 black sides] after seeing one black side = 
number of ways that [card with 2 black sides] can produce the one black side outcome
*
prior plausability of [card with 2 black sides]

Plausability of [card with 2 black sides] after seeing one black side = 2 * 2/4 = 1

##2M6:
on paper.

##2M7: 
on paper.

##2H1: 
0.167

##2H2:
Plausability of [species A] after seeing twins = 
number of ways that [species A] can produce twins outcome
*
prior plausability of [species A]

 = 1/10 * 0.5 = 0.05 or 1/20

##2H3:
I don’t know how to do this.

##2H4:
I don’t know how to do this.
