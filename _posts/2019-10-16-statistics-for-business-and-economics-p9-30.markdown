---
layout: post
title: "statistics-for-business-and-economics-p9-30"
date:  2019-10-16 14:40:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
The mean salary for full professors in the United States is $61650(The American
Almanac of Jobs and Salaries. 1994-1995 Edition). A sample of 36 full professors
at business colleges showed sample mean is 72800 and sample standard deviation
is 5000.
a. Develop a 95% confidence interval for the population mean salary of business
college professors.
b. Use the confidence interval to conduct hypothesis test H0: u = 61650 and Ha:
u != 61650. What is your conclusion?
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
    hypothesis_mean = 61650.0
    sample_size = 36
    sample_mean = 72800.0
    sample_standard_deviation = 5000.0
    significance = 0.05
    print('hypothesis_mean: ' + '{0:.4f}'.format(hypothesis_mean))
    print('sample_size: ' + '{0:d}'.format(sample_size))
    print('sample_mean: ' + '{0:.4f}'.format(sample_mean))
    print('sample_standard_deviation: ' + '{0:.4f}'.format(sample_standard_deviation))
    print()

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
    print()

    confidence_interval = confidence_interval_of_population_mean(sample_size, sample_mean, sample_standard_deviation, 95)
    print('95% confidence interval for population mean: ' + ' to '.join('{0:.2f}'.format(a) for a in confidence_interval))
    print('z_test with confidence interval')
    if hypothesis_mean < confidence_interval[0] or hypothesis_mean > confidence_interval[1]:
        print('reject H0')
    else:
        print('not reject H0')

if __name__ == "__main__":
    main()
```

## output
```
hypothesis_mean: 61650.0000
sample_size: 36
sample_mean: 72800.0000
sample_standard_deviation: 5000.0000

H0: population mean = 6.165e+04
Ha: population mean != 6.165e+04
significance: 0.0500
critical_z_score: 1.9600
test_statistics_z_score: 13.3800
p_value: 0.0000

z-test with z-score
reject if z_score < -1.9600 or z_score > 1.9600
reject H0

z-test with p-value:
reject if p_value < 0.0500
reject H0

95% confidence interval for population mean: 71166.70 to 74433.30
z_test with confidence interval
reject H0
```
