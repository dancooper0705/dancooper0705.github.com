---
layout: post
title: "statistics-for-business-and-economics-p9-12"
date:  2019-10-16 00:00:00  +0800
categories: [dev]
tags: [python, statistics]
---

## question
```
Consider the following hypothesis test.

H0: population mean <= 5
Ha: population mean > 5

Assume the following test statistics. Compute the corresponding p-values and
make the appropriate conclusion based on alpha = 0.05
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
    return z_score_to_p_value(z_score)

def z_score_to_p_value(z_score):
    p_value = 1.0 - scipy.stats.norm.cdf(z_score)
    return p_value

def main():
    hypothesis_mean = 5.0
    significance_level = 0.05
    print('H0: population mean <= ' + '{0:.4}'.format(hypothesis_mean))
    print('H1: population mean > ' + '{0:.4}'.format(hypothesis_mean))
    print('significance_level: ' + '{0:.4f}'.format(significance_level))

    test_statistics_z_scores = [1.82, 0.45, 1.50, 3.30, -1.00]
    for test_statistics_z_score in test_statistics_z_scores:
        p_value = z_score_to_p_value(test_statistics_z_score)
        print('test_statistics_z_score: ' + '{0:.4f}'.format(test_statistics_z_score))
        print('p_value: ' + '{0:.4f}'.format(p_value))
        if p_value < significance_level:
            print('reject H0')
        else:
            print('not reject H0')
        print()

if __name__ == "__main__":
    main()
```

## output
```
H0: population mean <= 5.0
H1: population mean > 5.0
significance_level: 0.0500
test_statistics_z_score: 1.8200
p_value: 0.0344
reject H0

test_statistics_z_score: 0.4500
p_value: 0.3264
not reject H0

test_statistics_z_score: 1.5000
p_value: 0.0668
not reject H0

test_statistics_z_score: 3.3000
p_value: 0.0005
reject H0

test_statistics_z_score: -1.0000
p_value: 0.8413
not reject H0
```
