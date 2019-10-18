---
layout: post
title: "statistics-for-business-and-economics-p11-04"
date:  2019-10-18 14:00:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
The variance in drug weights is critical in the pharmaceutical industry. For a
specific drug with weights measured in grams, a sample of 18 units provided a
sample variance of s^2 = 0.36.
a. Construct a 90% confidence interval esitmate of the population variance for
the weights of this drug.
b. Construct a 90% confidence interval estimate of the population standard
deviation.
```

## source
```python
import math
import scipy.stats
import numpy as np

def confidence_interval_populatoin_variance(sample_size, sample_variance, confidence_level):
    df = sample_size - 1
    confidence_coefficient = confidence_level / 100
    alpha_level = 1 - confidence_coefficient
    return [(sample_size - 1) * sample_variance / scipy.stats.chi2.ppf(1 - alpha_level / 2, df),
            (sample_size - 1) * sample_variance / scipy.stats.chi2.ppf(alpha_level / 2, df)];

def main():
    sample_size = 18
    sample_variance = 0.36

    confidence_level = 90
    confidence_interval = confidence_interval_populatoin_variance(sample_size, sample_variance, confidence_level)
    print(str(confidence_level) + '% confidence interval for population variance: ' + ' to '.join('{0:.4f}'.format(a) for a in confidence_interval))

    confidence_interval_population_standard_deviation = [math.sqrt(a) for a in confidence_interval]
    print(str(confidence_level) + '% confidence interval for population standard deviation: ' + ' to '.join('{0:.4f}'.format(a) for a in confidence_interval_population_standard_deviation))

if __name__ == "__main__":
    main()
```

## output
```
90% confidence interval for population variance: 0.2218 to 0.7057
90% confidence interval for population standard deviation: 0.4710 to 0.8401
```
