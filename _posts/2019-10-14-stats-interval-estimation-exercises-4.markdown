---
layout: post
title: "stats-interval-estimation-exercises-4"
date:  2019-10-14 23:00:00  +0800
categories: [dev]
tags: [python, statistics]
---

## question description
```
4. A 95% confidence interval for a population mean is reported to be 122 to 130. if
the saple mean is 126 and the sample standard deviation is 16.07, what sample
size was used in the study?
```

## source
### a.py
```python
import sys
import scipy.stats

def main():
    population_mean_interval_estimate = [122, 130]
    sample_mean = 126
    sample_standard_deviation = 16.07
    confidence_level = 95

    margin_of_error = sample_mean - population_mean_interval_estimate[0]
    confidence_coefficient = confidence_level / 100
    alpha_level = 1 - confidence_coefficient
    tail_area = alpha_level / 2
    z_score = float(scipy.stats.norm.ppf(1 - tail_area))
    print('z_score: ' + str(z_score))
    standard_deviation = margin_of_error / z_score;
    sample_size = round((sample_standard_deviation / standard_deviation) ** 2)
    print('sample_size: ' + str(sample_size))

if __name__ == "__main__":
    main()
```

## output
```bash
bash-3.2$ python3 a.py
z_score: 1.959963984540054
sample_size: 62
```
