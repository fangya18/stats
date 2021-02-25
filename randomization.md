Background Stroy:

Last time we emphasized the importance of Randomization because it will provide a balanced measurement for treated and placebo groups, so the treatment is exchangeable.

Today we will introduce 3 common randomization methods for different clinical trial purposes and the R code for implementing them: Simple Randomization, Block Randomization, and Stratified Randomization.

1.Simple Randomization

Decide Treatment group by flip a coin.

Pro: Easy to use

Con: Could lead to unbalanced groups over short time period

Tool: runif
```
t<-sample(0:1,100,replace=TRUE)
table(t)
##t
##  0  1 
## 57 43

trial<- data.frame(
  id=c(1:100),
  r= runif(100,0,1)
)

trial$treat<-ifelse(trial$r>0.5, "treatment", "placebo")
w=table(trial$treat)
w
## 
##   placebo treatment 
##        49        51
```



2. Block Ranomization

Randomize blocks of a specific size, so the treatment size are balanced.

Block of size 2 and 4 (AB,AABB,BA,BABA,ABBA…)

-Tool: psych: block.random

the graph shows the independent variable(drug, block,time) will produce uncorrelated conditions.

```
blockr<-block.random(n=100,c(drug=2))
blockr1<-data.frame(blockr)
table(blockr1$drug)

## 
##  1  2 
## 50 50

pairs.panels(blockr)
```






3. Stratified Randomization

Randomize within specific strata to ensure that we have equal numbers of treated and untreated subjects in each stratum (age, histology)

Tool: blockrand

Note: Strata is done in each site
```
age1 = blockrand(n = 50, id.prefix = "M", block.prefix = "M", stratum = "<=60")
age2 = blockrand(n = 50, id.prefix = "M", block.prefix = "M", stratum = ">60")
random_age = rbind(age1, age2)
table(random_age$treatment)
## 
##  A  B 
## 51 51
a<-xtabs(~random_age$stratum+random_age$treatment)
a
##                   random_age$treatment
## random_age$stratum  A  B
##               <=60 26 26
##               >60  25 25

```


Reference:

77's Havard Catalyst Class

https://www.rpubs.com/mhanauer/464752

https://personality-project.org/revelle/syllabi/205/block.randomization.pdf
