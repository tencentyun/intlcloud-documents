This document describes how to view the data overview.

## Prerequisites
You have [connected your application](https://intl.cloud.tencent.com/document/product/1131/44496).

## Directions
1. Log in to the [RUM console](https://console.cloud.tencent.com/rum).
2. On the left sidebar, click **Data Overview** to enter the data overview page.
3. On the data overview page, you can view the key metric information and overall application score, including PV, firstScreenTime, JavaScript errors/error rate, as well as success rate, failure rate, and duration of API or static resource requests.
You can click the star on the left of the score to favorite the application panel and view all favorited panels quickly. The panels are sorted by the favorite time.
![](https://main.qcloudimg.com/raw/22774ad1f80ff6d5bf122a86d498127a.png)

## Data Analysis Dashboard
On the data overview page, you can click the line chart icon ![](https://qcloudimg.tencent-cloud.cn/raw/7fe9ead8206ca53064ba67ff7005b506.png) in each project module to view the data analysis dashboard.
![](https://qcloudimg.tencent-cloud.cn/raw/12eda72f4e1e788ab6d1b9e4d925eb40.jpg)


### Scoring rules

The scoring rules and percentage vary by metric as detailed below:

| Applicable Scope                  | Scoring Metric                                      | Scoring Rules                                                     | Percentage |
| ------------------------- | --------------------------------------------- | ------------------------------------------------------------ | ---- |
| Web, mini program, Hippy, and React Native  | Page error rate (page errors/page opens)       | 1. If the error rate is less than or equal to 0.5%, the score will be 100.<br>2. If the error rate is greater than 0.5% but less than 10%, the score will be 100 - 10 * error rate.<br>3. If the error rate is greater than or equal to 10%, the score will be 0. | 30%  |
| Web, mini program, Hippy, and React Native  | Average page open duration                              | 1. If the duration is less than or equal to 1,000 ms, the score will be 100.<br>2. If the duration is greater than 1,000 ms by N 100 ms, the score will be 100 - 10 * N, and the lowest score can be 0. | 10%  |
| Web, mini program, Hippy, and React Native  | API success rate (successful API access requests/total access requests)     | Same as the rules for the page error rate.                                                 | 30%  |
| Web, mini program, Hippy, and React Native  | Average API access duration                              | Same as the rules for the average page open duration.                                           | 5%   |
| Web, mini program, Hippy, and React Native  | Static resource success rate (successful static resource requests/total requests) | Same as the rules for the page error rate.                                                 | 20%  |
| Web, mini program, Hippy, and React Native  | Average static resource request duration                               | Same as the rules for the average page open duration.                                           | 5%   |

### Descriptions of key application metric colors

| Metric Name | Green           | Orange                     | Red            |
| -------- | -------------- | ------------------------ | --------------- |
| firstScreenTime   | Duration ≤ 1000 ms | 1000 ms ≤ duration ≤ 3000 ms | Duration > 3000 ms   |
| JavaScript error rate   | Error rate ≤ 0.5% | 0.5% < error rate < 10%    | Error rate ≥ 10% |
| API success rate     | Success rate > 99.5% | 90% ≤ success rate ≤ 99.5%   | Success rate < 90%     |
| Static resource success rate | Success rate > 99.5% | 90% ≤ success rate ≤ 99.5%   | Success rate < 90%    |

