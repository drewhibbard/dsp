[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
%matplotlib inline
sns.set()
```


```python
import nsfg
```


```python
preg = nsfg.ReadFemPreg()
```


```python
live = preg[preg.outcome == 1]
```


```python
firsts_wgt = live[live.birthord==1].totalwgt_lb
others_wgt = live[live.birthord!=1].totalwgt_lb
firsts_prglngth = live[live.birthord==1].prglngth
others_prglngth = live[live.birthord!=1].prglngth
```


```python
print("Mean, Std of firsts (weight): ", (firsts_wgt.mean(),firsts_wgt.std()))
print("Mean, Std of others (weight): ", (others_wgt.mean(),others_wgt.std()))
```

    Mean, Std of firsts (weight):  (7.201094430437772, 1.4205728777207374)
    Mean, Std of others (weight):  (7.325855614973262, 1.3941954762143138)



```python
print("Mean, Std of firsts (preg length): ", (firsts_prglngth.mean(),firsts_prglngth.std()))
print("Mean, Std of others (preg length): ", (others_prglngth.mean(),others_prglngth.std()))
```

    Mean, Std of firsts (preg length):  (38.60095173351461, 2.7919014146686947)
    Mean, Std of others (preg length):  (38.52291446673706, 2.615852350439255)


Percent difference in weight means:


```python
(firsts_wgt.mean() - others_wgt.mean())/others_wgt.mean()
```




    -0.01703025436107311



Percent difference in pregnancy length means:


```python
(firsts_prglngth.mean() - others_prglngth.mean())/others_prglngth.mean()
```




    0.0020257363145493954




```python
import thinkstats2
```


```python
print("Cohen's D of weight, first births v. others: ", 
      thinkstats2.CohenEffectSize(firsts_wgt, others_wgt))
```

    Cohen's D of weight, first births v. others:  -0.088672927072602



```python
print("Cohen's D of pregnancy length, first births v. others: ", 
      thinkstats2.CohenEffectSize(firsts_prglngth, others_prglngth))
```

    Cohen's D of pregnancy length, first births v. others:  0.028879044654449883


There does not appear to be a significant difference in birth weight between first babies and others, nor a significant difference in pregnancy length.  This is indicated by a % difference in means of 1.7% for birth weights and 0.2% for pregnancy length, as well as Cohen's D values of 0.089 and 0.029, respectively
