---
layout: post
title: "statistics-for-business-and-economics-p9-42"
date:  2019-10-17 15:00:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
Joan's Nursery specializes in custom-designed landscaping for residential areas.
The estimated labor cost associated with a particular landscaping proposal is
based on the number of plantings of trees, shrubs, and so on to be used for the
project. For cost-estimating purposes, managers use two hours of labor time for
the planting of a medium-size tree. Actual times from a sample of 10 plantings
during the past month follow (times in hours).

1.9 1.7 2.8 2.4 2.6 2.5 2.8 3.2 1.6 2.5

Using a 0.05 level of significance, test to see whether the mean tree-planting
time exceeds two hours. What is your conclusion, and what recommendations would
you consider making to the managers?
```

## source
### dcstats.py
```python
import math
import scipy.stats

def confidence_interval_of_population_proportion(sample_size, sample_proportion, confidence_level):
    mean = sample_proportion
    standard_deviation = math.sqrt(sample_proportion * (1 - sample_proportion) / sample_size)
    confidence_coefficient = confidence_level / 100
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

def test_statistics_score(population_mean, sample_size, sample_mean, sample_standard_deviation):
    standard_deviation = sample_standard_deviation / math.sqrt(sample_size)
    z_score = (sample_mean - population_mean) / standard_deviation
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
    return scipy.stats.t.cdf(t_score, df)

def two_tailed_p_value_with_t_score(t_score, df):
    return 2.0 * scipy.stats.t.cdf(-abs(t_score), df)
```
### a.py
```python
import math
import scipy.stats
import numpy as np
import dcstats

def main():
    sample = [1.9, 1.7, 2.8, 2.4, 2.6, 2.5, 2.8, 3.2, 1.6, 2.5]
    hypothesis_mean = 2.0
    sample_size = len(sample)
    sample_mean = np.mean(sample)
    sample_standard_deviation = np.std(sample, ddof=1)
    significance = 0.05
    print('hypothesis_mean: ' + '{0:.4f}'.format(hypothesis_mean))
    print('sample_size: ' + '{0:d}'.format(sample_size))
    print('sample_mean: ' + '{0:.4f}'.format(sample_mean))
    print('sample_standard_deviation: ' + '{0:.4f}'.format(sample_standard_deviation))
    print()

    df = sample_size - 1
    critical_t_score = dcstats.upper_tailed_critical_t_score(significance, df)
    test_statistics_t_score = dcstats.test_statistics_score(hypothesis_mean, sample_size, sample_mean, sample_standard_deviation)
    p_value = dcstats.upper_tailed_p_value_with_t_score(test_statistics_t_score, df)
    print('H0: population mean <= ' + '{0:.4}'.format(hypothesis_mean))
    print('Ha: population mean > ' + '{0:.4}'.format(hypothesis_mean))
    print('significance: ' + '{0:.4f}'.format(significance))
    print('critical_t_score: ' + '{0:.4f}'.format(critical_t_score))
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

if __name__ == "__main__":
    main()
```

## output
```
hypothesis_mean: 2.0000
sample_size: 10
sample_mean: 2.4000
sample_standard_deviation: 0.5164

H0: population mean <= 2.0
Ha: population mean > 2.0
significance: 0.0500
critical_t_score: 1.8331
test_statistics_t_score: 2.4495
p_value: 0.0184

t-test with t-score:
reject if t_score > 1.8331
reject H0

t-test with p-value:
reject if p_value < 0.0500
reject H0
```
