---
layout: post
title: "statistics-for-business-and-economics-p8-32"
date:  2019-10-15 17:00:00  +0800
categories: [dev]
tags: [python, statistics]
---

## question
```
A simple random sample of 800 units generating a sample propotion p = 0.70
a. Provide a 90% confidence interval for the population propotion.
b. Provide a 95% confidence interval for the population propotion.
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

def main():
    print('p = sample proportion, it works when n*p >= 5 && n*(1-p)>=5')
    sample_size = 800
    sample_proportion = 0.7
    print('sample_size: ' + str(sample_size))
    print('sample_proportion: ' + str(sample_proportion))
    print('90% confidence interval for population proportion: ' + ' to '.join('{0:.4f}'.format(a) for a in confidence_interval_of_population_proportion(sample_size, sample_proportion, 90)))
    print('95% confidence interval for population proportion: ' + ' to '.join('{0:.4f}'.format(a) for a in confidence_interval_of_population_proportion(sample_size, sample_proportion, 95)))

if __name__ == "__main__":
    main()
```

## output
```
sample_size: 800
sample_proportion: 0.7
90% confidence interval for population proportion: 0.6734 to 0.7266
95% confidence interval for population proportion: 0.6682 to 0.7318
```
