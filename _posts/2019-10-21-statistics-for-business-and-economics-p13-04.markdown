---
layout: post
title: "statistics-for-business-and-economics-p13-04"
date:  2019-10-21 11:00:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
A random sample of 16 observations was selected from each of four populations.
A portion of the ANOVA table follows.
```

Source of Variation | Sum of Squares | Degrees of Freedom | Mean Square | F
--- | --- | --- | --- | ---
Treamtments | | | 400 |
Error | | | | 
Total | 1500 | | |

```
a. Provide the missing entries for the ANOVA table.
b. At the alpha = 0.05 levle of significance, can we reject the null hypothesis
that the mean of the four poulations are equal?
```

## source
```python
import math
import scipy.stats
import numpy as np

def query_analysis_of_variance(significance):
    treatment_number = 4
    sample_number = [16] * treatment_number
    print('treatment_number: ' +  str(treatment_number))
    print('sample_number: ' + str(sample_number))
    print()
    overall_sum_of_squares = 1500
    overall_sample_number = np.sum(sample_number)
    overall_sample_variance = overall_sum_of_squares / (overall_sample_number - 1)
    overall_sample_standard_deviation = math.sqrt(overall_sample_variance)
    print('overall_sample_number: ' + str(overall_sample_number))
    print('overall_sample_variance: ' + str(overall_sample_variance))
    print('overall_sample_standard_deviation: ' + str(overall_sample_standard_deviation))
    print('overall_sum_of_square: ' + str(overall_sample_variance * (overall_sample_number - 1)))
    print()
    MSTR = 400
    SSTR = MSTR * (treatment_number - 1)
    SSE = overall_sum_of_squares - SSTR
    MSE = SSE / (overall_sample_number - treatment_number)
    pooled_standard_deviation = math.sqrt(MSE)
    dfn = treatment_number - 1
    dfd = overall_sample_number - treatment_number
    statistics_test_f_score = MSTR / MSE
    critical_f_score = scipy.stats.f.ppf(1 - significance, dfn, dfd)
    p_value = 1.0 - scipy.stats.f.cdf(statistics_test_f_score, dfn, dfd)
    print('SSTR: ' + '{0:.4f}'.format(SSTR))
    print('MSTR: ' + '{0:.4f}'.format(MSTR))
    print('SSE: ' + '{0:.4f}'.format(SSE))
    print('MSE: ' + '{0:.4f}'.format(MSE))
    print('pooled_standard_deviation: ' + '{0:.4f}'.format(pooled_standard_deviation))
    print('dfn: ' + '{0:.4f}'.format(dfn))
    print('dfd: ' + '{0:.4f}'.format(dfd))
    print('statistics_test_f_score: ' + '{0:.4f}'.format(statistics_test_f_score))
    print('critical_f_score: ' + '{0:.4f}'.format(critical_f_score))
    print('p_value: ' + '{0:.4f}'.format(p_value))
    print()
    print('H0: the population of each treatment has the same mean')
    print('Ha: the population of each treatment doesn\'t have the same mean')
    print('test with statistics_test_f_score: ' + '{0:.4f}'.format(statistics_test_f_score))
    print('reject H0 if statistics_test_f_score > ' + '{0:.4f}'.format(critical_f_score))
    if statistics_test_f_score > critical_f_score:
        print('reject H0')
    else:
        print('do not reject H0')
    print('test with p_value: ' + '{0:.4f}'.format(p_value))
    print('reject H0 if p_value < ' + '{0:.4f}'.format(significance))
    if p_value < significance:
        print('reject H0')
    else:
        print('do not reject H0')

def main():
    significance = 0.05
    query_analysis_of_variance(significance)

if __name__ == "__main__":
    main()
```

## output
```
treatment_number: 4
sample_number: [16, 16, 16, 16]

overall_sample_number: 64
overall_sample_variance: 23.80952380952381
overall_sample_standard_deviation: 4.879500364742666
overall_sum_of_square: 1500.0

SSTR: 1200.0000
MSTR: 400.0000
SSE: 300.0000
MSE: 5.0000
pooled_standard_deviation: 2.2361
dfn: 3.0000
dfd: 60.0000
statistics_test_f_score: 80.0000
critical_f_score: 2.7581
p_value: 0.0000

H0: the population of each treatment has the same mean
Ha: the population of each treatment doesn't have the same mean
test with statistics_test_f_score: 80.0000
reject H0 if statistics_test_f_score > 2.7581
reject H0
test with p_value: 0.0000
reject H0 if p_value < 0.0500
reject H0
```

## conclusion
ANOVA table

Source of Variation | Sum of Squares | Degree of Freedom | Mean Square | F
--- | --- | --- | --- | ---
Treatments | 1200 | 3 | 400 | 80.0000
Error | 300 | 60 | 5 | /
Total | 1500 | 63 | 23.80952380952381 | /
