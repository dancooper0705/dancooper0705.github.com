---
layout: post
title: "statistics-for-business-and-economics-p9-20"
date:  2019-10-16 11:00:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
A new diet program claims that participants will lose on average at least eight
pounds during the first week of the program. A random sample of 40 people
participating in the program showed a sample mean wieght of seven punds. The
sample standard deviation was 3.2 punds.
a. What is the reject rule with significance = 0.05
b. What is your conclusion about the claim made the die program?
c. What is the p-value?
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
    hypothesis_mean = 8.0
    sample_size = 40
    sample_mean = 7.0
    sample_standard_deviation = 3.2
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
H0: population mean >= 8.0
H1: population mean < 8.0
significance: 0.0500
critical_z_score: -1.6449
test_statistics_z_score: -1.9764
p_value: 0.0241

z-test with z-score
reject H0

z-test with p-value:
reject H0
```
