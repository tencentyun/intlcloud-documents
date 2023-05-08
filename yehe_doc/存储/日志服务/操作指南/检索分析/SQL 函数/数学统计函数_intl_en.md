This document introduces the basic syntax and examples of mathematical statistical functions.

## Basic syntax

| Function                   | Description                                                         |
| -------------------------- | ------------------------------------------------------ |
| corr(key1, key2) [](id:corr)          | Returns the correlation coefficient of two columns. The calculation result range is [0,1].               |
| covar_pop(key1, key2) [](id:covar_pop)     | Returns the population covariance of two columns.                                 |
| covar_samp(key1, key2) [](id:covar_samp)    | Returns the sample covariance of two columns.                                 |
| regr_intercept(key1, key2)[](id:regr_intercept) | Returns linear regression intercept of input values. `key1` is the dependent value. `key2` is the independent value. |
| regr_slope(key1, key2) [](id:regr_slope)    | Returns linear regression slope of input values. `key1` is the dependent value. `key2` is the independent value. |
| stddev(key)    [](id:stddev)            | Returns the sample standard deviation of the `key` column. This function is equivalent to the `stddev_samp` function.         |
| stddev_samp(key)[](id:stddev_samp)           | Returns the sample standard deviation of the `key` column.                                |
| stddev_pop(key) [](id:stddev_pop)           | Returns the population standard deviation of the `key` column.                                |
| variance(key) [](id:variance)             | Returns the sample variance of the `key` column. This function is equivalent to the `var_samp` function.              |
| var_samp(key) [](id:var_samp)             | Returns the sample variance of the `key` column.                                |
| var_pop(key)   [](id:var_pop)            | Returns the population variance of the `key` column.                                 |



## Example
Returns the correlation between data in the `timeCost` (response time) and `SamplingRate` (sampling rate) columns:
```
* | select corr(timeCost,SamplingRate)
```

