You can view records of live push interruptions and their causes in the CSS console.

## Prerequisites
- You have logged in to the [CSS console](https://console.cloud.tencent.com/live).
- There is a live stream whose push was interrupted under your account.

## Directions

In the console, select **Event Center** > [Stream Interruption Records](https://console.cloud.tencent.com/live/tools/streamevent) on the left sidebar.
![](https://qcloudimg.tencent-cloud.cn/raw/7109f254ed3f4c892bd93632d9f04629.png)

On the **Stream Interruption Records** page:
- **Path** is the value of `AppName` in the push URL.
- **Stream Name** is the value of `StreamName` in the push URL.

[](id:erro_code)
## Causes of Stream Interruption
The table below lists the possible causes of stream interruption and their error codes: 

| errcode | sub_errcode | errmsg                                         |
| ------- | ----------- | ---------------------------------------------- |
| 0       | 0           | Unknown reason.                                       |
| 1       | 0           | The push client stopped the stream.                             |
| 2       | 0           | The push client stopped the stream.                             |
| 3       | 0           | The push client stopped the stream.                             |
| 4       | 0           | The push client stopped the stream.                             |
| 5       | 0           | CSS system internal error.                               |
| 6       | 0           | RTMP content error.                               |
| 7       | 0           | Exceeded the maximum size allowed for a single RTMP frame.             |
| 8       | 0           | The system stopped the stream because no data was generated for a long time.                 |
| 9       | 0           | CSS system internal error.                               |
| 10      | 0           | The proxy layer received an interruption command.                             |
| 11       | 0           | CSS system internal error.                               |
| 12      | 0           | Network error for the push client.                               |
| 13      | 0           | Network error for the push client.                               |
| 14      | 0           | Network error for the push client.                               |
| 15      | 0           | Network error for the push client.                               |
| 16      | 0           | Network error for the push client.                               |
| 17      | 0           | Network error for the push client.                               |
| 18       | 100           | CSS system internal error.                               |
| 18       | 101           | CSS system internal error.                               |
| 18       | 102           | CSS system internal error.                               |
| 18       | 103           | CSS system internal error.                               |
| 18       | 104           | CSS system internal error.                               |
| 18      | 200         | Failed to get the user information for the push URL.                 |
| 18      | 201         | Your CSS services have been suspended.                           |
| 18      | 202         | Your CSS services have been suspended due to overdue payments. Please top up your account balance. |
| 18      | 203         | Your CSS services have been suspended.                       |
| 18      | 300         | Push using an IP address is not allowed.                     |
| 18      | 301         | Unable to identify the push domain name.                               |
| 18      | 302         | Invalid push domain name.                                 |
| 18      | 303         | The push domain name is disabled.                                 |
| 18      | 304         | The push application is disabled.                               |
| 18      | 305         | The stream is disabled.                         |
| 18      | 306         | Channel mode is used, but there isn’t a push channel.   |
| 18      | 307         | Channel mode is used, but the current push channel is disabled.       |
| 18      | 308         | The push name contains unallowed characters.                       |
| 18      | 309         | The push application name contains unallowed characters.                       |
| 18      | 400         | The push client’s IP address is on the blocklist.                       |
| 18      | 401         | The push client’s IP address is not on the allowlist.                     |
| 18      | 500         | The expiration time parameter is missing from the push URL.                         |
| 18      | 501         | The push URL has expired.                         |
| 18      | 502         | The authentication parameter is missing from the push URL.                             |
| 18      | 503         | Authentication failed.                             |
| 18      | 600         | Reached the maximum number of streams that can be pushed.               |
| 18      | 601         | Reached the maximum number of streams that can be pushed using this stream name.   |
| 18      | 602         | The priority of this stream is lower than another stream.           |
| 19      | 0           | Third-party authentication failed.                                 |
| 20       | 0           | The system stopped the stream because no data was generated for a long time.                 |
| 21      | 100         | The stream was stopped at your request.                         |
| 21      | 101         | The stream was disabled at your request.                         |
| 21      | 102         | A new push URL replaced the current one.                   |
| 21      | 103         | A new push URL replaced the current one that has no data.           |
| 22       | 0           | Unknown reason.                                       |
| 23       | 0           | RTMP content error.                               |
| 24       | 0           | CSS system internal error.                               |
| 25       | 0           | Unknown reason.                                       |
| 26       | 0           | Unknown reason.                                       |
| 27       | 0           | Unknown reason.                                       |
| 28       | 0           | Unknown reason.                                       |
| 29       | 0           | Unknown reason.                                       |
| 30       | 0           | Unknown reason.                                       |
| 31       | 0           | Unknown reason.                                       |
| 32       | 0           | Unknown reason.                                       |
| 33      | 0           | RTMP AMF error.                              |
| 34       | 0           | Unknown reason.                                       |
| 35       | 0           | The push client stopped the stream.                             |
| 36       | 0           | Unknown reason.                                       |
| 37      | 0           | SRS stopped the stream because it was not played.                            |
| 38       | 0           | CSS system internal error.                               |
| 39      | 0           | Exceeded the maximum frame size allowed for push.               |

