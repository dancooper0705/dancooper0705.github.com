---
layout: post
title: "statistics-for-business-and-economics-p8-34"
date:  2019-10-15 17:20:00  +0800
categories: [dev]
tags: [python, statistics]
---

## question
```
Using 95% confidence, how large a sample should be taken to obain a margin of
error of 0.01 for the estimation of a population propotion of 0.03? Asssume that past
data are not available for developing a planning value for p.
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

def sample_size_for_confidence_level(sample_proportion, margin_of_error, confidence_level):
    confidence_coefficient = confidence_level / 100
    alpha_level = 1 - confidence_coefficient
    tail_area = alpha_level / 2
    z_score = scipy.stats.norm.ppf(1 - tail_area)
    return math.ceil(z_score**2 * sample_proportion * (1 - sample_proportion) / (margin_of_error ** 2))

def main():
    sample_proportion = 0.03
    margin_of_error = 0.01
    confidence_level = 95
    print('sample_proportion: ' + str(sample_proportion))
    print('margin_of_error: ' + str(margin_of_error))
    print('sample size for confidence level 95%: ' + str(sample_size_for_confidence_level(sample_proportion, margin_of_error, confidence_level)))

if __name__ == "__main__":
    main()
```

## output
```
sample_proportion: 0.03
margin_of_error: 0.01
sample size for confidence level 95%: 1118
```
