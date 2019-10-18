---
layout: post
title: "statistics-for-business-and-economics-p11-08"
date:  2019-10-18 14:50:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
A sample of eight earnings per share estimates for 1998 is shown below(Barron's,
December 8, 1997)
```

Company | Estimated Earnings Per Share
--- | ---
AT&T | 2.92
Catepillar | 4.65
Eastman Kodak | 4.27
Exxon | 3.09
Hewlet-Packard | 3.57
IBM | 7.04
McDonald's | 2.64
Wal-Mart | 1.74

```
a. Compute the sample variance and sample stndard deviation for the data.
b. What is the 95% confidence interval for the population variance?
c. What is the 95% confidence interval for the population standard deviation?
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
    sample = [2.92, 4.65, 4.27, 3.09, 3.57, 7.04, 2.64, 1.74]
    sample_size = len(sample)
    sample_mean = np.mean(sample)
    sample_standard_deviation = np.std(sample, ddof=1)
    sample_variance = np.var(sample, ddof=1)

    print('sample: ' + str(sample))
    print('sample_size: ' + str(sample_size))
    print('sample_mean: ' + '{0:.4f}'.format(sample_mean))
    print('sample_standard_deviation: ' + '{0:.4f}'.format(sample_standard_deviation))
    print('sample_variance: ' + '{0:.4f}'.format(sample_variance))

    confidence_level = 95
    confidence_interval = confidence_interval_populatoin_variance(sample_size, sample_variance, confidence_level)
    confidence_interval_population_standard_deviation = [math.sqrt(a) for a in confidence_interval]
    print(str(confidence_level) + '% confidence interval for population standard deviation: ' + ' to '.join('{0:.4f}'.format(a) for a in confidence_interval_population_standard_deviation))
    print(str(confidence_level) + '% confidence interval for population variance: ' + ' to '.join('{0:.4f}'.format(a) for a in confidence_interval))

if __name__ == "__main__":
    main()
```

## output
```
sample: [2.92, 4.65, 4.27, 3.09, 3.57, 7.04, 2.64, 1.74]
sample_size: 8
sample_mean: 3.7400
sample_standard_deviation: 1.6183
sample_variance: 2.6190
95% confidence interval for population standard deviation: 1.0700 to 3.2937
95% confidence interval for population variance: 1.1449 to 10.8487
```
