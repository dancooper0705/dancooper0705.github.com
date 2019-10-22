---
layout: post
title: "statistics-for-business-and-economics-p13-06"
date:  2019-10-21 11:00:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
To test whether the mean time needed to mix a batch of material is the same for
machines producted by three manufactures, the Jacobs Chemical Company obtained
the data to test whether the populations mean times for mixing a batch of
material differ for the three manufactures. Use alpha = 0.05.
```

Manufacture 1 | Manufacture 2 | Manufacture 3
--- | --- | ---
20 | 28 | 20
26 | 26 | 19
24 | 31 | 23
22 | 27 | 22


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
    overall_sample_number = np.array(test_data).size
    overall_sample_mean = np.mean(np.array(test_data))
    overall_sample_variance = np.var(np.array(test_data), ddof=1)
    overall_sample_standard_deviation = np.std(np.array(test_data), ddof=1)
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
    test_data = [[20, 26, 24, 22], [28, 26, 31, 27], [20, 19, 23, 22]]
    #test_data = [[85, 75, 82, 76, 71, 85], [71, 75, 73, 74, 69, 82], [59, 64, 62, 69, 75, 67]]
    significance = 0.05
    query_analysis_of_variance(test_data, significance)

if __name__ == "__main__":
    main()
```

## output
```
test_data: [[20, 26, 24, 22], [28, 26, 31, 27], [20, 19, 23, 22]]
treatment_number: 3
sample_number: [4, 4, 4]
sample_mean: [23.0, 28.0, 21.0]
sample_variance: [6.666666666666667, 4.666666666666667, 3.3333333333333335]
sample_standard_deviation: [2.581988897471611, 2.160246899469287, 1.8257418583505538]

overall_sample_number: 12
overall_sample_mean: 24.0
overall_sample_variance: 13.454545454545455
overall_sample_standard_deviation: 3.668043818514912
overall_sum_of_square: 148.0

SSTR: 104.0000
MSTR: 52.0000
SSE: 44.0000
MSE: 4.8889
pooled_standard_deviation: 2.2111
dfn: 2.0000
dfd: 9.0000
statistics_test_f_score: 10.6364
critical_f_score: 4.2565
p_value: 0.0043

H0: the population of each treatment has the same mean
Ha: the population of each treatment doesn't have the same mean
test with statistics_test_f_score: 10.6364
reject H0 if statistics_test_f_score > 4.2565
reject H0
test with p_value: 0.0043
reject H0 if p_value < 0.0500
reject H0
```

## conclusion
ANOVA table

Source of Variation | Sum of Squares | Degree of Freedom | Mean Square | F
--- | --- | --- | --- | ---
Treatments | 104 | 2 | 52 | 10.6364
Error | 44 | 9 | 4.8889 | /
Total | 148 | 11 | 13.454545454545455 | /
