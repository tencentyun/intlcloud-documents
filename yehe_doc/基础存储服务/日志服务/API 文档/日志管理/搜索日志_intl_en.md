## Feature Description

This API is used to search for log content by specified criteria.

## Request
#### Sample request

```plaintext
GET /searchlog?logset_id=xxxx-xx-xx-xx-xxxxxxxx&topic_ids=xxxx&start_time=2017-08-22+10%3A10%3A10&end_time=2017-08-23+10%3A10%3A10&query_string=&limit=10&context= HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>

```

#### Request line

```shell
GET /searchlog
```

#### Request header

There are only common request headers but no special request headers.

#### Request parameters

| Field Name | Type | Location | Required | Description |
|---------------|--------|------|--------|---------------------------------------------------|
| logset_id     | string | query| Yes      | ID of the logset to be queried                                   |
| topic_ids     | string | query| Yes      | IDs of the topics to be queried                         |
| start_time    | string | query| Yes      | Start time of the log to be queried in the format of `YYYY-mm-dd HH:MM:SS`       |
| end_time      | string | query| Yes      | End time of the log to be queried in the format of `YYYY-mm-dd HH:MM:SS`     |
| query_string         | string | query| Yes     |Query statement. For more information, see [Syntax and Rules](https://intl.cloud.tencent.com/document/product/614/30439)|
| limit         | int    | query| Yes      | Number of logs to be returned at a time. Maximum value: 100         |
| context       | string | query| No      | This field is used when loading more results. Pass through the last `context` value returned to get more log content. Up to 10,000 logs can be obtained through cursor. Please narrow down the time range as much as possible |
| sort          | string | query| No      | Sorting by log time. Valid values: asc (ascending), desc (descending). Default value: desc        |

## Response

#### Sample response

```shell
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 53

{
    "context": "abcdefg",
    "listover": false,
    "results": [
    {
        "timestamp": "2017-07-14 20:43:00",
        "topic_id": "xxxx-xx-xx-xx-xxxxxxxx",
        "topic_name": "xxxxxxx",
        "content": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
    },
    {
        "timestamp": "2017-07-14 20:42:00",
        "topic_id": "xxxx-xx-xx-xx-xxxxxxxx",
        "topic_name": "xxxxxxx",
        "content": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
    }
    ]
}
```

#### Response header

There are only common response headers but no special response headers.

#### Response parameters

| Field Name | Type | Required | Description |
|-------------|----------------------|---------|-------------------------------|
| context     | string               | Yes      | Cursor for more search results       |
| listover    | bool                 | Yes      | Whether all search results have been returned          |
| results     | JsonArray(LogObject) | Yes      | Log content information                    |

`LogObject` is in the following format:

| Field Name | Type | Required | Description |
|------------|--------|---------|-------------------------------|
| topic_id   | string | Yes      | Topic ID of log             |
| topic_name       | string     | Yes       | Log topic name                                               |
| timestamp  | string | Yes      | Log time                       |
| content    | string | Yes      | Log content                       |
| filename    | string | Yes      | Collection path                       |
| source    | string | Yes      | Log source device                       |

## Error Codes

For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).
