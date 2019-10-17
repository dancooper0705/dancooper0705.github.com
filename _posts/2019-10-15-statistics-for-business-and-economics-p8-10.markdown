---
layout: post
title: "statistics-for-business-and-economics-p8-10"
date:  2019-10-15 11:00:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
10. The profitability of used car sales was determined in a study conducted by
the National Automobile Dealers Association(USA Today, April 12, 1995). Assume
that a sample of 200 used car sales provided a sample mean profict of $300 and a
sample standard deviation of $150. Use this information to develop 95%
confidence interval estimate of the mean profict for the population of used car
sales.
```

## source
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

def main():
    sample_size = 200
    sample_mean = 300
    sample_standard_deviation = 150
    print('95% confidence interval for population mean: ' + ' to '.join('{0:.0f}'.format(a) for a in confidence_interval_of_population_mean(sample_size, sample_mean, sample_standard_deviation, 95)))

if __name__ == "__main__":
    main()
```

## output
```
95% confidence interval for population mean: 279 to 321
```
