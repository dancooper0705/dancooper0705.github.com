---
layout: post
title: "statistics-for-business-and-economics-p11-12"
date:  2019-10-18 16:40:00  +0800
categories: [dev]
tags: [statistics]
---

## question
```
The variance in the number of vehicles owned or leased by subscribers to Fortune
magazine is 0.94(Fortune subscriber Portrait 1994). Assume a sample of 12
subscribers to another magazined provided the following data on the number of
vechicles owned or leased: 2, 1, 2, 0, 3, 2, 2, 1, 2, 1, 0, and 1.
a. Compute the sample variance in the number of vehicles owned or leased by the
12 subscribers.
b. Test the hypothesis that the variance in the number of vehicles owned or
leaased is the same for both magazines. WIth a 0.05 level of significance, what
is your conclusion/
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
    sample = [2, 1, 2, 0, 3, 2, 2, 1, 2, 1, 0, 1]
    sample_size = len(sample)
    hypothesis_variance = 0.94
    hypothesis_standard_deviation = math.sqrt(hypothesis_variance)
    sample_size = len(sample)
    sample_standard_deviation = np.std(sample, ddof=1)
    sample_variance = np.var(sample, ddof=1)
    significance = 0.05

    print('sample_size: ' + str(sample_size))
    print('sample_standard_deviation: ' + '{0:.4f}'.format(sample_standard_deviation))
    print('sample_variance: ' + '{0:.4f}'.format(sample_variance))
    print('significance: ' + '{0:.4f}'.format(significance))
    print()

    query_two_tailed_chi2_test(hypothesis_variance, sample_size, sample_variance, significance)
    print()

if __name__ == "__main__":
    main()
```

## output
```
sample_size: 12
sample_standard_deviation: 0.9003
sample_variance: 0.8106
significance: 0.0500

H0: population variance = 0.9400
Ha: population variance != 0.9400
test_statistics_chi2_score: 9.4858
two_tailed_critical_chi2_score: 3.8157 to 21.9200
chi2 test with chi2_score
reject if test_statistics_chi2_score < 3.8157 or test_statistics_chi2_score > 21.9200
do not reject H0
```
