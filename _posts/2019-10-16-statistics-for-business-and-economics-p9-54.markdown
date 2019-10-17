---
layout: post
title: "statistics-for-business-and-economics-p9-54"
date:  2019-10-17 18:30:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
A fast-food restaurant plans a special offer that will enable customers to
purchase specially designed drink glasses featuring well-known cartoon
characters. If more than 15% of the cusotmers will purchase the glasses, the
special offer will be implemented. A preliminary test has bee set up at several
locations, and 88 of 500 customers have purchased the glasses. Should the
special glass offer be implemented? Conduct a hypothesis test that will support
your decision. Use a 0.01 level of significance. What is your recomendation?
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

def sample_mean_test_statistics_score(population_mean, sample_size, sample_mean, sample_standard_deviation):
    standard_deviation = sample_standard_deviation / math.sqrt(sample_size)
    z_score = (sample_mean - population_mean) / standard_deviation
    return z_score

def sample_proportion_test_statistics_score(population_proportion, sample_size, sample_proportion):
    standard_deviation = math.sqrt(population_proportion * (1 - population_proportion) / sample_size)
    z_score = (sample_proportion - population_proportion) / standard_deviation
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
    t_score = scipy.stats.t.ppf(1 - significance, df)
    return t_score

def lower_tailed_critical_t_score(significance, df):
    t_score = scipy.stats.t.ppf(significance, df)
    return t_score

def two_tailed_critical_t_score(significance, df):
    t_score = scipy.stats.t.ppf(1 - significance / 2, df)
    return t_score

def upper_tailed_p_value_with_t_score(t_score, df):
    t_score = scipy.stats.t.cdf(-t_score, df)
    return t_score

def lower_tailed_p_value_with_t_score(t_score, df):
    t_score = scipy.stats.t.cdf(t_score, df)
    return t_score

def two_tailed_p_value_with_t_score(t_score, df):
    t_score = 2.0 * scipy.stats.t.cdf(-abs(t_score), df)
    return t_score
```
### a.py
```python
import math
import scipy.stats
import numpy as np
import dcstats

def main():
    hypothesis_proportion = 0.15
    sample_size = 500
    sample_proportion = 88  / sample_size
    sample_standard_deviation = math.sqrt(hypothesis_proportion * (1 - hypothesis_proportion) / sample_size)
    significance = 0.01
    print('hypothesis_proportion: ' + '{0:.4f}'.format(hypothesis_proportion))
    print('sample_size: ' + '{0:d}'.format(sample_size))
    print('sample_proportion: ' + '{0:.4f}'.format(sample_proportion))
    print('sample_standard_deviation: ' + '{0:.4f}'.format(sample_standard_deviation))
    print()

    critical_z_score = dcstats.upper_tailed_critical_z_score(significance)
    test_statistics_z_score = dcstats.sample_proportion_test_statistics_score(hypothesis_proportion, sample_size, sample_proportion)
    p_value = dcstats.upper_tailed_p_value_with_z_score(test_statistics_z_score)
    print('H0: population proportion <= ' + '{0:.4}'.format(hypothesis_proportion))
    print('Ha: population proportion > ' + '{0:.4}'.format(hypothesis_proportion))
    print('significance: ' + '{0:.4f}'.format(significance))
    print('critical_z_score: ' + '{0:.4f}'.format(critical_z_score))
    print('test_statistics_z_score: ' + '{0:.4f}'.format(test_statistics_z_score))
    print('p_value: ' + '{0:.4f}'.format(p_value))
    print()

    print('z-test with z-score:');
    print('reject if z_score > ' + '{0:.4f}'.format(critical_z_score))
    if test_statistics_z_score > critical_z_score:
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
hypothesis_proportion: 0.1500
sample_size: 500
sample_proportion: 0.1760
sample_standard_deviation: 0.0160

H0: population proportion <= 0.15
Ha: population proportion > 0.15
significance: 0.0100
critical_z_score: 2.3263
test_statistics_z_score: 1.6282
p_value: 0.0517

z-test with z-score:
reject if z_score > 2.3263
not reject H0

z-test with p-value:
reject if p_value < 0.0100
not reject H0
```

## conclusion
```
statistics test doesn't support population proportion > 0.15.
```
