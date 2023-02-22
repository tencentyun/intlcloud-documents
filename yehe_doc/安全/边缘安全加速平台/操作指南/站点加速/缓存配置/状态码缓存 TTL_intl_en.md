
## Overview
You can specify a TTL period for origin response status codes, allowing the node to directly respond with non-2XX codes.

Currently supported status codes are as follows:
- 4XX: 400, 401, 403, 404, 405, 407, 414
- 5XX: 500, 501, 502, 503, 504, 509, 514

## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Click **Rule Engine** on the left sidebar.
2. On the page that displays, select the target site and create TTL cache rules for status codes as needed. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/1145/46151).

## Configuration Sample
The following configuration sample shows how to configure the node to return the 404 status code within the specified TTL (10 seconds) for each failed request:
![](https://qcloudimg.tencent-cloud.cn/raw/1ef85ed70569a9c6fe3a0b2214a1ced8.png)