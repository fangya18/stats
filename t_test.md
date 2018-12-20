#### Data Science Day 20:

When we are watching Soccer games, at the beginning of the match, the screen will show the basic info for each team. Suppose we want to know **is there any difference between the average age between Real Madrid and Barcelona pl****ayers,** What statistical test should we use?

![image](http://upload-images.jianshu.io/upload_images/8699364-f8129e542c34ea84.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

 [RonnyK](https://pixabay.com/users/RonnyK/) / Pixabay![image](http://upload-images.jianshu.io/upload_images/8699364-2324a650eb171ea6.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

 [kappilrinesh](https://pixabay.com/users/kappilrinesh/) / Pixabay[/caption]

**Answer:**

We can use **T-test** to determine **whether there is a significant difference between the means of two groups**.

**T-test assumptions:**
*   The dependent variable is **Normally distributed**
    *Note, identify the probability of a particular outcome*
*   **Independent observations**
*   The dependent variable is **Continuous**.  
*   **No outliers**

### **Example: Kaggle FIFA 2018 dataset**

**Null Hypothesis H0:** There is NO significant difference between the age of  Real Madrid and Barcelona's players.

1.  We choose the variable Age and Club (Real Madrid, Barcelona).
    ![image](http://upload-images.jianshu.io/upload_images/8699364-3ce91dc70ad39aab.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


 # import packages
    import numpy as np
    from scipy import stats
    import pandas as pd
    import matplotlib.pyplot as plt
    import statistics as st
    import seaborn as sns

    data1= data[["club","age"]]
    data2=data1.loc[data1["club"].isin(["Real Madrid CF", "FC Barcelona"])
    

2.  #### **Histogram Graph for Age **

![image](http://upload-images.jianshu.io/upload_images/8699364-4dd8739238d186fb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

``` python
data3=data1.loc[data1["club"].isin(["Real Madrid CF"])]
data4=data1.loc[data1["club"].isin(["FC Barcelona"])]

plt.hist(data3.age, bins="auto", color="c" ,edgecolor="k",alpha=0.5)
plt.hist(data4.age, bins="auto", color="r", alpha=0.5)
plt.xlabel('Age')
plt.ylabel('Frequency')
plt.title('Age Distribution in Barcelona vs MFC')

plt.show()
```

#### 3**. Density Plot of Age**

![image](http://upload-images.jianshu.io/upload_images/8699364-63240c5647f038ac.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```python
#kde plot
df=pd.DataFrame({"mfc": data3.age, "barcelona":data4.age,})
ax=df.plot.kde()
plt.title("Density Plot for Players' Age in Barcelona vs MFC")
plt.show()
```

####       ** 4\. Statistical T-test **

```python
stats.ttest_ind(data3.age,data4.age, equal_var=False)
Ttest_indResult(statistic=-1.9061510499479299, pvalue=0.062416380021536121)
```

#### **Conclusion:**

Although the Histogram graph does not show a normal distribution, the Density Plot represents some feature of the Normality for Age Distribution. Since the P-value= 0.06, we will **Accept the Null** Hypothesis: 
There is **No significant difference in players age** between Real Madrid and Barcelona. 

#### **Additional Info:**

We used Non-direction (two sided) Ttest to generate the results,  but one question we can ask ourselves is how sure are we about the results?

1.  **Type 1 error, Reject a null hypothesis that is True**
    Predict there is a difference while in reality there's no.
    p=0.05,  there is  a 5% chance we are making type 1 error
2.  **Type 2 error, Accept a null hypothesis that is false**
    Predict there  is no difference when the reality has one

In the previous example, we have a 2-level independent variable Club (Barcelona, Real Madrid), and one dependent variable age.

What if we have an independent variable more than 2 levels?
AC Milan, Barcelona, and Real Madrid ? 

That will be **ANOVA's** show!

#### **Happy Studying!** 🍉
