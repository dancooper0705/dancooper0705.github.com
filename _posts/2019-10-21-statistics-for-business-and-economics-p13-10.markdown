---
layout: post
title: "statistics-for-business-and-economics-p13-10"
date:  2019-10-21 13:00:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
The Business Week Global 1000 ranks companies on the basis of their market
value(Business Week, July 7, 1997). The following table shows the P/E ratios for
29 companies classifed as being in the finance economic sector. An industry code
of 1 indicates a banking firm, a code of 2 a financial services firm, and a code
of 3 an insurance firm. At the 0.05 level of significance, test whether the mean
price/earnings ratio is the same for these three groups of financial firms.
```

Company | Industry Code | P/E
--- | --- | ---
Citicorp | 1 | 15
NationsBank | 1 | 14
Wells Fargo | 1 | 25
First Union | 1 | 13
KeyCorp | 1 | 14
Chase Manhantan | 1 | 12
FIth Third Bancorp | 1 | 23
Bank of New York | 1 | 17
First Chicago NBD | 1 | 13
Mellon Bank | 1 | 16
Fleet Financial Group | 1 | 15
First Bank System | 1 | 16
American Express | 2 | 19
Travelers | 2 | 15
Merrill Lynch | 2 | 12
MBNA | 2 | 24
Cincinnati Financial | 2 | 19
Franklin Resources | 2 | 22
Fannie Mae | 2 | 17
American International Group | 3 | 21
Allstate | 3 | 14
Marsh & McLennan | 3 | 20
American General | 3 | 16
Cigna | 3 | 12
Linconln National | 3 | 13
AFLAC | 3 | 21
Equitable | 3 | 11
Chubb | 3 | 20
General Re | 3 | 15

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
    # test_data = [[165, 149, 156, 142], [174, 164, 180, 158], [169, 154, 161, 148]]
    test_data = [[15, 14, 25, 13, 14, 12, 23, 17, 13, 16, 15, 16], [19, 15, 12, 24, 19, 22, 17], [21, 14, 20, 16, 12, 13, 21, 11, 20, 15]]
    significance = 0.05
    query_analysis_of_variance(test_data, significance)

if __name__ == "__main__":
    main()
```

## output
```
test_data: [[15, 14, 25, 13, 14, 12, 23, 17, 13, 16, 15, 16], [19, 15, 12, 24, 19, 22, 17], [21, 14, 20, 16, 12, 13, 21, 11, 20, 15]]
treatment_number: 3
sample_number: [12, 7, 10]
sample_mean: [16.083333333333332, 18.285714285714285, 16.3]
sample_variance: [15.901515151515154, 16.571428571428573, 15.122222222222222]
sample_standard_deviation: [3.987670391533778, 4.0708019567928595, 3.8887301554906353]

overall_test_data: [15, 14, 25, 13, 14, 12, 23, 17, 13, 16, 15, 16, 19, 15, 12, 24, 19, 22, 17, 21, 14, 20, 16, 12, 13, 21, 11, 20, 15]
overall_sample_number: 29
overall_sample_mean: 16.689655172413794
overall_sample_variance: 15.507389162561577
overall_sample_standard_deviation: 3.937942249774821
overall_sum_of_square: 434.2068965517241

SSTR: 23.7617
MSTR: 11.8808
SSE: 410.4452
MSE: 15.7864
pooled_standard_deviation: 3.9732
dfn: 2.0000
dfd: 26.0000
statistics_test_f_score: 0.7526
critical_f_score: 3.3690
p_value: 0.4811

H0: the population of each treatment has the same mean
Ha: the population of each treatment doesn't have the same mean
test with statistics_test_f_score: 0.7526
reject H0 if statistics_test_f_score > 3.3690
do not reject H0
test with p_value: 0.4811
reject H0 if p_value < 0.0500
do not reject H0
```

## conclusion
ANOVA table

Source of Variation | Sum of Squares | Degree of Freedom | Mean Square | F
--- | --- | --- | --- | ---
Treatments | 23.7617 | 2 | 11.8808 | 0.7526
Error | 410.4452 | 26 | 15.7864 | /
Total | 434.2068965517241 | 28 | 15.507389162561577 | /
