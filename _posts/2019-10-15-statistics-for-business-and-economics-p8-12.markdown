---
layout: post
title: "statistics-for-business-and-economics-p8-12"
date:  2019-10-15 11:30:00  +0800
categories: [dev]
tags: [python, statistics]
---

## question
```
The Internaltional Air Transport Association surveys business travelers to
develop quality ratings for transatlantic gateway airports. The maximum
possible ratings is 10. The highest rated airport is Amsterdam with an average
of 7.93, followed by Toronto with rating of 7.17(Newsweek, June 13, 1994).
Suppose a simple random sample of 50 business travelers is selected and each
traverler is asked to provide a rating for the Miami International Airport. The
ratings obtained from the sample of 50 follow.
6 4 6 8 7 7 6 3 3 8 10 4 8
7 8 7 5 9 5 8 4 3 8 5 5 4
4 4 8 4 5 6 2 5 9 9 8 4 8
9 9 5 9 7 8 3 10 8 9 6
Develop a 95% confidence interval estimate for the population mean rating for
Miami.
```

## source
### dcstat.py
```python
import math
import scipy.stats

def confidence_interval_of_population_mean(sample_size, sample_mean, sample_standard_deviation, confidence_level):
    mean = sample_mean
    standard_deviation = sample_standard_deviation / math.sqrt(sample_size)
    confidence_coefficient = confidence_level / 100
    alpha_level = 1 - confidence_coefficient
    tail_area = alpha_level / 2
    z_score = scipy.stats.norm.ppf(1 - tail_area)
    return [mean - z_score * standard_deviation, mean + z_score * standard_deviation]

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
    for i in range(30):
        sample.add_element(i)
    print('sample.size(): ' + str(sample.size()))
    print('sample.mean(): ' + str(sample.mean()))
    print('sample.variance(): ' + str(sample.variance()))
    print('sample.standard_deviation(): ' + str(sample.standard_deviation()))
    print('90% confidence interval for population mean: ' + str(sample.confidence_interval_of_population_mean(90)))
    print('95% confidence interval for population mean: ' + str(sample.confidence_interval_of_population_mean(95)))
    print('99% confidence interval for population mean: ' + str(sample.confidence_interval_of_population_mean(99)))

if __name__ == "__main__":
    main()
```
### a.py
```python
import dcstat

def main():
    ratings = [6, 4, 6, 8, 7, 7, 6, 3, 3, 8, 10, 4, 8, 7, 8, 7, 5, 9, 5, 8, 4, 3, 8, 5, 5, 4, 4, 4, 8, 4, 5, 6, 2, 5, 9, 9, 8, 4, 8, 9, 9, 5, 9, 7, 8, 3, 10, 8, 9, 6]
    sample = dcstat.Sample()
    for a in ratings:
        sample.add_element(a)
    print('95% confidence interval estimate for the population mean: ' + ' to '.join("{0:.2f}".format(a) for a in sample.confidence_interval_of_population_mean(95)))

if __name__ == "__main__":
    main()
```

## output
```bash
bash-3.2$ python3 a.py 
95% confidence interval estimate for the population mean: 5.74 to 6.94
```
