Background Story:

One day, my boss asked me to check if the data has a certain number of events to perform an efficacy analysis. I was curious how did he come up with the number, later I know he must have done the Sample Size Calculation. Today we will go over the basics and R applications for sample size calculation.

Five components of Sample Size:

Sample Size: N

Type I error rate: α- level (2-sided 0.05)

Mean under the null and alternative: μ0 and μa

Variance: σ²

Power: 1-β

We can use any four of these five factors to calculate the fifth one.

Two methods to calculate the sample size:
Hypothesis testing: a specific null and alternative hypothesis
Confidence interval: an estimated interest
Hypothesis testing approach:
State the null and the alternative hypothesis
Specify standard deviation
Decide the power and alpha level
- Power=0.8, Alpha=0.05 for two-sided test 
State the test
R/ SAS program




1. H0: mean=80, Ha: mean1= 70
2. standard deviation =20, d=(80-70)/20
3. Power=0.8 , Alpha=0.05 for two-sided test
 
pwr.t.test(d =0.5 , sig.level =0.05, power =0.8 , type = "one.sample", alternative="two.sided")

#General formula:
pwr.t.test(n=, d = , sig.level =, power =, type = ("one.sample","two.sample", "piared"), alternative=("two.sided", "less", "great"))
    One-sample t test power calculation 

              n = 33.36713
              d = 0.5
      sig.level = 0.05
          power = 0.8
    alternative = two.sided

Advanced Sample Size:
Two Sample T-test
Comparison of proportions

pwr.t.test(d=0.7882 , sig.level =0.05, power =0.8 , type = "two.sample", alternative="two.sided")

     Two-sample t test power calculation 

              n = 26.26343
              d = 0.7882
      sig.level = 0.05
          power = 0.8
    alternative = two.sided

NOTE: n is number in *each* group
Summary of Sample Size variations:

Variance σ² increase, the sample size N increase
Difference between groups increases (μ1-μ2), sample size N decrease
Type I error rate (α) increase, sample size N decrease
Power (1-ß) increases sample size N increase.




Thanks 77 for sharing the Havard Catalyst class material!

Happy Studying!
