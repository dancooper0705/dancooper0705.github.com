---
layout: post
title: "statistics-for-business-and-economics-p11-02"
date:  2019-10-18 13:00:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
A sample of 20 items provides a sample stnadard deviation of 5.
a. Compute the 90% confidence interval estimate of the population variance.
b. Compute the 95% confidence interval estimate of the population variance.
c. Compute the 95% confidence interval estimate of the population standard
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
    sample_size = 20
    sample_standard_deviation = 5
    sample_variance = sample_standard_deviation ** 2

    confidence_level = 90
    confidence_interval = confidence_interval_populatoin_variance(sample_size, sample_variance, confidence_level)
    print(str(confidence_level) + '% confidence interval for population variance: ' + ' to '.join('{0:.4f}'.format(a) for a in confidence_interval))

    confidence_level = 95
    confidence_interval = confidence_interval_populatoin_variance(sample_size, sample_variance, confidence_level)
    print(str(confidence_level) + '% confidence interval for population variance: ' + ' to '.join('{0:.4f}'.format(a) for a in confidence_interval))

    confidence_interval_population_standard_deviation = [math.sqrt(a) for a in confidence_interval]
    print(str(confidence_level) + '% confidence interval for population standard deviation: ' + ' to '.join('{0:.4f}'.format(a) for a in confidence_interval_population_standard_deviation))

if __name__ == "__main__":
    main()
```

## output
```
90% confidence interval for population variance: 15.7579 to 46.9506
95% confidence interval for population variance: 14.4586 to 53.3317
95% confidence interval for population standard deviation: 3.8025 to 7.3029
```
