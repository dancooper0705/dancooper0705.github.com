---
layout: post
title: "statistics-for-business-and-economics-p11-06"
date:  2019-10-18 14:10:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
The oppenheimer Capital Appreiciation mutual fund provided a 17.6% average
annual return over a five-year period(Fortune, August 18, 1997). Assume that the
following data show the annual returns for each of the five years: 10.8, 34.2,
4.2, 9.4, and 29.4. The standard deviation of the annual returns can be used a
measure of risk, with a larger standard deviation indicating more variation and
therefore more uncertainty in the annual returns. A standard deviation of 18.2%
was reporeted for the 10 aggresive growth mutual funds similar to the
Oppenhemier Capital Appreciation mutal funds.  a. Using the data as a sample of
five annual returns, what is the smaple standard deviation measure of risk for
the Oppenheimer Capital Appreciation mutual fund?  b. What is the 95% confidence
interval for the population standard deviation of annual returns for the
Oppenheimer Capital Appreciation mutal fund?
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
    sample = [10.8, 34.2, 4.2, 9.4, 29.4]
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
sample: [10.8, 34.2, 4.2, 9.4, 29.4]
sample_size: 5
sample_mean: 17.6000
sample_standard_deviation: 13.3026
sample_variance: 176.9600
95% confidence interval for population standard deviation: 7.9700 to 38.2259
95% confidence interval for population variance: 63.5217 to 1461.2157
```
