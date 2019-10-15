---
layout: post
title: "statistics-for-business-and-economics-p8-40"
date:  2019-10-15 18:10:00  +0800
categories: [dev]
tags: [python, statistics]
---

## question
```
Ferrel Calvillo Communications conducted a national survey of 902 women golfers
to study how women golfers view themselves as begin treated at golf curses(USA
Today, June 3, 1997). The survey found that 397 women were satisfied with the
availability of tee times, 307 women were satisfied with membership policies,
and 234 women were satisfied with locker room facilities.
a. Develop the point estimate of thhe population proportion and the 95%
cnofidence interval for each of the three survey questions.
b. The USA Today article about the survey was entitled: Survey: Women Get Subpar
Treatment. Do you feel that the satistical information provided in part(a)
justifies this title?
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
    sample_size = 902
    sample_proportion_tea = 397 / sample_size
    sample_proportion_membership = 307 / sample_size
    sample_proportion_locker = 234 / sample_size

    print('point estimate of populatoin proportion satified with tea time: ' + '{0:.4f}'.format(sample_proportion_tea))
    print('point estimate of populatoin proportion satified with membership policies: ' + '{0:.4f}'.format(sample_proportion_membership))
    print('point estimate of populatoin proportion satified with locker room facilities: ' + '{0:.4f}'.format(sample_proportion_locker))
    print('95% confidence interval for population proportion satisfied with tea time: ' + ' to '.join('{0:.4f}'.format(a) for a in confidence_interval_of_population_proportion(sample_size, sample_proportion_tea, 95)))
    print('95% confidence interval for population proportion satisfied with membership policies: ' + ' to '.join('{0:.4f}'.format(a) for a in confidence_interval_of_population_proportion(sample_size, sample_proportion_membership, 95)))
    print('95% confidence interval for population proportion satisfied with locker room facilities: ' + ' to '.join('{0:.4f}'.format(a) for a in confidence_interval_of_population_proportion(sample_size, sample_proportion_locker, 95)))

if __name__ == "__main__":
    main()
```

## output
```
point estimate of populatoin proportion satified with tea time: 0.4401
point estimate of populatoin proportion satified with membership policies: 0.3404
point estimate of populatoin proportion satified with locker room facilities: 0.2594
95% confidence interval for population proportion satisfied with tea time: 0.4077 to 0.4725
95% confidence interval for population proportion satisfied with membership policies: 0.3094 to 0.3713
95% confidence interval for population proportion satisfied with locker room facilities: 0.2308 to 0.2880
```

## discussion
```
It's reasonable since the population proportion of satification is less than 0.5.
```
