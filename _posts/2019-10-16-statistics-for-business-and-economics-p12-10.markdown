---
layout: post
title: "statistics-for-business-and-economics-p12-10"
date:  2019-10-18 20:00:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
Below is a 3 x 3 contingency table with observed frequency table with observed
frequencies for a sample of 240. Test for independence of the row and column
variables using the x^2 test with alpha = 0.05.
```

Row Variable/Column variable | A | B | C
--- | --- | --- | ---
P | 20 | 30 | 20
Q | 30 | 60 | 25
R | 10 | 15 | 30

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
    observed_freq = [[20, 30, 20], [30, 60, 25], [10, 15, 30]]
    significance = 0.05
    query_independence_goodness_of_fit_test(observed_freq, significance)

if __name__ == "__main__":
    main()
```

### output
```
row_total: [70, 115, 55]
col_total: [60, 105, 75]
total: 240
observed_freq: [[20, 30, 20], [30, 60, 25], [10, 15, 30]]
expected_freq: [[17.5, 30.625, 21.875], [28.75, 50.3125, 35.9375], [13.75, 24.0625, 17.1875]]

H0: freq = [[17.5, 30.625, 21.875], [28.75, 50.3125, 35.9375], [13.75, 24.0625, 17.1875]]
Ha: freq != [[17.5, 30.625, 21.875], [28.75, 50.3125, 35.9375], [13.75, 24.0625, 17.1875]]
significance: 0.0500
critical_chi2_score: 9.4877
test_statistics_chi2_score: 19.7661
p_value: 0.0006
test with critical_chi2_score:
reject H0 if test_statistics_chi2_score > 9.4877
reject H0
test with p-value:
reject H0 if p-value < 0.0500
reject H0
```
