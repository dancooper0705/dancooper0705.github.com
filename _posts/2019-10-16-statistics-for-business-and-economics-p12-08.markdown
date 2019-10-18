---
layout: post
title: "statistics-for-business-and-economics-p12-08"
date:  2019-10-18 18:50:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
Grade distribution gudielines for a statistics course at a mojor university are:
10% A, 30% B, 40% C, 15% D, 5% F. A sample of 120 statistics grades at the end
of a semester showed 18 As, 30 Bs, 40 cs, 22 Ds, and 10 Fs. Use alpha = 0.05 and
test whether the actual grades deviate significanly from the grade distribution
guidelines.
```

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

def main():
    expected_freq = [0.1, 0.3, 0.4, 0.15, 0.05]
    observed_freq = [18, 30, 40, 22, 10]
    total = np.sum(observed_freq)
    expected_freq = [total * a for a in expected_freq]
    significance = 0.05

    print('observed_freq: ' + str(observed_freq))
    print('expected_freq: ' + str(expected_freq))
    print()

    query_multinormal_goodness_of_fit_test(observed_freq, expected_freq, significance)

if __name__ == "__main__":
    main()
```

### output
```
observed_freq: [18, 30, 40, 22, 10]
expected_freq: [12.0, 36.0, 48.0, 18.0, 6.0]

H0: freq = [12.0, 36.0, 48.0, 18.0, 6.0]
Ha: freq != [12.0, 36.0, 48.0, 18.0, 6.0]
significance: 0.0500
critical_chi2_score: 9.4877
test_statistics_chi2_score: 8.8889
p_value: 0.0639
test with critical_chi2_score:
reject H0 if test_statistics_chi2_score > 9.4877
do not reject H0
test with p-value:
reject H0 if p-value < 0.0500
do not reject H0
```
