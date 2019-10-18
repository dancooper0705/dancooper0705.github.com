---
layout: post
title: "statistics-for-business-and-economics-p12-04"
date:  2019-10-18 18:30:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
M&M/MARS, makers of M&M chocolate candies, conducted a national poll in which
more than ten million people indicated their preference for a new color. The
tally of this poll resulted in the replacemnt of tan-colored M&Ms with a new
blue color. In the brochure "color", made availbe by M7M/MARS Consumer Affairs,
the distribution of colors for the plain candies is as follows:
```

Brown | Yello | Red | Orange | Green | Blue
--- | --- | --- | --- | --- | ---
30% | 20%  | 20% | 10% | 10% | 10%

```
In a study reported in Chance(no. 4, 1996), samples of one-pound bags were used
to determine whether the reported percentages were indeed valid. The following
results were obtained for one sample of 506 plain candies.
```

Brown | Yello | Red | Orange | Green | Blue
--- | --- | --- | --- | --- | ---
177 | 135  | 79 | 41 | 36 | 38

```
Use alpha = 0.5 to determine whether these data support the percentages reported
by the company.
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
    sample_size = 506
    expected_freq = [0.3, 0.2, 0.2, 0.1, 0.1, 0.1]
    expected_freq = [sample_size * a for a in expected_freq]
    observed_freq = [177.0, 135.0, 79.0, 41.0, 36.0, 38.0]
    significance = 0.05

    print('observed_freq: ' + str(observed_freq))
    print('expected_freq: ' + str(expected_freq))
    print()

    query_multinormal_goodness_of_fit_test(observed_freq, expected_freq, significance)

if __name__ == "__main__":
    main()
```

## output
```
observed_freq: [177.0, 135.0, 79.0, 41.0, 36.0, 38.0]
expected_freq: [151.79999999999998, 101.2, 101.2, 50.6, 50.6, 50.6]

H0: freq = [151.79999999999998, 101.2, 101.2, 50.6, 50.6, 50.6]
Ha: freq != [151.79999999999998, 101.2, 101.2, 50.6, 50.6, 50.6]
significance: 0.0500
critical_chi2_score: 11.0705
test_statistics_chi2_score: 29.5138
p_value: 0.0000
test with critical_chi2_score:
reject H0 if test_statistics_chi2_score > 11.0705
reject H0
test with p-value:
reject H0 if p-value < 0.0500
reject H0
```
