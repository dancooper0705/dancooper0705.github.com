---
layout: post
title: "statistics-for-business-and-economics-p8-14"
date:  2019-10-15 12:00:00  +0800
categories: [dev]
tags: [python, statistics]
---

## question
```
Find the t value(s) for each of the following examples.
a. Upper tail area of .05 with 18 degrees of freedom.
b. Lower tail area of .10 with 22 degrees of freedom.
c. Upper tail area of .01 with 5 degrees of freedom.
d. 90% of the area is between these two t values for 14 degrees of freedom.
e. 95% of the area is between these two t values with 28 degrees of freedom.
```

## source
```python
import math
import scipy.stats

def query_t_score(upper_tail_area, degree_freedom):
    lower_tail_area = 1.0 - upper_tail_area
    t_score = scipy.stats.t.ppf(1.0 - upper_tail_area, degree_freedom)
    print('degree-freedom: ' + '{0:d}'.format(degree_freedom))
    print('lower_tail_area: ' + '{0:.2f}'.format(lower_tail_area))
    print('upper_tail_area: ' + '{0:.2f}'.format(upper_tail_area))
    print('t_score: ' + '{0:.3f}'.format(t_score))

def query_critical_t_score(confidence_level, degree_freedom):
    confidence_coefficient = confidence_level / 100
    upper_tail_area = (1 - confidence_coefficient) / 2
    critical_t_score = scipy.stats.t.ppf(1.0 - upper_tail_area, degree_freedom)
    print('confidence_level: ' + '{0:.2f}'.format(confidence_level))
    print('degree-freedom: ' + '{0:d}'.format(degree_freedom))
    print('upper_tail_area: ' + '{0:.2f}'.format(upper_tail_area))
    print('critical_t_score: ' + '{0:.3f}'.format(critical_t_score))
    print('t_score interval: ' + '{0:.3f}'.format(-critical_t_score) + ' to ' + '{0:.3f}'.format(critical_t_score))

def main():
    print('problem a:')
    query_t_score(0.05, 18)
    print()

    print('problem b:')
    query_t_score(0.90, 22)
    print()

    print('problem c:')
    query_t_score(0.10, 5)
    print()

    print('problem d:')
    query_critical_t_score(90, 14)
    print()

    print('problem e:')
    query_critical_t_score(95, 28)
    print()

if __name__ == "__main__":
    main()
```

## output
```
problem a:
degree-freedom: 18
lower_tail_area: 0.95
upper_tail_area: 0.05
t_score: 1.734

problem b:
degree-freedom: 22
lower_tail_area: 0.10
upper_tail_area: 0.90
t_score: -1.321

problem c:
degree-freedom: 5
lower_tail_area: 0.90
upper_tail_area: 0.10
t_score: 1.476

problem d:
confidence_level: 90.00
degree-freedom: 14
upper_tail_area: 0.05
critical_t_score: 1.761
t_score interval: -1.761 to 1.761

problem e:
confidence_level: 95.00
degree-freedom: 28
upper_tail_area: 0.03
critical_t_score: 2.048
t_score interval: -2.048 to 2.048
```
