---
layout: post
title: "statistics-for-business-and-economics-p12-06"
date:  2019-10-18 18:40:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
Negative appeals have been recongnized as an effective method of persuasion in
advertising. A study in The Journal of Advertising(Summer 1997) reported the
results of a content analysis of guilt advertisments in 24 magazines. The number
of ads with guilt appeals that appeared in seclected magazine types follow.
```

Magazine Type | Number of Ads with Guilt Appeals
--- | ---
News and opinion | 20
General editorial | 15
Family-oriented | 30
Business/financial | 22
Female-oriented | 16
African-American | 12

```
Use alpha = 0.10 test to see whether there is a difference in the proportion of
ads with guilt appeals among the six types  of magazines.
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
    observed_freq = [20, 15, 30, 22, 16, 12]
    sample_size = np.sum(observed_freq)
    expected_freq = [sample_size / 6] * 6
    significance = 0.10

    print('observed_freq: ' + str(observed_freq))
    print('expected_freq: ' + str(expected_freq))
    print()

    query_multinormal_goodness_of_fit_test(observed_freq, expected_freq, significance)

if __name__ == "__main__":
    main()
```

### output
```
observed_freq: [20, 15, 30, 22, 16, 12]
expected_freq: [19.166666666666668, 19.166666666666668, 19.166666666666668, 19.166666666666668, 19.166666666666668, 19.166666666666668]

H0: freq = [19.166666666666668, 19.166666666666668, 19.166666666666668, 19.166666666666668, 19.166666666666668, 19.166666666666668]
Ha: freq != [19.166666666666668, 19.166666666666668, 19.166666666666668, 19.166666666666668, 19.166666666666668, 19.166666666666668]
significance: 0.1000
critical_chi2_score: 9.2364
test_statistics_chi2_score: 10.6870
p_value: 0.0580
test with critical_chi2_score:
reject H0 if test_statistics_chi2_score > 9.2364
reject H0
test with p-value:
reject H0 if p-value < 0.1000
reject H0
```
