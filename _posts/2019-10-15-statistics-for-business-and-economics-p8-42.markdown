---
layout: post
title: "statistics-for-business-and-economics-p8-42"
date:  2019-10-15 19:00:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
a survey of female executives donduced by Louis Harris & Associates showed that
33% of those surved rated their own company as an excellent place for women
executives to work(Working Woman, November 1994). Suppose Working Woman wants to
conduct an annual survey to monitor this proportion. With p = 0.33 as a planning
value for the population proportion, how many female executies should be
sampled for each of the following margins of error? Assume that all interval
esitmates are conducted at the 95% confidence level.
a. 10%
b. 5%
c. 2%
d. 1%
e. In general, what happens to the sample size as the margin of error decreases?
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
    sample_proportion = 0.33
    print('sample size for confidence level 95% with 10% margin error: ' + str(sample_size_for_confidence_level_of_population_proportion(sample_proportion, 0.1, 95)))
    print('sample size for confidence level 95% with 5% margin error: ' + str(sample_size_for_confidence_level_of_population_proportion(sample_proportion, 0.05, 95)))
    print('sample size for confidence level 95% with 2% margin error: ' + str(sample_size_for_confidence_level_of_population_proportion(sample_proportion, 0.02, 95)))
    print('sample size for confidence level 95% with 1% margin error: ' + str(sample_size_for_confidence_level_of_population_proportion(sample_proportion, 0.01, 95)))

if __name__ == "__main__":
    main()
```

## output
```
sample size for confidence level 95% with 10% margin error: 85
sample size for confidence level 95% with 5% margin error: 340
sample size for confidence level 95% with 2% margin error: 2124
sample size for confidence level 95% with 1% margin error: 8494
```

## discussion
```
As the margin of erro decreases, the required sample size increase. It implies that the more data we have, the sampling error will dercase.
```
