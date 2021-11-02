## 1.Bernoulli Distribution 
* Assumptions:
  *  Only two outcomes:
      * Coin toss/Roll dice (6 success, else fail)
   * Only one Trail 

* PMF of a random variable x that follows the Bernoulli distribution is:

![image](https://user-images.githubusercontent.com/59746522/139757903-05c13007-3dc4-47de-8d98-6f7c756b936b.gif)

```python

import numpy as np
np.random.choice(['success', 'failure'],size = 10, p = (0.6,0.4))

```

## 2. Binomial Distribution 

It describes the random variable x as the number of success in n Bernoulli trials 

> **Can think of Binomial distribution as the outcome distribution of n identical Bernoulli distributed random variables**

* Assumptions:
  * each trail only has two outcome
  * n identical trails in total 
  * each trail is independent of other trails
  * the p and 1-p are the same for all trails 

* PMF

![image](https://user-images.githubusercontent.com/59746522/139779350-b10c7170-73e0-4ece-9f3a-bdf8fa222d34.gif)

![image](https://user-images.githubusercontent.com/59746522/139775371-632a3be2-72ec-4ba2-b9da-aa744c006557.gif)

```python
n = 100
p = 0.5
size = 1000
binomial = np.random.binomial(n,p,size)![image](https://user-images.githubusercontent.com/59746522/139776519-48426ed8-d240-454f-8a1d-6b4e29073a80.png)
plt.hist(binomial)
# Mean around np = 50
```

## 3. Geometric Distribution 

Model the number of failures before the first success in repeated, independent Berboulli trails.

* Assumptions -> same as Binominal 
* PMF

![image](https://user-images.githubusercontent.com/59746522/139779581-dd75f475-0175-448c-9bd9-ca3c00b452fe.gif)


![image](https://user-images.githubusercontent.com/59746522/139779634-efdc2efb-c23a-4a4c-99b5-4efac40a6496.gif)

## Uniform Distribution

* Depending on the R.V, the distribution can be discrete or continuous
  * n outcomes (discrete)
  * a range of outcomes to be at (continuous)

* All values in the outcome set or the range are equally likely to occur.

```python
# Uniform distribution in range [0,1]
uniform = np.random.uniform(0,1,size = 1000)
plt.hist(uniform)
```

## Normal Distribution 

Continuous distribution - Many r.v are normally distributed b/c of the CLT 
* the PDF is bell-shaped any symmetric at x=u 
* the values between [u-o, u+o] takes roughly 68% of data (o is the standard deviation) 

```python
# If use numpy function 

#np.random.normal(mu,sigma, 1000)

# Use CLT to simulate Normal Distribution
def clt(N,n):
  # generate a sample from any random population N
  lis = np.random.random(size = N)
  means = []

  # take random subsample with size n from N
  for i in range(n):
    lis_index = np.random.randint(0,N,n)
    means.append(lis[lis_index].mean()) # ramdomly pick numbers with size n from population by passing in n index 
    i += 1
  return plt.hist(means)
clt(1000,100)
```

## Poisson Distribution 

Poisson distribution is a distribution that models the probability of a num of evnts occuring in a fixed interval of time or space *eg. num of customers arriving in a store in an hour 

PMF

![image](https://user-images.githubusercontent.com/59746522/139788407-a3f12504-b7db-4f1b-8ce5-809dae866834.gif)



![image](https://user-images.githubusercontent.com/59746522/139788565-dc80a042-0c10-4c8c-9b8c-8431fe16be18.gif)


```python
lam = 5 # expected num of event to occur in a fixed-time interval (n Bernoulli trail)

poi = np.random.poisson(lam = lam, size = 100)
plt.hist(poi)
plt.axvline(x = lam, c = 'red') # lam = mean 
```
