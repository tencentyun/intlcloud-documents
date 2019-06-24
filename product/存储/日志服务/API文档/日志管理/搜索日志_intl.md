## Description

This API is used to search the log content according to specified criteria.

### Request example

```
GET /searchlog?logset_id=xxxx-xx-xx-xx-xxxxxxxx&topic_ids=xxxx,xxxx&start_time=2017-08-22%2010%3A10%3A10&end_time=2017-08-23%2010%3A10%3A10&query=&limit=10&context= HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>

```

### Request line

```
GET /searchlog
```

### Request header

No special request header is used except for the common header.

### Request parameters

| Field Name | Type | Location | Required | Description |
|---------------|--------|------|--------|---------------------------------------------------|
| logset_id | string | query | Yes | ID of the logset to be queried |
| topic_ids | string | query | Yes | IDs of topics to be queried, separated by commas (`,`). |
| start_time | string | query | Yes | Start time of the log to be queried. Format: YYYY-mm-dd HH:MM:SS |
| end_time | string | query | Yes | End time of the log to be queried. Format: YYYY-mm-dd HH:MM:SS |
| query | string | query | Yes | Content to be queried |
| limit | int | query | Yes | Number of logs to be returned at a time, which is limited to `100`. |
| context | string | query | No | Load more for use. Transparently transmit the last returned context value, and obtain follow-up log content. |
| sort | string | query | No | Sorted by time: "asc" (ascending order) or "desc" (descending order). It defaults to "desc". |

## Response

### Response example

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

### Response header

No special response header is used except for the common response header.

### Response parameters

| Field Name | Type | Required | Description |
|-------------|----------------------|---------|-------------------------------|
| context | string | Yes | The context for loading follow-up content |
| listover | bool | Yes | Indicates whether all searched results are returned |
| results | JsonArray(LogObject) | Yes | Log content information |

LogObject is composed as follows:

| Field Name | Type | Required | Description |
|------------|--------|---------|-------------------------------|
| topic_id | string | Yes | ID of the topic to which the log belongs |
| topic_name | string | Yes | Name of the log topic |
| timestamp | string | Yes | Log time |
| content | string | Yes | Log content |

## Error Codes

For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).

