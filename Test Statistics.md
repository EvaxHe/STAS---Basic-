Tow way to reject a Null Hypothesis:
1. p-value < significance level 
2. test statistic > critical value (calculate based on significance level alpha) 

![image](https://user-images.githubusercontent.com/59746522/140372656-f6048fe2-e515-496d-9f75-0689c479316a.png)

* ### Z-test
![image](https://user-images.githubusercontent.com/59746522/140376848-4db9b8a1-7333-465d-82ae-bf34d61b6473.png)

```python

ztest ,pval1 = stests.ztest(df['bp_before'], x2=df['bp_after'], value=0,alternative='two-sided')
print(float(pval1))
if pval<0.05:
    print("reject null hypothesis")
else:
    print("accept null hypothesis")    
```
* ### F-test (on diff class of one variable)

The t-test works well when dealing with two groups, but sometimes we want to compare more than two groups at the same time. For example, if we wanted to test whether voter age differs based on some categorical variable like race, we have to compare the means of each level or group the variable. We could carry out a separate t-test for each pair of groups, but when you conduct many tests you increase the chances of false positives. 

**F = Between group variability / Within group variability**

* ### Chi-square (on diff categorical variables) 

For example, in an election survey, voters might be classified by gender (male or female) and voting preference (Democrat, Republican, or Independent). We could use a chi-square test for independence to determine whether gender is related to voting preference

```python

df_chi = pd.read_csv('chi-test.csv')
contingency_table=pd.crosstab(df_chi["Gender"],df_chi["Shopping?"])
print('contingency_table :-\n',contingency_table)
#Observed Values
Observed_Values = contingency_table.values 
print("Observed Values :-\n",Observed_Values)
b=stats.chi2_contingency(contingency_table)
Expected_Values = b[3]
print("Expected Values :-\n",Expected_Values)
no_of_rows=len(contingency_table.iloc[0:2,0])
no_of_columns=len(contingency_table.iloc[0,0:2])
ddof=(no_of_rows-1)*(no_of_columns-1)
print("Degree of Freedom:-",ddof)
alpha = 0.05
from scipy.stats import chi2
chi_square=sum([(o-e)**2./e for o,e in zip(Observed_Values,Expected_Values)])
chi_square_statistic=chi_square[0]+chi_square[1]
print("chi-square statistic:-",chi_square_statistic)
critical_value=chi2.ppf(q=1-alpha,df=ddof)
print('critical_value:',critical_value)
#p-value
p_value=1-chi2.cdf(x=chi_square_statistic,df=ddof)
print('p-value:',p_value)
print('Significance level: ',alpha)
print('Degree of Freedom: ',ddof)
print('chi-square statistic:',chi_square_statistic)
print('critical_value:',critical_value)
print('p-value:',p_value)
if chi_square_statistic>=critical_value:
    print("Reject H0,There is a relationship between 2 categorical variables")
else:
    print("Retain H0,There is no relationship between 2 categorical variables")
    
if p_value<=alpha:
    print("Reject H0,There is a relationship between 2 categorical variables")
else:
    print("Retain H0,There is no relationship between 2 categorical variables")
```

## one-tailed vs. two-tailed test 

Given p and t values from a two-tailed test, you would reject the null hypothesis of a greater-than test when p/2 < alpha and t > 0, and of a less-than test when p/2 < alpha and t < 0.

## one-sample vs. Two sampled 
1. The One Sample t Test determines whether the sample mean is statistically different from a known or hypothesised population mean

    Example :- you have 10 ages and you are checking whether avg age is 30 or not. 
    
    ```python 
    from scipy.stats import ttest_1samp
    import numpy as np
    ages = np.genfromtxt(“ages.csv”)
    print(ages)
    ages_mean = np.mean(ages)
    print(ages_mean)
    tset, pval = ttest_1samp(ages, 30)
    print(“p-values”,pval)
    if pval < 0.05:    # alpha value is 0.05 or 5%
       print(" we are rejecting null hypothesis")
    else:
      print("we are accepting null hypothesis")
      ```
 2. Two sampled T-test :-The Independent Samples t Test or 2-sample t-test compares the means of two independent groups in order to determine whether there is statistical evidence that the associated population means are significantly different. 

```python
ttest,pval = ttest_ind(week1,week2)
print("p-value",pval)
if pval <0.05:
  print("we reject null hypothesis")
```

## Probability Density Function (PDF) vs Cumulative Distribution Function (CDF)
The CDF is the probability that random variable values less than or equal to x whereas the PDF is a probability that a random variable, say X, will take a value exactly equal to x.

![image](https://user-images.githubusercontent.com/59746522/140399207-ac8fba7d-02c4-48c5-86c3-22131c005ee2.jpeg)



[reference](https://towardsdatascience.com/hypothesis-testing-in-machine-learning-using-python-a0dc89e169ce)
 
 
