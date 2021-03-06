# pykliep
A density ratio estimator package for python using the KLIEP algorithm.

This fork of the original repository is just to make it python 3 compatible.

## Usage

```python
from scipy.stats import norm
from pykliep import DensityRatioEstimator
import matplotlib.pyplot as plt
import numpy as np

def true_density_ratio(x):
    return norm.pdf(x, 1, 1./8) / norm.pdf(x, 1, 1./2)

np.random.seed(0)

x = norm.rvs(size = 1500, loc = 1, scale = 1./8).reshape(-1,1)
y = norm.rvs(size = 1500, loc = 1, scale = 1./2).reshape(-1,1)

# density ration estimation
kliep = DensityRatioEstimator()
# first argument denominator, second numerator
kliep.fit(y, x)

x = np.linspace(-1, 3, 400)
plt.plot(x, true_density_ratio(x), "r-", lw=5, alpha=0.6, label="w(x)")
plt.plot(x, kliep.predict(x.reshape(-1,1)), "k-", lw=2, label="w-hat(x)")
plt.legend(loc="best", frameon=False)
plt.xlabel("x")
plt.ylabel("Density Ratio")
plt.show()

```

The above code snippet makes the plot.

![](https://raw.githubusercontent.com/kaikai581/pykliep/master/plots/KLIEP.png)

There is literature claiming KLIEP is one of the better-performing algorithms [1]. This can be seen by comparing with another python package which uses the uLSIF algorithm:

![](https://raw.githubusercontent.com/kaikai581/pykliep/master/plots/uLSIF.png)

## References

[1] Tongliang Liu, Dacheng Tao, "Classification with Noisy Labels by Importance Reweighting"