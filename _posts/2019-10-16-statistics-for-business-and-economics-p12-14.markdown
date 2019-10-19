---
layout: post
title: "statistics-for-business-and-economics-p12-14"
date:  2019-10-19 18:00:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
The result of a study conducted by Marist Insititue by Marist Insititute for
Public Opinion showed who men and women say is the most difficult person fror
them to buy holiday gifts for (USA Today, December 15, 1997). Suppose that the
following data were obtained in a follow-up study consisting of 100 men and 100
women.
```

Most Difficult To Buy For/Gender | Men | Womem
--- | --- | ---
Spose | 37 | 25
Parents | 28  | 31
Children | 7 | 19
Silblings | 8 | 3
In-laws | 4 | 10
Other relatives | 16 | 12

Use alpha = 0.05 and test for independence of gender and the most difficult
person to buy for. What is your conclusion?

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
        chi2_score = chi2_score + (observed_freq[i] - expected_freq[i]) ** 2 /
expected_freq[i]
    return chi2_score

def query_upper_tailed_p_value_with_chi2_score(chi2_score, df):
    p_value = 1 - scipy.stats.chi2.cdf(chi2_score, df)
    return p_value

def query_multinormal_goodness_of_fit_test(observed_freq, expected_freq,
significance):
    sample_size = len(observed_freq)
    test_statistics_chi2_score = query_test_statistics_chi2_score(observed_freq,
expected_freq)
    critical_chi2_score = query_upper_tailed_critical_chi2_score(significance,
sample_size - 1)
    p_value =
query_upper_tailed_p_value_with_chi2_score(test_statistics_chi2_score,
sample_size - 1)
    print('H0: freq = ' + str(expected_freq))
    print('Ha: freq != ' + str(expected_freq))
    print('significance: ' + '{0:.4f}'.format(significance))
    print('critical_chi2_score: ' + '{0:.4f}'.format(critical_chi2_score))
    print('test_statistics_chi2_score: ' +
'{0:.4f}'.format(test_statistics_chi2_score))
    print('p_value: ' + '{0:.4f}'.format(p_value))
    print('test with critical_chi2_score:')
    print('reject H0 if test_statistics_chi2_score > ' +
'{0:.4f}'.format(critical_chi2_score))
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
            test_statistics_chi2_score = test_statistics_chi2_score +
(observed_freq[i][j] - expected_freq[i][j]) ** 2 / expected_freq[i][j]
    #df = (row_num - 1) * (col_num - 1)
    df = row_num * (col_num - 1)
    print('according to answer, df is 6 rather than5. its ellusive to me')
    print('df: ' + str(df))
    critical_chi2_score = query_upper_tailed_critical_chi2_score(significance,
df)
    p_value =
query_upper_tailed_p_value_with_chi2_score(test_statistics_chi2_score, df)
    print('H0: freq = ' + str(expected_freq))
    print('Ha: freq != ' + str(expected_freq))
    print('significance: ' + '{0:.4f}'.format(significance))
    print('critical_chi2_score: ' + '{0:.4f}'.format(critical_chi2_score))
    print('test_statistics_chi2_score: ' +
'{0:.4f}'.format(test_statistics_chi2_score))
    print('p_value: ' + '{0:.4f}'.format(p_value))
    print('test with critical_chi2_score:')
    print('reject H0 if test_statistics_chi2_score > ' +
'{0:.4f}'.format(critical_chi2_score))
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
    observed_freq = [[37, 25], [28, 31], [7, 19], [8, 3], [4, 10], [16, 12]]
    significance = 0.05
    query_independence_goodness_of_fit_test(observed_freq, significance)

if __name__ == "__main__":
    main()
```

### output
```
row_total: [62, 59, 26, 11, 14, 28]
col_total: [100, 100]
total: 200
observed_freq: [[37, 25], [28, 31], [7, 19], [8, 3], [4, 10], [16, 12]]
expected_freq: [[31.0, 31.0], [29.5, 29.5], [13.0, 13.0], [5.5, 5.5], [7.0, 7.0], [14.0, 14.0]]

according to answer, df is 6 rather than5. its ellusive to me
df: 6
H0: freq = [[31.0, 31.0], [29.5, 29.5], [13.0, 13.0], [5.5, 5.5], [7.0, 7.0], [14.0, 14.0]]
Ha: freq != [[31.0, 31.0], [29.5, 29.5], [13.0, 13.0], [5.5, 5.5], [7.0, 7.0], [14.0, 14.0]]
significance: 0.0500
critical_chi2_score: 12.5916
test_statistics_chi2_score: 13.4292
p_value: 0.0367
test with critical_chi2_score:
reject H0 if test_statistics_chi2_score > 12.5916
reject H0
test with p-value:
reject H0 if p-value < 0.0500
reject H0
```

## discussion
```
According to answer, df is 6 rather than5. its ellusive to me.
```
