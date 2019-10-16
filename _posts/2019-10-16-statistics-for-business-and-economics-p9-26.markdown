---
layout: post
title: "statistics-for-business-and-economics-p9-26"
date:  2019-10-16 14:00:00  +0800
categories: [dev]
tags: [python, statistics]
---

## question
```
CNN and ActMedia provided a television channel that showed news, features, and
ads, and was targeted to individuals waiting in grocery checkout lines. The
television program were designed with an eight-minute cycle on the assumption
that the population mean time a shooper stands in line at a grocery store
checkout is eight minutes(Astounding Averrages, 1995). A sample of 120 shoppers
at a major grocery store showed a sample mean waiting time of 7.5 minutes with a
sample stanard deviation of 3.2 minutes.
a. Test H0: u = 8 and Ha: u != 8. Use a 0.05 level of significance. Does the
population mean waiting at the grocery store differ from the eight-minute
waiting time assumption?
b. What is the p-value for the test?
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
    hypothesis_mean = 8.0
    sample_size = 120 
    sample_mean = 7.5
    sample_standard_deviation = 3.2
    significance = 0.05
    critical_z_score = query_two_tailed_critical_z_score(significance)
    test_statistics_z_score = query_test_statistics_z_score(hypothesis_mean, sample_size, sample_mean, sample_standard_deviation)
    p_value = query_two_tailed_p_value(test_statistics_z_score)

    print('H0: population mean = ' + '{0:.4}'.format(hypothesis_mean))
    print('Ha: population mean != ' + '{0:.4}'.format(hypothesis_mean))
    print('significance: ' + '{0:.4f}'.format(significance))
    print('critical_z_score: ' + '{0:.4f}'.format(critical_z_score))
    print('test_statistics_z_score: ' + '{0:.4f}'.format(test_statistics_z_score))
    print('p_value: ' + '{0:.4f}'.format(p_value))
    print()

    print('z-test with z-score');
    print('reject if z_score < ' + '{0:.4f}'.format(-critical_z_score) + ' or z_score > ' + '{0:.4f}'.format(critical_z_score))
    if test_statistics_z_score < -critical_z_score or test_statistics_z_score > critical_z_score:
        print('reject H0')
    else:
        print('not reject H0')
    print()

    print('z-test with p-value:')
    print('reject if p_value < ' + '{0:.4f}'.format(significance))
    if p_value < significance:
        print('reject H0')
    else:
        print('not reject H0')

if __name__ == "__main__":
    main()
```

## output
```
H0: population mean = 8.0
Ha: population mean != 8.0
significance: 0.0500
critical_z_score: 1.9600
test_statistics_z_score: -1.7116
p_value: 0.0870

z-test with z-score
reject if z_score < -1.9600 or z_score > 1.9600
not reject H0

z-test with p-value:
reject if p_value < 0.0500
not reject H0
```
