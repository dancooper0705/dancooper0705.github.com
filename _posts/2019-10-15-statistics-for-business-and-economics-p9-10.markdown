---
layout: post
title: "statistics-for-business-and-economics-p9-10"
date:  2019-10-15 20:45:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
Consider the following hypothesis test.
H0: population mean <= 15
H1: population mean > 15
A sample of 40 provides a sample mean of 16.5 and sample standard deivation of 7.
a. At alpha=0.02, what is the critical value for z and what is the rejected rule?
b. Compute the value of test statistics z.
c. what is the p-value?
d. what is your conclusion?
```

## source
```python
import math
import scipy.stats

def query_critical_z_score(significance_level):
    tail_area = significance_level
    critical_z_score = scipy.stats.norm.ppf(1 - tail_area)
    return critical_z_score

def query_test_statistics_z_score(hypothesis_mean, sample_size, sample_mean, sample_standard_deviation):
    standard_deviation = sample_standard_deviation / math.sqrt(sample_size)
    z_score = (sample_mean - hypothesis_mean) / standard_deviation
    return z_score

def query_p_value(hypothesis_mean, sample_size, sample_mean, sample_standard_deviation):
    standard_deviation = sample_standard_deviation / math.sqrt(sample_size)
    z_score = (sample_mean - hypothesis_mean) / standard_deviation
    p_value = 1.0 - scipy.stats.norm.cdf(z_score)
    return p_value

def main():
    sample_size = 40
    sample_mean = 16.5
    sample_standard_deviation = 7
    significance_level = 0.02
    hypothesis_mean = 15.0
    critical_z_score = query_critical_z_score(significance_level)
    test_statistics_z_score = query_test_statistics_z_score(hypothesis_mean, sample_size, sample_mean, sample_standard_deviation)
    p_value = query_p_value(hypothesis_mean, sample_size, sample_mean, sample_standard_deviation)
    print('H0: population mean <= ' + '{0:.4}'.format(hypothesis_mean))
    print('H1: population mean > ' + '{0:.4}'.format(hypothesis_mean))
    print('significance_level: ' + '{0:.4f}'.format(significance_level))
    print('reject H0 if z_score > critical_z_score: ' + '{0:.4f}'.format(critical_z_score))
    print('test_statistics_z_score: ' + '{0:.4f}'.format(test_statistics_z_score))
    print('p_value: ' + '{0:.4f}'.format(p_value))
    if test_statistics_z_score > critical_z_score:
        print('reject H0')
    else:
        print('not reject H0')

if __name__ == "__main__":
    main()
```

## output
```
H0: population mean <= 15.0
H1: population mean > 15.0
significance_level: 0.0200
reject H0 if z_score > critical_z_score: 2.0537
test_statistics_z_score: 1.3553
p_value: 0.0877
not reject H0
```
