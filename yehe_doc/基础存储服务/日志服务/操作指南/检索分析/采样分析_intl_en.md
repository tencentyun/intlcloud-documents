## Overview

When using the statistical analysis feature as described in [Overview and Syntax Rules](https://intl.cloud.tencent.com/document/product/614/37803), if the number of raw logs is very high or the search statement (SQL) is complex, the analysis may be slow or even time out. In this case, you can use the sampling analysis feature to sample raw logs first and then perform statistical analysis.

CLS samples raw logs randomly. According to relevant statistical principles, under a reasonable sample rate and a large number of samples, the statistical results after sampling are very close to the accurate full statistical results, which can satisfy the needs of big data analysis in most cases.

## Sampling Method and Accuracy

### Sampling method

Statistical analysis adopts the "precise analysis" method by default, i.e., no sampling. If sampling is required, you can choose either of the following two sampling methods:
- Automatic sampling: The sample rate is automatically determined based on the number of raw log entries, so that the number of samples is about 1 million, and statistical analysis is performed on such samples. For example, if raw logs contain 10 billion entries, and automatic sampling is used to get 1 million samples, then the sample rate is 1:10,000.
- Fixed-rate sampling: You can manually set the sample rate to get samples from raw logs accordingly. For example, if the raw logs contain 10 billion entries and are sampled at the rate of 1:100,000, then the number of samples is 100,000. The sample rate can range from 1:1,000,000 to 1 (no sampling).

Regardless of the sampling method used, the final actual sample rate can be viewed in the statistical analysis results.


### Estimating the true value

Sampling analysis results can largely reflect the true value. Based on the value calculation method, the true value can be estimated in the following ways:
- For calculation methods related to averages such as `avg` and `geometric_mean`, the sample statistical result can directly represent the true value.
- For calculation methods related to values such as `count(*)`, `sum`, and `count_if`, the sample statistical result divided by the sample rate can represent the true value. For example, if the sample rate for pv(`count(*)`) is 1:10,000 and the statistical result is 232, then the true value is about 232 / (1:10000) = 2320000.

#### Examples

To sample at 1:10,000, the search statement is:
```
* | select count(*)/(1.0/10000) as pv,avg(response_time) as response_time_avg
```
- `pv` calculation: `count(*)` is to calculate the number of log entries and involves sum calculation. You can divide the sample statistical result by the sample rate to get the true value. Here, `(1.0/10000)` is the sample rate, and the calculated `pv` is the estimated true value of `pv`.
- `response_time_avg` calculation: `avg(response_time)` is to calculate the average of `response_time` and involves average calculation. The result can be directly used as the estimated true value of `response_time_avg`.


### Sampling analysis accuracy

In statistics, the confidence level and confidence interval are used to measure the accuracy of the sampling results. The former represents the reliability of the sampling results, and the latter represents the interval of the true value at the specified confidence level. For example, if the confidence level of a certain sample statistical result is 95%, and the confidence interval is [212,478], then the true value has a 95% probability of being between 212 and 478.

The higher the confidence level, the larger the confidence interval. The commonly used confidence level is 95% (in statistics, a probability below 5% is generally considered as a small probability). The confidence interval is calculated as follows:


Here, x̅ is the sample average, s is the sample standard deviation, and n is the number of samples.

In case of statistical analysis using automatic sampling:
```
* | select avg(response_time) as x,count(response_time) as n,stddev_samp(response_time) as s
```
The statistical analysis result of the samples is:
- x: The sample average, which is 544.4656932942215.
- n: The number of samples, which is 995,097.
- s: The sample standard deviation, which is 1,382.618439585749.

Then, if the confidence level is 95%, the true value of `avg(response_time)` is within the confidence interval of [541.75,547.18]. The `avg(response_time)` value obtained by accurate statistical calculation in this case is 545.16, which is within the confidence interval.

>? The above is a strict sampling accuracy measurement method. In actual use, when there are more than 1,000 samples, the results obtained by sampling generally are highly accurate.
>

During statistical analysis by dimension (i.e., `group by`), as the samples will be divided into multiple groups by the specified dimension, and the statistical value will be calculated in each group, the number of samples in a single group will be lower than the total number of samples. This will result in less accurate statistics for groups with a small sample size.
In case of sampling statistical analysis:

```
* | select avg(response_time) as response_time,count(*) as sampleCount,url group by url order by count(*) desc
```
The statistical analysis result of the samples is:

| url          | response_time | sampleCount |
| ------------ | ------------- | ----------- |
| /user        | 45.23         | 7845        |
| /user/list   | 78.45         | 6574        |
| /user/login  | 45.85         | 5235        |
| /user/logout | 45.48         | 1245        |
| /book/new    | 125.78        | 987         |
| /book/list   | 17.23         | 658         |
| /book/col    | 10.21          | 23          |
| /order       | 12.13          | 2           |

Here, the number of samples of the two URLS `/book/col` and `/order` is too low, so the statistical results are less accurate. To get more accurate statistical results for these two URLs, you can increase the overall sample rate or perform statistical analysis on them separately, for example:
```
url:"/book/col" OR url:"/order" | select avg(response_time) as response_time,count(*) as sampleCount,url group by url order by count(*) desc
```

## Directions

1. Log in to the [CLS console](https://console.cloud.tencent.com/cls).

2. On the left sidebar, click **Search and Analysis** to enter the log topic search and analysis page.

3. At the top of the page, select the log topic for search and analysis.

4. After entering the search statement (with SQL included), set whether sampling analysis is required and select the corresponding sample rate below the **Search and Analysis** button on the right.

5. Click **Search and Analysis**.
After the search and analysis is completed, the sample rate used for this analysis will be displayed at the top of the chart.

	
