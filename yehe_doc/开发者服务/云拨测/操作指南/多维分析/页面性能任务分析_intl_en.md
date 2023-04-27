After creating a page performance test task successfully, you can analyze the overall webpage performance on the **Test Statistics** page.

## Directions

1. Log in to the [CAT console](https://console.cloud.tencent.com/cat/probe/tasklist).
2. Click **Test Statistics** on the left sidebar and select **Page performance**.
3. On the **Test Statistics** page, analyze the test data in multiple dimensions such as map, line chart, figure, and detailed data.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/YQwx417_49intl_%E5%A5%BD%E5%8E%8B%E7%9C%8B%E5%9B%BE.png)


## Metric description

| Metric               | Description                                                     |
| ------------------ | ------------------------------------------------------------ |
| Overall performance (s)      | The time from starting browsing a page to receiving the last packet.                  |
| 100 KB time (s)      | The average time taken to load 100 KB of content:<br>100 KB time = overall performance / total number of downloaded bytes x 100. |
| Time to first screen (s)      | The time from entering an URL to rendering an area on the page to a height greater than or equal to the specified height, which is 600 pixels by default. If the height is smaller than 600 pixels, the time is from starting browsing to the IE kernel sending the `Document Completed` event. |
| Availability (%)        | The rate of successful access requests to the target by the client performing the test tasks:<br>Availability = number of valid test tasks / total number of test tasks x 100%. |
| Downloaded size (KB)       | The total size downloaded by the IE kernel during the browsing.                               |
| Overall speed (KB/s)   | The average speed of loading a page:<br>Overall speed = total number of downloaded bytes / overall performance.          |
| Hijacks    | Total number of hijack occurrences.                                               |
| Rendering duration (s)     | Rendering duration = overall performance – time taken to download basic documents.                       |
| Document completion duration (s)  | The time from starting browsing a page to parsing the basic document.              |
| Errors     | Number of failed access requests in the test.                                           |
| Top 5 error types       | The top five error types of the most errors.                             |
| Top 5 slowest ISPs     | The top five ISPs with the poorest overall performance.                               |
| Valid tests | Number of valid data samples.     |
| Invalid tests | Number of invalid data samples.     |


