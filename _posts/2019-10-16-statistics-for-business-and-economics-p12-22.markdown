---
layout: post
title: "statistics-for-business-and-economics-p12-22"
date:  2019-10-20 15:30:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
The number of automobile accidents per day in a particular city is believed to
have a Poisson distribution. A sample of 80 days during the past year give the
data listed below. Do these data support the belief that the number of accidents
per day has a Poisson distributino? Use alpha = 0.05.
```

Number of Accidents | Observed Frequency(days)
--- | ---
0 | 34
1 | 25
2 | 11
3 |  7
4 |  3

## source
```python
import math
import scipy.stats
import numpy as np

def query_upper_tailed_critical_chi2_score(significance, df):
    upper_tail_area = significance
    chi2_score = scipy.stats.chi2.ppf(1 - upper_tail_area, df)
    return chi2_score

def query_test_statistics_chi2_score(observed_freq, expected_freq):
    chi2_score = 0
    n = len(observed_freq)
    for i in range(n):
        chi2_score = chi2_score + (observed_freq[i] - expected_freq[i]) ** 2 / expected_freq[i]
    return chi2_score

def query_upper_tailed_p_value_with_chi2_score(chi2_score, df):
    p_value = 1 - scipy.stats.chi2.cdf(chi2_score, df)
    return p_value

def query_multinormal_goodness_of_fit_test(observed_freq, expected_freq, significance):
    sample_size = len(observed_freq)
    test_statistics_chi2_score = query_test_statistics_chi2_score(observed_freq, expected_freq)
    critical_chi2_score = query_upper_tailed_critical_chi2_score(significance, sample_size - 1)
    p_value = query_upper_tailed_p_value_with_chi2_score(test_statistics_chi2_score, sample_size - 1)
    print('H0: freq = ' + str(expected_freq))
    print('Ha: freq != ' + str(expected_freq))
    print('significance: ' + '{0:.4f}'.format(significance))
    print('critical_chi2_score: ' + '{0:.4f}'.format(critical_chi2_score))
    print('test_statistics_chi2_score: ' + '{0:.4f}'.format(test_statistics_chi2_score))
    print('p_value: ' + '{0:.4f}'.format(p_value))
    print('test with critical_chi2_score:')
    print('reject H0 if test_statistics_chi2_score > ' + '{0:.4f}'.format(critical_chi2_score))
    if test_statistics_chi2_score > critical_chi2_score:
        print('reject H0')
    else:
        print('do not reject H0')
    print('test with p-value:')
    print('reject H0 if p-value < ' + '{0:.4f}'.format(significance))
    if p_value < significance:
        print('reject H0')
    else:
        print('do not reject H0')

def query_independence_goodness_of_fit_test(observed_freq, significance):
    row_num = len(observed_freq)
    col_num = len(observed_freq[0])
    row_total = [0] * row_num
    col_total = [0] * col_num
    total = 0
    for i in range(row_num):
        for j in range(col_num):
            row_total[i] = row_total[i] + observed_freq[i][j]
            col_total[j] = col_total[j] + observed_freq[i][j]
            total += observed_freq[i][j]
    print('row_total: ' + str(row_total))
    print('col_total: ' + str(col_total))
    print('total: ' + str(total))
    expected_freq =  [[0]*col_num for i in range(row_num)]
    for i in range(row_num):
        for j in range(col_num):
            expected_freq[i][j] = (row_total[i] * col_total[j] / total)
    print('observed_freq: ' + str(observed_freq))
    print('expected_freq: ' + str(expected_freq))
    print()
    test_statistics_chi2_score = 0
    for i in range(row_num):
        for j in range(col_num):
            test_statistics_chi2_score = test_statistics_chi2_score + (observed_freq[i][j] - expected_freq[i][j]) ** 2 / expected_freq[i][j]
    df = (row_num - 1) * (col_num - 1)
    critical_chi2_score = query_upper_tailed_critical_chi2_score(significance, df)
    p_value = query_upper_tailed_p_value_with_chi2_score(test_statistics_chi2_score, df)
    print('H0: freq = ' + str(expected_freq))
    print('Ha: freq != ' + str(expected_freq))
    print('df: ' + str(df))
    print('significance: ' + '{0:.4f}'.format(significance))
    print('critical_chi2_score: ' + '{0:.4f}'.format(critical_chi2_score))
    print('test_statistics_chi2_score: ' + '{0:.4f}'.format(test_statistics_chi2_score))
    print('p_value: ' + '{0:.4f}'.format(p_value))
    print('test with critical_chi2_score:')
    print('reject H0 if test_statistics_chi2_score > ' + '{0:.4f}'.format(critical_chi2_score))
    if test_statistics_chi2_score > critical_chi2_score:
        print('reject H0')
    else:
        print('do not reject H0')
    print('test with p-value:')
    print('reject H0 if p-value < ' + '{0:.4f}'.format(significance))
    if p_value < significance:
        print('reject H0')
    else:
        print('do not reject H0')

