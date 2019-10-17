---
layout: post
title: "statistics-for-business-and-economics-p9-36"
date:  2019-10-17 13:00:00  +0800
categories: [dev]
tags: [python, statistics]
---

## question
```
Consider the following hypothesis test.
H0: u <= 50
Ha: u > 50
Assume a sample of 16 items provides the following test statistics. What can you
say about the p-value in each case? What are your conclusions based on alpha =
0.05?
a. t = 2.602
b. t = 1.341
c. t = 1.960
d. t = 1.055
e. t = 3.261
```

## source
### dcstats.py
```python
import math
import scipy.stats

def confidence_interval_of_population_proportion(sample_size, sample_proportion, confidence_level):
    mean = sample_proportion
    standard_deviation = math.sqrt(sample_proportion * (1 - sample_proportion) / sample_size)
    cotgfidence_coefficient = confidence_level / 100
    alpha_level = 1 - confidence_coefficient
    tail_area = alpha_level / 2
    z_score = scipy.stats.norm.ppf(1 - tail_area)
    return [mean - z_score * standard_deviation, mean + z_score * standard_deviation]

def sample_size_for_confidence_level_of_population_proportion(sample_proportion, margin_of_error, confidence_level):
    confidence_coefficient = confidence_level / 100
    alpha_level = 1 - confidence_coefficient
    tail_area = alpha_level / 2
    z_score = scipy.stats.norm.ppf(1 - tail_area)
    return math.ceil(z_score**2 * sample_proportion * (1 - sample_proportion) / (margin_of_error ** 2))

def confidence_interval_of_population_mean_with_normal_distribution(sample_size, sample_mean, sample_standard_deviation, confidence_level):
    mean = sample_mean
    standard_deviation = sample_standard_deviation / math.sqrt(sample_size)
    confidence_coefficient = confidence_level / 100
    alpha_level = 1 - confidence_coefficient
    tail_area = alpha_level / 2
    z_score = scipy.stats.norm.ppf(1 - tail_area)
    return [mean - z_score * standard_deviation, mean + z_score * standard_deviation]

def confidence_interval_of_population_mean_with_students_t_distribution(sample_size, sample_mean, sample_standard_deviation, confidence_level):
    mean = sample_mean
    standard_deviation = sample_standard_deviation / math.sqrt(sample_size)
    confidence_coefficient = confidence_level / 100
    alpha_level = 1 - confidence_coefficient
    tail_area = alpha_level / 2
    degree_freedom = sample_size - 1
    t_score = scipy.stats.t.ppf(1 - tail_area, degree_freedom)
    return [mean - t_score * standard_deviation, mean + t_score * standard_deviation]

def confidence_interval_of_population_mean(sample_size, sample_mean, sample_standard_deviation, confidence_level, is_population_standard_deviationi_known=False):
    if is_population_standard_deviationi_known == True or sample_size >= 30:
        return confidence_interval_of_population_mean_with_normal_distribution(sample_size, sample_mean, sample_standard_deviation, confidence_level)
    else:
        return confidence_interval_of_population_mean_with_students_t_distribution(sample_size, sample_mean, sample_standard_deviation, confidence_level)

def upper_tailed_critical_z_score(significance):
    tail_area = significance
    critical_z_score = scipy.stats.norm.ppf(1 - tail_area)
    return critical_z_score

def lower_tailed_critical_z_score(significance):
    tail_area = significance
    critical_z_score = scipy.stats.norm.ppf(tail_area)
    return critical_z_score

def two_tailed_critical_z_score(significance):
    tail_area = significance / 2
    critical_z_score = scipy.stats.norm.ppf(1 - tail_area)
    return critical_z_score

def test_statistics_score(hypothesis_mean, sample_size, sample_mean, sample_standard_deviation):
    standard_deviation = sample_standard_deviation / math.sqrt(sample_size)
    z_score = (sample_mean - hypothesis_mean) / standard_deviation
    return z_score

def upper_tailed_p_value_with_z_score(z_score):
    p_value = scipy.stats.norm.cdf(-z_score)
    return p_value

def lower_tailed_p_value_with_z_score(z_score):
    p_value = scipy.stats.norm.cdf(z_score)
    return p_value

def two_tailed_p_value_with_z_score(z_score):
    p_value = 2.0 * scipy.stats.norm.cdf(-abs(z_score))
    return p_value

def upper_tailed_critical_t_score(significance, df):
    return scipy.stats.t.ppf(1 - significance, df)

def lower_tailed_critical_t_score(significance, df):
    return scipy.stats.t.ppf(significance, df)

def two_tailed_critical_t_score(significance, df):
    return scipy.stats.t.ppf(1 - significance / 2, df)

def upper_tailed_p_value_with_t_score(t_score, df):
    return scipy.stats.t.cdf(-t_score, df)

def lower_tailed_p_value_with_t_score(t_score, df):
    return scipy.stats.norm.cdf(t_score)

def two_tailed_p_value_with_t_score(t_score, df):
    return 2.0 * scipy.stats.norm.cdf(-abs(t_score))
```
### a.py
```python
import math
import scipy.stats
import numpy as np
import dcstats

def main():
    hypothesis_mean = 50.0
    sample_size = 16
    significance = 0.05
    df = sample_size - 1
    critical_t_score = dcstats.upper_tailed_critical_t_score(significance, df)
    print('hypothesis_mean: ' + '{0:.4f}'.format(hypothesis_mean))
    print('H0: population mean <= ' + '{0:.4}'.format(hypothesis_mean))
    print('Ha: population mean > ' + '{0:.4}'.format(hypothesis_mean))
    print('significance: ' + '{0:.4f}'.format(significance))
    print('critical_t_score: ' + '{0:.4f}'.format(critical_t_score))
    print()

    test_statistics_t_scores = [2.602, 1.341, 1.960, 1.055, 3.261]
    for i in range(len(test_statistics_t_scores)):
        print('Example ' + str(i + 1) + ":")
        test_statistics_t_score = test_statistics_t_scores[i]
        p_value = dcstats.upper_tailed_p_value_with_t_score(test_statistics_t_score, df)
        print('test_statistics_t_score: ' + '{0:.4f}'.format(test_statistics_t_score))
        print('p_value: ' + '{0:.4f}'.format(p_value))
        print()

        print('t-test with t-score:');
        print('reject if t_score > ' + '{0:.4f}'.format(critical_t_score))
        if test_statistics_t_score > critical_t_score:
            print('reject H0')
        else:
            print('not reject H0')
        print()

        print('t-test with p-value:')
        print('reject if p_value < ' + '{0:.4f}'.format(significance))
        if p_value < significance:
            print('reject H0')
        else:
            print('not reject H0')
        print()

if __name__ == "__main__":
    main()
```

## output
```
hypothesis_mean: 50.0000
H0: population mean <= 50.0
Ha: population mean > 50.0
significance: 0.0500
critical_t_score: 1.7531

Example 1:
test_statistics_t_score: 2.6020
p_value: 0.0100

t-test with t-score:
reject if t_score > 1.7531
reject H0

t-test with p-value:
reject if p_value < 0.0500
reject H0

Example 2:
test_statistics_t_score: 1.3410
p_value: 0.0999

t-test with t-score:
reject if t_score > 1.7531
not reject H0

t-test with p-value:
reject if p_value < 0.0500
not reject H0

Example 3:
test_statistics_t_score: 1.9600
p_value: 0.0344

t-test with t-score:
reject if t_score > 1.7531
reject H0

t-test with p-value:
reject if p_value < 0.0500
reject H0

Example 4:
test_statistics_t_score: 1.0550
p_value: 0.1541

t-test with t-score:
reject if t_score > 1.7531
not reject H0

t-test with p-value:
reject if p_value < 0.0500
not reject H0

Example 5:
test_statistics_t_score: 3.2610
p_value: 0.0026

t-test with t-score:
reject if t_score > 1.7531
reject H0

t-test with p-value:
reject if p_value < 0.0500
reject H0
```
