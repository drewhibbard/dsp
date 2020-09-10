[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
sns.set()
%matplotlib inline
```


```python
import nsfg
import first
import thinkstats2
import thinkplot
```


```python
resp = nsfg.ReadFemResp()
```

**Exercise:** Something like the class size paradox appears if you survey children and ask how many children are in their family. Families with many children are more likely to appear in your sample, and families with no children have no chance to be in the sample.

Use the NSFG respondent variable `numkdhh` to construct the actual distribution for the number of children under 18 in the respondents' households.

Now compute the biased distribution we would see if we surveyed the children and asked them how many children under 18 (including themselves) are in their household.

Plot the actual and biased distributions, and compute their means.


```python
plt.hist(resp.numkdhh,align='left',bins=range(0,7,1))
```




    (array([3563., 1636., 1500.,  666.,  196.,   82.]),
     array([0, 1, 2, 3, 4, 5, 6]),
     <a list of 6 Patch objects>)




![png](output_4_1.png)



```python
pmf = resp.numkdhh.value_counts().sort_index()/len(resp.numkdhh)
```


```python
pmf.plot(kind='bar')
plt.xlabel('Number of children in family')
plt.ylabel('PMF')
```




    Text(0, 0.5, 'PMF')




![png](output_6_1.png)



```python
plt.step(pmf.index,pmf)
```




    [<matplotlib.lines.Line2D at 0x7fcc0e15cdf0>]




![png](output_7_1.png)



```python
pmf = thinkstats2.Pmf(resp.numkdhh,label='Actual')
```


```python
def BiasPmf(pmf, label):
    new_pmf = pmf.Copy(label=label)

    for x, p in pmf.Items():
        new_pmf.Mult(x, x)
        
    new_pmf.Normalize()
    return new_pmf
```


```python
biased_pmf = BiasPmf(pmf,label='biased by asking children')
```


```python
thinkplot.PrePlot(2,cols=2)
thinkplot.Hist(pmf,align='right',width=0.5,label='actual')
thinkplot.Hist(biased_pmf,align='left',width=0.5,label='biased')
plt.xlabel('Number of children in family')
plt.ylabel('PMF')
plt.legend()

thinkplot.PrePlot(2)
thinkplot.SubPlot(2)
thinkplot.Pmfs([pmf, biased_pmf])
plt.xlabel('Number of children in family')
plt.ylabel('PMF')
plt.legend()
```




    <matplotlib.legend.Legend at 0x7fcc0e1cceb0>




![png](output_11_1.png)


Mean and standard deviation of actual responses v. biased results if we had surveyed children.


```python
print('Actual response mean: ', pmf.Mean(), pmf.Std())
print('Biased mean: ', biased_pmf.Mean(), biased_pmf.Std())
```

    Actual response mean:  1.024205155043831 1.1886396957670224
    Biased mean:  2.403679100664282 1.083176857907326



```python
#without using author's built-in functions
print(resp.numkdhh.mean(),resp.numkdhh.std())
```

    1.024205155043831 1.1887174634203603


Summary: As we can see, the biased version that would result from giving children the same survey is significantly different from the actual result of the NSFG survey.  Naturally, we see a bias towards higher numbers of children in the family due to the size effect, and zero families with zero children.
