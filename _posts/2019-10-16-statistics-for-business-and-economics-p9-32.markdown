---
layout: post
title: "statistics-for-business-and-economics-p9-32"
date:  2019-10-16 15:00:00  +0800
categories: [dev]
tags: [python, statistics]
---

## question
```
An industry pays an average wage rate of $9.00 per hour. A sample of 36 workers
from one company showed a mean wage of u = $8.50 and a sample standard
deviation of s = $0.60.
a. A one-sided confidence interval uses the sample resultes to establish either
an upper limit or a lower limit for the value of the population parameter. For
this exercise establish an upper 95% confidence limit for the hourly wage rate
paied by company. The form of one-side confidence interval requires that we be
95% confident that the population mean is this value or less. What is 95%
confidence standard for this one-sided confidence interval?
b. Use the one-sided confidence interval result to test H0: u >= 9. What is your
conclusion? Explain.
```

## source
```python
import math
import scipy.stats

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
    hypothesis_mean = 9.0
    sample_size = 36
    sample_mean = 8.5
    sample_standard_deviation = 0.6
    significance = 0.05
    print('hypothesis_mean: ' + '{0:.4f}'.format(hypothesis_mean))
    print('sample_size: ' + '{0:d}'.format(sample_size))
    print('sample_mean: ' + '{0:.4f}'.format(sample_mean))
    print('sample_standard_deviation: ' + '{0:.4f}'.format(sample_standard_deviation))
    print()

    critical_z_score = query_lower_tailed_critical_z_score(significance)
    test_statistics_z_score = query_test_statistics_z_score(hypothesis_mean, sample_size, sample_mean, sample_standard_deviation)
    p_value = query_lower_tailed_p_value(test_statistics_z_score)
    print('H0: population mean >= ' + '{0:.4}'.format(hypothesis_mean))
    print('Ha: population mean < ' + '{0:.4}'.format(hypothesis_mean))
    print('significance: ' + '{0:.4f}'.format(significance))
    print('critical_z_score: ' + '{0:.4f}'.format(critical_z_score))
    print('test_statistics_z_score: ' + '{0:.4f}'.format(test_statistics_z_score))
    print('p_value: ' + '{0:.4f}'.format(p_value))
    print()

    print('z-test with z-score:');
    print('reject if z_score < ' + '{0:.4f}'.format(-critical_z_score))
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
    print()

    print('z_test with one-sided upper 95% confidence interval')
    confidence_interval = confidence_interval_of_population_mean(sample_size, sample_mean, sample_standard_deviation, 90)
    confidence_interval[0] = float('-inf')
    print('one-sided upper 95% confidence interval for population mean: ' + ' to '.join('{0:.2f}'.format(a) for a in confidence_interval))
    print('reject if hypothesis_mean > one-sided upper 95% confidence interval for population mean')
    if hypothesis_mean > confidence_interval[1]:
        print('reject H0')
    else:
        print('not reject H0')

if __name__ == "__main__":
    main()
```

## output
```
hypothesis_mean: 9.0000
sample_size: 36
sample_mean: 8.5000
sample_standard_deviation: 0.6000

H0: population mean >= 9.0
Ha: population mean < 9.0
significance: 0.0500
critical_z_score: -1.6449
test_statistics_z_score: -5.0000
p_value: 0.0000

z-test with z-score:
reject if z_score < 1.6449
reject H0

z-test with p-value:
reject if p_value < 0.0500
reject H0

z_test with one-sided upper 95% confidence interval
one-sided upper 95% confidence interval for population mean: -inf to 8.66
reject if hypothesis_mean > one-sided upper 95% confidence interval for population mean
reject H0
```
