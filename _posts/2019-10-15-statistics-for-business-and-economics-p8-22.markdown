---
layout: post
title: "statistics-for-business-and-economics-p8-22"
date:  2019-10-15 15:30:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
The number of hours American sleep each night varies considerably with 12% of
the population sleeping less than six hours to 3% sleeping more than eight
hours(The Macmillan Visual Almanac, 1996). A sample of 25 individuals reported
the hours of sleep per night as shown below.
6.9 7.6 6.5 6.2 5.3
7.8 7.0 5.5 7.6 6.7
7.3 6.6 7.1 6.9 6.0
6.8 6.5 7.2 5.8 8.6
7.6 7.1 6.0 7.2 7.7
a. what is the point estimate of the population mean number of hours of sleep
each night.
b.  Assuming that the population has a normal distribution, develop a 95%
confidence interval for the population mean numbero of hours of sleep each night?
```

## source
### dcstat.py
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

class Sample:
    arr = []

    def __init__(self):
        pass

    def add_element(self, val):
        self.arr.append(val)

    def size(self):
        return len(self.arr)

    def mean(self):
        total = 0
        for a in self.arr:
            total += a
        avg = total / len(self.arr)
        return avg

    def variance(self):
        ans = 0
        x = 0
        x2 = 0
        n = len(self.arr)
        for a in self.arr:
            x = x + a
            x2 = x2 + a ** 2
        ans = (x2 - x **2 / n) / (n - 1)
        return ans

    def standard_deviation(self):
        return math.sqrt(self.variance())

    def confidence_interval_of_population_mean(self, confidence_level):
        sample_size = self.size()
        sample_mean = self.mean()
        sample_standard_deviation = self.standard_deviation()
        return confidence_interval_of_population_mean(sample_size, sample_mean, sample_standard_deviation, confidence_level)

def main():
    sample = Sample()
    ratings = [6, 4, 6, 8, 7, 7, 6, 3, 3, 8, 10, 4, 8, 7, 8, 7, 5, 9, 5, 8, 4, 3, 8, 5, 5, 4, 4, 4, 8, 4, 5, 6, 2, 5, 9, 9, 8, 4, 8, 9, 9, 5, 9, 7, 8, 3, 10, 8, 9, 6]
    sample = Sample()
    for a in ratings:
        sample.add_element(a)
    print('example1, sample size >= 30, use t-score to estimate confidence interval')
    print('sample.size(): ' + str(sample.size()))
    print('sample.mean(): ' + str(sample.mean()))
    print('sample.variance(): ' + str(sample.variance()))
    print('sample.standard_deviation(): ' + str(sample.standard_deviation()))
    print('90% confidence interval for population mean: ' + ' to '.join('{0:.2f}'.format(a) for a in sample.confidence_interval_of_population_mean(90)))
    print('95% confidence interval for population mean: ' + ' to '.join('{0:.2f}'.format(a) for a in sample.confidence_interval_of_population_mean(95)))
    print('99% confidence interval for population mean: ' + ' to '.join('{0:.2f}'.format(a) for a in sample.confidence_interval_of_population_mean(99)))
    print()

    print('example2, sample size < 30, use t-score to estimate confidence interval')
    sample_size = 20
    sample_mean = 17.25
    sample_standard_deviation = 3.3
    print('sample.size: ' + str(sample_size))
    print('sample.mean: ' + str(sample_mean))
    print('sample.standard_deviation: ' + str(sample_standard_deviation))
    print('90% confidence interval for population mean: ' + ' to '.join('{0:.2f}'.format(a) for a in confidence_interval_of_population_mean(sample_size, sample_mean, sample_standard_deviation, 90)))
    print('95% confidence interval for population mean: ' + ' to '.join('{0:.2f}'.format(a) for a in confidence_interval_of_population_mean(sample_size, sample_mean, sample_standard_deviation, 95)))
    print('99% confidence interval for population mean: ' + ' to '.join('{0:.2f}'.format(a) for a in confidence_interval_of_population_mean(sample_size, sample_mean, sample_standard_deviation, 99)))

if __name__ == "__main__":
    main()
```
### a.py
```python
import dcstat

def main():
    data = [6.9, 7.6, 6.5, 6.2, 5.3, 7.8, 7.0, 5.5, 7.6, 6.7, 7.3, 6.6, 7.1, 6.9, 6.0, 6.8, 6.5, 7.2, 5.8, 8.6, 7.6, 7.1, 6.0, 7.2, 7.7]
    sample = dcstat.Sample()
    for a in data:
        sample.add_element(a)
    print('sample: ' + str(data))
    print('point estimate of population mean: ' + '{0:.2f}'.format(sample.mean()))
    print('95% confidence interval for population mean: ' + ' to '.join('{0:.2f}'.format(a) for a in sample.confidence_interval_of_population_mean(95)))

if __name__ == "__main__":
    main()
```

## output
```bash
6.86
6.54 to 7.18
```
