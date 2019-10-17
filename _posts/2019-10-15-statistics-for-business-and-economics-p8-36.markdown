---
layout: post
title: "statistics-for-business-and-economics-p8-36"
date:  2019-10-15 18:00:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
The Bureau of National Affairs, Inc., selected 617 companies and found that 56
companies required their employees to surrender airline frequent-flier mileage
awards for business related travel(The Wall Street Journal, March 28, 1994).
a. What is the point estimate of the proportion of all companies that require
their employees to surrender airline frequent-flier mileage awards?
b. Develop a 95% confidence interval estimate of the population proportion.
```

## source
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

def main():
    sample_size = 617
    sample_proportion = 56 / sample_size
    print('sample_proportion: ' + '{0:.4f}'.format(sample_proportion))
    print('95% confidence interval for population proportion: ' + ' to '.join('{0:.4f}'.format(a) for a in confidence_interval_of_population_proportion(sample_size, sample_proportion, 95)))

if __name__ == "__main__":
    main()
```

## output
```
sample_proportion: 0.0908
95% confidence interval for population proportion: 0.0681 to 0.1134
```
