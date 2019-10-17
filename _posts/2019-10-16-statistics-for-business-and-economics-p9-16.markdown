---
layout: post
title: "statistics-for-business-and-economics-p9-16"
date:  2019-10-16 10:00:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
Fightmaster and Associates Real Estate, Inc., advertises that the mean selling
time of a residential home is 40 days or less. A sample of 50 recently wold
residential homes shows a sample mean selling time of 45 days and a sample
standard deviation of 20 days. Using a .02 level of sigificance, test the
validility of the company's cliam.
```

## source
```python
import math
import scipy.stats

def query_upper_tailed_critical_z_score(significance):
    tail_area = significance
    critical_z_score = scipy.stats.norm.ppf(1 - tail_area)
    return critical_z_score

def query_test_statistics_z_score(hypothesis_mean, sample_size, sample_mean, sample_standard_deviation):
    standard_deviation = sample_standard_deviation / math.sqrt(sample_size)
    z_score = (sample_mean - hypothesis_mean) / standard_deviation
    return z_score

def query_upper_tailed_p_value(z_score):
    p_value = scipy.stats.norm.cdf(-z_score)
    return p_value

def main():
    hypothesis_mean = 40.0
    sample_size = 50
    sample_mean = 45.0
    sample_standard_deviation = 20.0
    significance = 0.02
    critical_z_score = query_upper_tailed_critical_z_score(significance)
    test_statistics_z_score = query_test_statistics_z_score(hypothesis_mean, sample_size, sample_mean, sample_standard_deviation)
    p_value = query_upper_tailed_p_value(test_statistics_z_score)

    print('H0: population mean <= ' + '{0:.4}'.format(hypothesis_mean))
    print('H1: population mean > ' + '{0:.4}'.format(hypothesis_mean))
    print('significance: ' + '{0:.4f}'.format(significance))
    print('critical_z_score: ' + '{0:.4f}'.format(critical_z_score))
    print('test_statistics_z_score: ' + '{0:.4f}'.format(test_statistics_z_score))
    print('p_value: ' + '{0:.4f}'.format(p_value))
    print()

    print('z-test with z-score');
    if test_statistics_z_score > critical_z_score:
        print('reject H0')
    else:
        print('not reject H0')
    print()

    print('z-test with p-value:')
    if p_value < significance:
        print('reject H0')
    else:
        print('not reject H0')

if __name__ == "__main__":
    main()
```

## output
```
H0: population mean <= 40.0
H1: population mean > 40.0
significance: 0.0200
critical_z_score: 2.0537
test_statistics_z_score: 1.7678
p_value: 0.0385

z-test with z-score
not reject H0

z-test with p-value:
not reject H0
```
