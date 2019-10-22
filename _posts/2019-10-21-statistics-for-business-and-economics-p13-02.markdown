---
layout: post
title: "statistics-for-business-and-economics-p13-02"
date:  2019-10-21 10:00:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
Four observations were selected from each of three populatinos. The data
obtained follow.
```

Observation | Sample 1 | Sample 2 | Sample 3
--- | --- | --- | ---
1 | 165 | 174 | 169
2 | 149 | 164 | 154
3 | 156 | 180 | 161
4 | 142 | 158 | 148
Sample mean | 153 | 169 | 158
Sample variance | 96.67 | 97.33 | 82.00

```
a. Compute the between-treatments estimate of variance.
b. Compute the within-treatments estimate of variance.
c. At the alpha = 0.05 level of significance, can we reject the null hypothesis
that the three population means are equal? Explain.
d. Set up the ANOVA table for this population.
```

## source
```python
import math
import scipy.stats
import numpy as np

def query_analysis_of_variance(test_data, significance):
    treatment_number = len(test_data)
    sample_number = [np.array(data).size for data in test_data]
    sample_mean = [np.mean(data) for data in test_data]
    sample_variance = [np.var(data, ddof=1) for data in test_data]
    sample_standard_deviation = [np.std(data, ddof=1) for data in test_data]
    print('test_data: ' + str(test_data))
    print('treatment_number: ' +  str(treatment_number))
    print('sample_number: ' + str(sample_number))
    print('sample_mean: ' + str(sample_mean))
    print('sample_variance: ' + str(sample_variance))
    print('sample_standard_deviation: ' + str(sample_standard_deviation))
    print()
    overall_test_data = [a for data in test_data for a in data]
    overall_sample_number = np.array(overall_test_data).size
    overall_sample_mean = np.mean(np.array(overall_test_data))
    overall_sample_variance = np.var(np.array(overall_test_data), ddof=1)
    overall_sample_standard_deviation = np.std(np.array(overall_test_data), ddof=1)
    print('overall_test_data: ' + str(overall_test_data))
    print('overall_sample_number: ' + str(overall_sample_number))
    print('overall_sample_mean: ' + str(overall_sample_mean))
    print('overall_sample_variance: ' + str(overall_sample_variance))
    print('overall_sample_standard_deviation: ' + str(overall_sample_standard_deviation))
    print('overall_sum_of_square: ' + str(overall_sample_variance * (overall_sample_number - 1)))
    print()
    SSTR = np.sum([sample_number[i] * (sample_mean[i] - overall_sample_mean) ** 2 for i in range(treatment_number)])
    MSTR = SSTR / (treatment_number - 1)
    SSE = np.sum([(sample_number[i] - 1) * sample_variance[i] for i in range(treatment_number)])
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
    # test_data = [[15, 14, 25, 13, 14, 12, 23, 17, 13, 16, 15, 16], [19, 15, 12, 24, 19, 22, 17], [21, 14, 20, 16, 12, 13, 21, 11, 20, 15]]
    test_data = [[165, 149, 156, 142], [174, 164, 180, 158], [169, 154, 161, 148]]
    significance = 0.05
    query_analysis_of_variance(test_data, significance)

if __name__ == "__main__":
    main()
```

## output
```
test_data: [[165, 149, 156, 142], [174, 164, 180, 158], [169, 154, 161, 148]]
treatment_number: 3
sample_number: [4, 4, 4]
sample_mean: [153.0, 169.0, 158.0]
sample_variance: [96.66666666666667, 97.33333333333333, 82.0]
sample_standard_deviation: [9.83192080250175, 9.865765724632494, 9.055385138137417]

overall_test_data: [165, 149, 156, 142, 174, 164, 180, 158, 169, 154, 161, 148]
overall_sample_number: 12
overall_sample_mean: 160.0
overall_sample_variance: 124.0
overall_sample_standard_deviation: 11.135528725660043
overall_sum_of_square: 1364.0

SSTR: 536.0000
MSTR: 268.0000
SSE: 828.0000
MSE: 92.0000
pooled_standard_deviation: 9.5917
dfn: 2.0000
dfd: 9.0000
statistics_test_f_score: 2.9130
critical_f_score: 4.2565
p_value: 0.1058

H0: the population of each treatment has the same mean
Ha: the population of each treatment doesn't have the same mean
test with statistics_test_f_score: 2.9130
reject H0 if statistics_test_f_score > 4.2565
do not reject H0
test with p_value: 0.1058
reject H0 if p_value < 0.0500
do not reject H0
```

## conclusion
ANOVA table

Source of Variation | Sum of Squares | Degree of Freedom | Mean Square | F
--- | --- | --- | --- | ---
Treatments | 536 | 2 | 268 | 2.9130
Error | 828 | 9 | 92 | /
Total | 1364 | 11 | 124 | /
