---
layout: post
title: "statistics-for-business-and-economics-p9-48"
date:  2019-10-17 17:30:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
Burger King sponsered what it believed to be the biggest product giveaway in
fast-food history when it initiated FreeFryDay on Friday, January 2, 1998.
Anyone who stopped at one of Burger Kings's 7400 restaurants received a samll
order of the new Burger King fries freee of charge. A national taste test
comparing the new Burger King fries to McDonalsd's fries as the basis for the
launch of the Burger King promotion. Of the 500 customers who participated in
the taste test, 285 expressed a taste preference for the Burger King fries(USA
Today, December 10, 1997). Let p = the population promotion who favors the
Burger King fries. Consider the hypothesis following test:
H0: p <= 0.50
Ha: p > 0.50
a. What is the point estimate of the population proportion that favors the
Burger King fries?
b. What is your conclusion? Use a 0.01 level of significance.
c. Do you believe that the national taste test statistics helped Burger King's
management decide to implement the FreeFryDay campaigan? Discuss.
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
    hypothesis_proportion = 0.50
    sample_size = 500
    sample_proportion = 285 / sample_size
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
hypothesis_proportion: 0.5000
sample_size: 500
sample_proportion: 0.5700
sample_standard_deviation: 0.0224

H0: population proportion <= 0.5
Ha: population proportion > 0.5
significance: 0.0100
critical_z_score: 2.3263
test_statistics_z_score: 3.1305
p_value: 0.0009

z-test with z-score:
reject if z_score > 2.3263
reject H0

z-test with p-value:
reject if p_value < 0.0100
reject H0
```

## discuss
```
Q: Do you believe that the national taste test statistics helped Burger King's
management decide to implement the FreeFryDay campaigan? Discuss.

A: Yes. According the result of alternative hypothesis, the Burger King's
management have confidence of their own fries. They think the free fries
campaign could help attract more customers.
```
