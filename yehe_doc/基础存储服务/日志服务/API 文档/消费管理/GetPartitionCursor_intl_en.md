## Feature Description

This API is used to get the cursor of the corresponding topic partition based on time, which is used to get the log data on the corresponding topic partition.

## Request

#### Sample request

```shell
GET /cursor?topic_id=xxxxxxxx-xxxx-xxxx-xxxx&partition_id=1&from=end HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
```

#### Request header

There are only common request headers but no special request headers.

#### Request parameters

| Parameter Name | Type | Location | Required | Description |
| ------------ | ------ | ----- | -------- | ------------------------------------------------------------ |
| topic_id       | string            | query | Yes       | Log topic ID            |
| partition_id   | int    | query | Yes       | Topic partition number                                        |
| from         | string | query | Yes       | `from` is used to identify the start time of real-time consumption, which supports three types: <br />1. "UNIX timestamp (seconds)", which indicates to consume the logs starting at the specified UNIX time <br />2. "start", which indicates to consume logs starting at the start time of the topic partition lifecycle <br />3. "end", which indicates to consume logs starting at the end time of the topic partition lifecycle (current time) |

##### Topic partition lifecycle description

The data lifecycle of a topic partition is set by the CLS backend and is no less than 1 day (the lifecycle of topic partition data varies by log topic).

For example, if the current time is 2019-10-10 12:00:00, the time range (based on the server time) in which data in each topic partition can be consumed is: [2019-10-09 12:00:00, 2019-10-10 12:00:00).

`from` can be used to locate the starting position of real-time consumption in the topic partition. If the lifecycle of the topic partition is [start_time, end_time), then:
- When `from (UNIX timestamp) ≤ start_time or from = "start"`, the time point returned by the API will be the cursor position corresponding to `start_time`.
- When `from (UNIX timestamp) ≥ end_time or from = "end"`, the API will return the next cursor position to be written at the current time point (there is no data at this cursor position currently).
- When `from (UNIX timestamp) > start_time and from (UNIX timestamp) < end_time`, the API will return the cursor position corresponding to the first data packet received by the server at a time after or at `from` (UNIX timestamp).



## Response

#### Sample response

```shell
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 23

{"cursor": "MTQ0NzI5OTYwNjg5NjYzMjM1Ng=="}
```

#### Response header

There are only common response headers but no special response headers.

#### Response parameters

| Field Name | Type | Required | Description |
| ------ | ------ | -------- | ------------ |
| cursor         | string | Yes       | Returned cursor value                  |

## Error Codes

For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).
