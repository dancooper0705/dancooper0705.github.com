---
layout: post
title: "statistics-for-business-and-economics-p11-10"
date:  2019-10-18 15:10:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
The average useful life of a VCR is six year with a standard deviation of 0.75
years (Consumer Reports 1995 Buying Gudide). A sample of the useful life of 30
television sets provided a sample standard deviation of two years. Construct a
hypothesis test that can be used to determine whether the standard deviation of
the useful life of a television sets is significanly greater than the standard
deviation of the useful life of VCR. With a 0.05 levle of significance, what is
you conclusion?
```

## source
```python
import math
import scipy.stats
import numpy as np

def query_confidence_interval_populatoin_variance(sample_size, sample_variance, confidence_level):
    df = sample_size - 1
    confidence_coefficient = confidence_level / 100
    alpha_level = 1 - confidence_coefficient
    return [(sample_size - 1) * sample_variance / scipy.stats.chi2.ppf(1 - alpha_level / 2, df),
            (sample_size - 1) * sample_variance / scipy.stats.chi2.ppf(alpha_level / 2, df)];

def query_two_tailed_critical_chi2_score(significance, df):
    tail_area = significance / 2
    return [scipy.stats.chi2.ppf(tail_area, df), scipy.stats.chi2.ppf(1 - tail_area, df)]

def query_upper_tailed_critical_chi2_score(significance, df):
    upper_tail_area = significance
    chi2_score = scipy.stats.chi2.ppf(1 - upper_tail_area, df)
    return chi2_score

def query_lower_tailed_critical_chi2_score(significance, df):
    lower_tail_area = significance
    chi2_score = scipy.stats.chi2.ppf(lower_tail_area, df)
    return chi2_score

def query_sample_variance_test_statistics_chi2_score(population_variance, sample_size, sample_variance):
    score = (sample_size - 1) * sample_variance / population_variance
    return score

def query_two_tailed_chi2_test(hypothesis_variance, sample_size, sample_variance, significance):
    two_tailed_critical_chi2_score = query_two_tailed_critical_chi2_score(significance, sample_size - 1)
    test_statistics_chi2_score = query_sample_variance_test_statistics_chi2_score(hypothesis_variance, sample_size, sample_variance)
    print('H0: population variance = ' + '{0:.4f}'.format(hypothesis_variance))
    print('Ha: population variance != ' + '{0:.4f}'.format(hypothesis_variance))
    print('test_statistics_chi2_score: ' + '{0:.4f}'.format(test_statistics_chi2_score))
    print('two_tailed_critical_chi2_score: ' + ' to '.join('{0:.4f}'.format(a) for a in two_tailed_critical_chi2_score))
    print('chi2 test with chi2_score')
    print('reject if test_statistics_chi2_score < ' + '{0:.4f}'.format(two_tailed_critical_chi2_score[0]) + ' or test_statistics_chi2_score > ' + '{0:.4f}'.format(two_tailed_critical_chi2_score[1]))
    if test_statistics_chi2_score < two_tailed_critical_chi2_score[0] or test_statistics_chi2_score > two_tailed_critical_chi2_score[1]:
        print('reject H0')
        return 1
    else:
        print('do not reject H0')
        return 0

def query_lower_tailed_chi2_test(hypothesis_variance, sample_size, sample_variance, significance):
    lower_tailed_critical_chi2_score = query_lower_tailed_critical_chi2_score(significance, sample_size - 1)
    test_statistics_chi2_score = query_sample_variance_test_statistics_chi2_score(hypothesis_variance, sample_size, sample_variance)
    print('H0: population variance >= ' + '{0:.4f}'.format(hypothesis_variance))
    print('Ha: population variance < ' + '{0:.4f}'.format(hypothesis_variance))
    print('test_statistics_chi2_score: ' + '{0:.4f}'.format(test_statistics_chi2_score))
    print('lower_tailed_critical_chi2_score: ' + '{0:.4f}'.format(lower_tailed_critical_chi2_score))
    print('chi2 test with chi2_score')
    print('reject if test_statistics_chi2_score < ' + '{0:.4f}'.format(lower_tailed_critical_chi2_score))
    if test_statistics_chi2_score < lower_tailed_critical_chi2_score:
        print('reject H0')
        return 1
    else:
        print('do not reject H0')
        return 0

def query_upper_tailed_chi2_test(hypothesis_variance, sample_size, sample_variance, significance):
    upper_tailed_critical_chi2_score = query_upper_tailed_critical_chi2_score(significance, sample_size - 1)
    test_statistics_chi2_score = query_sample_variance_test_statistics_chi2_score(hypothesis_variance, sample_size, sample_variance)
    print('H0: population variance <= ' + '{0:.4f}'.format(hypothesis_variance))
    print('Ha: population variance > ' + '{0:.4f}'.format(hypothesis_variance))
    print('test_statistics_chi2_score: ' + '{0:.4f}'.format(test_statistics_chi2_score))
    print('upper_tailed_critical_chi2_score: ' + '{0:.4f}'.format(upper_tailed_critical_chi2_score))
    print('chi2 test with chi2_score')
    print('reject if test_statistics_chi2_score > ' + '{0:.4f}'.format(upper_tailed_critical_chi2_score))
    if test_statistics_chi2_score > upper_tailed_critical_chi2_score:
        print('reject H0')
        return 1
    else:
        print('do not reject H0')
        return 0

def main():
    hypothesis_mean = 6.0
    hypothesis_standard_deviation = 0.75
    hypothesis_variance = hypothesis_standard_deviation ** 2
    sample_size = 30
    sample_standard_deviation = 2.0
    sample_variance = sample_standard_deviation ** 2
    significance = 0.05

    print('sample_size: ' + str(sample_size))
    print('sample_standard_deviation: ' + '{0:.4f}'.format(sample_standard_deviation))
    print('sample_variance: ' + '{0:.4f}'.format(sample_variance))
    print('significance: ' + '{0:.4f}'.format(significance))
    print()

    query_two_tailed_chi2_test(hypothesis_variance, sample_size, sample_variance, significance)
    print()

if __name__ == "__main__":
    main(
```

## output
```
sample_size: 30
sample_standard_deviation: 2.0000
sample_variance: 4.0000
significance: 0.0500

H0: population variance = 0.5625
Ha: population variance != 0.5625
test_statistics_chi2_score: 206.2222
two_tailed_critical_chi2_score: 16.0471 to 45.7223
chi2 test with chi2_score
reject if test_statistics_chi2_score < 16.0471 or test_statistics_chi2_score > 45.7223
reject H0
```
