---
layout: post
title: "statistics-for-business-and-economics-p8-20"
date:  2019-10-15 14:30:00  +0800
categories: [dev]
tags: [python, statistics]
---

## question
```
The Money & Investing section of the The Wall Street Journal contains a summary
of daily investing performance for stock exchange, overseas market, options,
commodities, futures, and so on. In the New York Stock Exchange section,
information is provided on each stock's 52-week high price per share, 52-week
low price per share, closing price per share, and daily net change. The
P/E(price-earnings) ratio for each stock is determined by dividing the price of
a share of stock by the earnings per share reported by the company for the most
recent four quarters. A sample of 10 stocks taken from The Wall Street
Journal(March 19, 1998) provided the following data on P/E ratio: 5, 7, 9, 10,
14, 23, 20, 15, 3, 26.
a. What is the point estimate of the mean P/E ratio for the population of all
stocks listed in the New York Stock Exchange?
b. What is the point estimate of the standard deviation of the P/E ratios for
the population of all stocks listed on the New York Stock Exchange?
c. At 95% confidence, what is the interval estimate of the P/E ratio for the
population of all stocks listed on the New York Stock Exchange? Assume that the
population has a nomark distribution.
d. Comment on the precision of the result.
```

## source
### dcstat.py
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
    data = [5, 7, 9, 10, 14, 23, 20, 15, 3, 26]
    sample = dcstat.Sample()
    for a in data:
        sample.add_element(a)
    print('sample: ' + str(data))
    print('point estimate of population mean: ' + '{0:.1f}'.format(sample.mean()))
    print('point estimate of population standard deviation: ' + '{0:.1f}'.format(sample.standard_deviation()))
    print('95% confidence interval estimate of population mean: ' + ' to '.join('{0:.2f}'.format(a) for a in sample.confidence_interval_of_population_mean(95)))
    print('The interval estimate is too wide. More sampled data is required')

if __name__ == "__main__":
    main()
```

## output
```bash
bash-3.2$ python3 a.py
sample: [5, 7, 9, 10, 14, 23, 20, 15, 3, 26]
point estimate of population mean: 13.2
point estimate of population standard deviation: 7.8
95% confidence interval estimate of population mean: 7.62 to 18.78
The interval estimate is too wide. More sampled data is required
```
