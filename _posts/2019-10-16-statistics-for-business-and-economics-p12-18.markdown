---
layout: post
title: "statistics-for-business-and-economics-p12-18"
date:  2019-10-20 14:00:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
A study of educational levles of voters and their political party affilication
yielded the following results.
```

Educational Level/Party Affilication | Democratic | Republican | Independent
--- | --- | --- | ---
Did not  complete high school | 40 | 20 | 10
High school degree | 30 | 35 | 15
College degree | 30 | 45 | 25

Use alpha = 0.01 and determine whether party affilication is independent of the
education level of the voters.

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

def main():
    observed_freq = [[40, 20, 10], [30, 35, 15], [30, 45, 25]]
    significance = 0.01
    query_independence_goodness_of_fit_test(observed_freq, significance)

if __name__ == "__main__":
    main()
```

## output
```
row_total: [70, 80, 100]
col_total: [100, 100, 50]
total: 250
observed_freq: [[40, 20, 10], [30, 35, 15], [30, 45, 25]]
expected_freq: [[28.0, 28.0, 14.0], [32.0, 32.0, 16.0], [40.0, 40.0, 20.0]]

H0: freq = [[28.0, 28.0, 14.0], [32.0, 32.0, 16.0], [40.0, 40.0, 20.0]]
Ha: freq != [[28.0, 28.0, 14.0], [32.0, 32.0, 16.0], [40.0, 40.0, 20.0]]
df: 4
significance: 0.0100
critical_chi2_score: 13.2767
test_statistics_chi2_score: 13.4152
p_value: 0.0094
test with critical_chi2_score:
reject H0 if test_statistics_chi2_score > 13.2767
reject H0
test with p-value:
reject H0 if p-value < 0.0100
reject H0
```

## conclusion
```
Statistics test rejects the cliam that thatparty affilication is independent of
the education level of the voters.
```