def query_poisson_distribution_goodness_of_fit_test(observed_freq, significance):
    total_freq = np.sum(observed_freq)
    sample_mean = np.sum([i * observed_freq[i] for i in range(len(observed_freq))]) / total_freq
    expected_freq = [0] * len(observed_freq)
    for i in range(len(observed_freq)):
        expected_freq[i] = total_freq * scipy.stats.poisson.pmf(i, sample_mean)
    expected_freq[-1] = total_freq - np.sum(expected_freq[:-1])
    print('total freq: ' + '{0:.4f}'.format(total_freq))
    print('sample_mean: ' + '{0:.4f}'.format(sample_mean))
    print('observed_freq: ' + str(observed_freq))
    print('expected_freq: ' + str(expected_freq))
    print()
    observed_freq[-2] = observed_freq[-2] + observed_freq[-1]
    observed_freq = observed_freq[:-1]
    expected_freq[-2] = expected_freq[-2] + expected_freq[-1]
    expected_freq = expected_freq[:-1]
    print('adjust freq due to some freq < 5')
    print('observed_freq: ' + str(observed_freq))
    print('expected_freq: ' + str(expected_freq))
    print()
    test_statistics_chi2_score = 0
    for i in range(len(observed_freq)):
        test_statistics_chi2_score = test_statistics_chi2_score + (observed_freq[i] - expected_freq[i]) ** 2 / expected_freq[i]
    df = len(observed_freq) - 2
    critical_chi2_score = query_upper_tailed_critical_chi2_score(significance, df)
    p_value = query_upper_tailed_p_value_with_chi2_score(test_statistics_chi2_score, df)
    print('H0: freq = ' + str(expected_freq))
    print('Ha: freq != ' + str(expected_freq))
    print('df: ' + str(df))
    print('significance: ' + '{0:.4f}'.format(significance))
    print('critical_chi2_score: ' + '{0:.4f}'.format(critical_chi2_score))
    print('test_statistics_chi2_score: ' + '{0:.4f}'.format(test_statistics_chi2_score))
    print('p_value: ' + '{0:.4f}'.format(p_value))
    print('test with critical_chi2_score:')
    print('reject H0 if test_statistics_chi2_score > ' + '{0:.4f}'.format(critical_chi2_score))
    if test_statistics_chi2_score > critical_chi2_score:
        print('reject H0')
    else:
        print('do not reject H0')
    print('test with p-value:')
    print('reject H0 if p-value < ' + '{0:.4f}'.format(significance))
    if p_value < significance:
        print('reject H0')
    else:
        print('do not reject H0')

def main():
    observed_freq = [34, 25, 11, 7, 3]
    significance = 0.05
    query_poisson_distribution_goodness_of_fit_test(observed_freq, significance)

if __name__ == "__main__":
    main()
```

## output
```
total freq: 80.0000
sample_mean: 1.0000
observed_freq: [34, 25, 11, 7, 3]
expected_freq: [29.430355293715387, 29.430355293715387, 14.715177646857692, 4.905059215619231, 1.5190525500922973]

adjust freq due to some freq < 5
observed_freq: [34, 25, 11, 10]
expected_freq: [29.430355293715387, 29.430355293715387, 14.715177646857692, 6.424111765711529]

H0: freq = [29.430355293715387, 29.430355293715387, 14.715177646857692, 6.424111765711529]
Ha: freq != [29.430355293715387, 29.430355293715387, 14.715177646857692, 6.424111765711529]
df: 2
significance: 0.0500
critical_chi2_score: 5.9915
test_statistics_chi2_score: 4.3049
p_value: 0.1162
test with critical_chi2_score:
reject H0 if test_statistics_chi2_score > 5.9915
do not reject H0
test with p-value:
reject H0 if p-value < 0.0500
do not reject H0
```

## conclusion
```
Statistics test doesn't reject the claim that the data fit poisson distribution.
```
