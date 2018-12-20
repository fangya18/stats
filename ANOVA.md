

#### Data Science Day 21:

Last time we showed an example of using the independent T-test to compare the Age mean value between players in Real Madrid and Barcelona. What statistical method should we use if we want to **compare the age mean among the players in Barcelona, Real Madrid, and Juventus**?

![image](http://upload-images.jianshu.io/upload_images/8699364-448e86f8b6327ee8.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

 [kappilrinesh](https://pixabay.com/users/kappilrinesh/) / Pixabay![image](http://upload-images.jianshu.io/upload_images/8699364-6ffb5f8886104395.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

 [RonnyK](https://pixabay.com/users/RonnyK/) / Pixabay![image](http://upload-images.jianshu.io/upload_images/8699364-67a8ed3f268a93f2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

 [RonnyK](https://pixabay.com/users/RonnyK/) / Pixabay[/caption]

#### Answer: 

We will use **ANOVA**( analysis of variance) Test, a case of GLM(Generalized Linear Model), for **comparing the means between more than 2 groups**.

**Null Hypothesis: Mean(A) = Mean(B) = Mean(C)**

#### ANOVA Assumptions:

*   **Normality** of the dependent variable
*   **Homogeneity** of Variance
*   **Independent** of observations

#### **Example: Kaggle FIFA 2018 dataset**

**Null Hypothesis:** There is **NO** significance in the mean of players' age among Real Madrid, Barcelona, and Juventus.

**H0:  Age.mean(Real Madrid) = Age.mean(Barcelona) = Age.mean(Juventus)**

1.  #### Dataset 

    We choose the variable Age and Club (Real Madrid, Barcelona, and Juventus).

    ![image](http://upload-images.jianshu.io/upload_images/8699364-c61fdf045c6f123b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

<pre class="EnlighterJSRAW" data-enlighter-language="python">data2=data1.loc[data1["club"].isin(["Real Madrid CF", "FC Barcelona","Juventus"])]</pre>

####      2.Histogram Plot

![image](http://upload-images.jianshu.io/upload_images/8699364-f8a604cc2e241579.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```python
plt.hist(data3.age, bins="auto", color="c" ,edgecolor="k",alpha=0.5)
plt.hist(data4.age, bins="auto", color="r",edgecolor="k", alpha=0.5)
plt.hist(data5.age, bins="auto", color="y",edgecolor="k", alpha=0.5)
plt.xlabel('Age')
plt.ylabel('Frequency')
plt.title('Age Dist in Barcelona vs MFC vs Juventus')

plt.show()
```

####       3\. KDE Density Plot

![image](http://upload-images.jianshu.io/upload_images/8699364-9ecb5fb2314c1533.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
#kde
df=pd.DataFrame({"mfc": data3.age, "barcelona":data4.age,
                "juventus": data5.age ,})
ax=df.plot.kde()
plt.title("Density Plot for Players' Age in Barcelona vs MFC vs Juventus")
plt.show()
```

####       4\. ANOVA Test 

```
stats.f_oneway(data3.age, data4.age, data5.age)
F_onewayResult(statistic=4.8827728579356524, pvalue=0.010152460067260918)
```

#### **Outcome:**

F-statistics 4.88 and **P-value= 0.01** which is indicating **there is an overall significance of the players' mean age among MFC, Barcelona, and Juventus**. Both Histogram and Density plots supported the outcome.  However, we don't know where the difference lies between the groups, we can use the Bonferroni Method for further investigation.

#### **Bonus:**

I remember Song asked me, it is good to know what ANOVA is used for, but do you know which **test generates the P-value of ANOVA**?

I thought since ANOVA has similar application as T-test, so the t.test generates P-value.
However, the truth is **F-test generates the ANOVA's P-value.**

Later, little rain mentioned T-test and F-test is convertible with the relation **T^{2}= F**.
We will go over the relationship between T-test and F-test next time!

**Happy Studying and Soccer game watching!** ⚽
