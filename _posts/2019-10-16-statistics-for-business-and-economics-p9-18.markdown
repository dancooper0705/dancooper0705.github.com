---
layout: post
title: "statistics-for-business-and-economics-p9-18"
date:  2019-10-16 10:30:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
New tires manufactured by a company in Findlay, Ohio, are designed to provide a
mean of at least 28000 miles. Testes with 30 tires show a sample mean of 27500
miles and a sample standard deviation of 1000 miles. Using a 0.05 level of
significance, test whether there is a sufficient evidence to reject the cliam of
a mean of at least 28000 miles. What is the p-value?
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

def main():
    hypothesis_mean = 28000.0
    sample_size = 30
    sample_mean = 27500
    sample_standard_deviation = 1000.0
    significance = 0.05
    critical_z_score = query_lower_tailed_critical_z_score(significance)
    test_statistics_z_score = query_test_statistics_z_score(hypothesis_mean, sample_size, sample_mean, sample_standard_deviation)
    p_value = query_lower_tailed_p_value(test_statistics_z_score)

    print('H0: population mean >= ' + '{0:.4}'.format(hypothesis_mean))
    print('H1: population mean < ' + '{0:.4}'.format(hypothesis_mean))
    print('significance: ' + '{0:.4f}'.format(significance))
    print('critical_z_score: ' + '{0:.4f}'.format(critical_z_score))
    print('test_statistics_z_score: ' + '{0:.4f}'.format(test_statistics_z_score))
    print('p_value: ' + '{0:.4f}'.format(p_value))
    print()

    print('z-test with z-score');
    if test_statistics_z_score < critical_z_score:
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
H0: population mean >= 2.8e+04
H1: population mean < 2.8e+04
significance: 0.0500
critical_z_score: -1.6449
test_statistics_z_score: -2.7386
p_value: 0.0031

z-test with z-score
reject H0

z-test with p-value:
reject H0
```
