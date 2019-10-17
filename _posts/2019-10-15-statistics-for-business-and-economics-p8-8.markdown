---
layout: post
title: "statistics-for-business-and-economics-p8-8"
date:  2019-10-15 10:00:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
8. In a study of student loan subsidies, the Department of Education reported
that four-year Stafford Loan borrowers will owe an average of $12,168 upon
graduation(USA Today, April 5, 1995). Assume that this average or mean amount
owed its based on a sample of 480 student loans and that the population standard
deviation for the amount owed upon graduation is &2200.
a. Develop a 90% confidence interval estimate of the population mean amount
owed.
b. Develop a 95% confidence interval estimate of the population mean amount
owed.
c. Develop a 99% confidence interval estimate of the population mean amount
owed.
d. Discuss what happens to the width  of the confidence interval as the
confidence level is incrased. Does this seem reasonable? Explain.
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
    sample_size = 480
    sample_mean = 12168
    sample_standard_deviation = 2200
    print('90% confidence interval for population mean: ' + ' to '.join('{0:.0f}'.format(a) for a in confidence_interval_of_population_mean(sample_size, sample_mean, sample_standard_deviation, 90)))
    print('95% confidence interval for population mean: ' + ' to '.join('{0:.0f}'.format(a) for a in confidence_interval_of_population_mean(sample_size, sample_mean, sample_standard_deviation, 95)))
    print('99% confidence interval for population mean: ' + ' to '.join('{0:.0f}'.format(a) for a in confidence_interval_of_population_mean(sample_size, sample_mean, sample_standard_deviation, 99)))

if __name__ == "__main__":
    main()
```

## output
```
90% confidence interval for population mean: 12003 to 12333
95% confidence interval for population mean: 11971 to 12365
99% confidence interval for population mean: 11909 to 12427
```

## discuss
```
As the output shows, the width of confidence interval is increased as the
confidence level is increased. It make sense since a wider confidence interval
is more likely to include the real polulation mean. To put it in another way, if
a interval estimate with higher confidence level is required, then this
esitimate is supposed to be wider to be more likely to include the real
population mean.
```
