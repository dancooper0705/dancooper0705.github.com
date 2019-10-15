---
layout: post
title: "statistics-for-business-and-economics-p8-16"
date:  2019-10-15 14:00:00  +0800
categories: [dev]
tags: [python, statistics]
---

## question
```
A simple random sample of 20 items from a normal population resulted in a sample
mean of 17.25 and a sample standard deviation of 3.3.
a. Develop a 90% confidence interval for the population mean.
b. Develop a 95% confidence interval for the population mean.
c. Develop a 99% confidence interval for the population mean.
```

## source
```python
import math
import scipy.stats

def confidence_interval_of_population_mean(sample_size, sample_mean, sample_standard_deviation, confidence_level, is_population_standard_deviationi_known=False):
    mean = sample_mean
    standard_deviation = sample_standard_deviation / math.sqrt(sample_size)
    confidence_coefficient = confidence_level / 100
    alpha_level = 1 - confidence_coefficient
    tail_area = alpha_level / 2
    if is_population_standard_deviationi_known == True or sample_size >= 30:
        z_score = scipy.stats.norm.ppf(1 - tail_area)
        return [mean - z_score * standard_deviation, mean + z_score * standard_deviation]
    else:
        degree_freedom = sample_size - 1
        t_score = scipy.stats.t.ppf(1 - tail_area, degree_freedom)
        return [mean - t_score * standard_deviation, mean + t_score * standard_deviation]

def main():
    sample_size = 20
    sample_mean = 17.25
    sample_standard_deviation = 3.3
    print('90% confidence interval for population mean: ' + ' to '.join('{0:.2f}'.format(a) for a in confidence_interval_of_population_mean(sample_size, sample_mean, sample_standard_deviation, 90)))
    print('95% confidence interval for population mean: ' + ' to '.join('{0:.2f}'.format(a) for a in confidence_interval_of_population_mean(sample_size, sample_mean, sample_standard_deviation, 95)))
    print('99% confidence interval for population mean: ' + ' to '.join('{0:.2f}'.format(a) for a in confidence_interval_of_population_mean(sample_size, sample_mean, sample_standard_deviation, 99)))

if __name__ == "__main__":
    main()
```

## output
```
90% confidence interval for population mean: 15.97 to 18.53
95% confidence interval for population mean: 15.71 to 18.79
99% confidence interval for population mean: 15.14 to 19.36
```
