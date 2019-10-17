---
layout: post
title: "statistics-for-business-and-economics-p8-38"
date:  2019-10-15 18:10:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
Audience profile data collected at the ESPN Sportszone web site showed that 26%
of the users were women(USA Today, January 20, 1998). Assume that this
percentage was based on a sample of 400 users.
a. Using 95% confidence, what is the margin of error assiciated with the
estimated proportino of users who are women?
b. What is the 95% confidence interval for the population proportion of ESPN
Sportszone web site users who are women?
c. How large a sample should be taken if the desired margin of error is 3%?
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
    sample_size = 400
    sample_proportion = 0.26
    print('sample_proportion: ' + '{0:.4f}'.format(sample_proportion))
    confidence_interval = confidence_interval_of_population_proportion(sample_size, sample_proportion, 95)
    margin_of_error = (confidence_interval[1] - confidence_interval[0]) / 2
    print('95% confidence interval for population proportion has margin of error: ' + '{0:.4f}'.format(margin_of_error))
    print('95% confidence interval for population proportion: ' + ' to '.join('{0:.4f}'.format(a) for a in confidence_interval))
    print('sample size for confidence level 95% with 0.03 margin error: ' + str(sample_size_for_confidence_level_of_population_proportion(sample_proportion, 0.03, 95)))

if __name__ == "__main__":
    main()
```

## output
```
sample_proportion: 0.2600
95% confidence interval for population proportion has margin of error: 0.0430
95% confidence interval for population proportion: 0.2170 to 0.3030
sample size for confidence level 95% with 0.03 margin error: 822
```
