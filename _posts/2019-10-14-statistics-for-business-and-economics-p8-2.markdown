---
layout: post
title: "statistics-for-business-and-economics-p8-2"
date:  2019-10-14 21:00:00  +0800
categories: [dev]
tags: [python, statistics]
---

## question
```
2. A simple random sample of 50 items resulted in a sample mean of 32 and a sample
standard-deviation of 6.
a. Privide a 90% confidence interval for the popluation mean
b. Privide a 95% confidence interval for the popluation mean
c. Privide a 99% confidence interval for the popluation mean
```

## source code
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

def main():
    print('90% confidence interval for population mean: ' + str(confidence_interval_of_population_mean(50, 32, 6, 90)))
    print('95% confidence interval for population mean: ' + str(confidence_interval_of_population_mean(50, 32, 6, 95)))
    print('990% confidence interval for population mean: ' + str(confidence_interval_of_population_mean(50, 32, 6, 99)))

if __name__ == "__main__":
    main()
```

## output
```
90% confidence interval for population mean: [30.60429541558799, 33.39570458441201]
95% confidence interval for population mean: [30.336915410780385, 33.663084589219615]
990% confidence interval for population mean: [29.81433635873786, 34.18566364126214]
```
