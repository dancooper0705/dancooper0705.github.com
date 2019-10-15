---
layout: post
title: "statistics-for-business-and-economics-p8-6"
date:  2019-10-14 23:30:00  +0800
categories: [dev]
tags: [python, statistics]
---

## question
```
6. Mean weekly earnings of individuals working in various industries were
reported  in The New York Times 1998 Almanac. The mean weekly earnings for
individuals in the service industry were $369. Assume that this result was
based on a sample of 250 service individual and that the sample standard deviation
was $50. Compute the 95% confidence interval for the population mean weekly
earnings for individuals working in the service industry.
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
    sample_size = 250
    sample_mean = 369
    sample_standard_deviation = 50
    confidence_level = 95
    print('95% confidence interval for population mean: ' + str(confidence_interval_of_population_mean(sample_size, sample_mean, sample_standard_deviation, confidence_level)))

if __name__ == "__main__":
    main()
```

## output
```
95% confidence interval for population mean: [362.80204967695437, 375.19795032304563]
```
