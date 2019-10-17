---
layout: post
title: "statistics-for-business-and-economics-p9-24"
date:  2019-10-16 12:30:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
Consider the following hypothesis test.
h0: u = 5
ha: u != 5
Assume the following test statistics. Compute the corresponding p-values and
specify your conclusions based on alpha = 0.05.
a. z = 1.80
b. z = -0.45
c. z = 2.05
d. z = -3.50
e. z = -1.00
```

## source
```python
import math
import scipy.stats

def query_upper_tailed_critical_z_score(significance):
    tail_area = significance
    critical_z_score = scipy.stats.norm.ppf(1 - tail_area)
    return critical_z_score

def query_lower_tailed_critical_z_score(significance):
    tail_area = significance
    critical_z_score = scipy.stats.norm.ppf(tail_area)
    return critical_z_score

def query_two_tailed_critical_z_score(significance):
    tail_area = significance / 2
    critical_z_score = scipy.stats.norm.ppf(1 - tail_area)
    return critical_z_score

def query_test_statistics_z_score(hypothesis_mean, sample_size, sample_mean, sample_standard_deviation):
    standard_deviation = sample_standard_deviation / math.sqrt(sample_size)
    z_score = (sample_mean - hypothesis_mean) / standard_deviation
    return z_score

def query_upper_tailed_p_value(z_score):
    p_value = scipy.stats.norm.cdf(-z_score)
    return p_value

def query_lower_tailed_p_value(z_score):
    p_value = scipy.stats.norm.cdf(z_score)
    return p_value

def query_two_tailed_p_value(z_score):
    p_value = 2.0 * scipy.stats.norm.cdf(-abs(z_score))
    return p_value

def main():
    hypothesis_mean = 5.0
    significance = 0.05
    print('H0: population mean = ' + '{0:.4}'.format(hypothesis_mean))
    print('Ha: population mean != ' + '{0:.4}'.format(hypothesis_mean))
    print('significance: ' + '{0:.4f}'.format(significance))

    test_statistics_z_scores = [1.80, -0.45, 2.05, -3.50, -1.00]
    for test_statistics_z_score in test_statistics_z_scores:
        p_value = query_two_tailed_p_value(test_statistics_z_score)
        print('test_statistics_z_score: ' + '{0:.4f}'.format(test_statistics_z_score))
        print('p_value: ' + '{0:.4f}'.format(p_value))

if __name__ == "__main__":
    main()
```

## output
```
H0: population mean = 5.0
Ha: population mean != 5.0
significance: 0.0500
test_statistics_z_score: 1.8000
p_value: 0.0719
test_statistics_z_score: -0.4500
p_value: 0.6527
test_statistics_z_score: 2.0500
p_value: 0.0404
test_statistics_z_score: -3.5000
p_value: 0.0005
test_statistics_z_score: -1.0000
p_value: 0.3173
```
