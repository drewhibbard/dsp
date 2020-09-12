[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)

```python
mu = 178
sigma = 7.7
low_cm = ((5*12)+10)*2.54
high_cm = ((6*12) + 1)*2.54
high_cm
```




    185.42000000000002




```python
from scipy import stats
```


```python
low_range = stats.norm.cdf(low_cm,loc=mu,scale=sigma)
```


```python
high_range = stats.norm.cdf(high_cm,loc=mu,scale=sigma)
```


```python
solution = high_range - low_range
solution
```




    0.34274683763147457
