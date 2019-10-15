---
layout: post
title: "statistics-for-business-and-economics-p8-6"
date:  2019-10-14 23:30:00  +0800
categories: [dev]
tags: [python, statistics]
---

## question description
```
6. Mean weekly earnings of individuals working in various industries were
reported  in The New York Times 1998 Almanac. The mean weekly earnings for
individuals in the service industry were $369. Assume that this result was
based on a sample of 250 service individual and that the sample standard deviation
was $50. Compute the 95% confidence interval for the population mean weekly
earnings for individuals working in the service industry.
```

## source
### a.py
```python
import math
import scipy.stats

def main():
    sample_mean = 369
    sample_size = 250
    sample_standard_deviation = 50
    confidence_level = 95

    confidence_coefficient = confidence_level / 100
    alpha_level = 1 - confidence_coefficient
    tail_area = alpha_level / 2
    z_score = float(scipy.stats.norm.ppf(1 - tail_area))
    standard_deviation = sample_standard_deviation / math.sqrt(sample_size)
    print('z_score: ' + str(z_score))
    margin_of_error =  standard_deviation * z_score
    print('margin_of_error: ' + str(margin_of_error))
    population_mean_interval_estimate = [sample_mean - margin_of_error,
sample_mean + margin_of_error]
    print('population_mean_interval_estimate: ' +
str(population_mean_interval_estimate))

if __name__ == "__main__":
    main()
```

## output
```bash
cat a.txt | python3 a.py 2>&1 | tee  b.txt
z_score: 1.959963984540054
margin_of_error: 6.197950323045616
population_mean_interval_estimate: [362.80204967695437, 375.19795032304563]
```
