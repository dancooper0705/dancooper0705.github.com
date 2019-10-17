---
layout: post
title: "statistics-for-business-and-economics-p9-22"
date:  2019-10-16 12:00:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
Consider the following hypothesis test.
H0: u = 15
Ha: u != 15
A sample of 50 gives a sample mean of 14.2 and sample standard deviation of 5.
a. At alpha = 0.02, what is the rejection rule?
b. Compute the value of teh test statistics z.
c. What is the p-value?
d. What is your conclusion?
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
    hypothesis_mean = 15.0
    sample_size = 50
    sample_mean = 14.2
    sample_standard_deviation = 5.0
    significance = 0.02
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
H0: population mean = 15.0
Ha: population mean != 15.0
significance: 0.0200
critical_z_score: 2.3263
test_statistics_z_score: -1.1314
p_value: 0.2579

z-test with z-score
reject if z_score < -2.3263 or z_score > 2.3263
not reject H0

z-test with p-value:
reject if p_value < 0.0200
not reject H0
```
