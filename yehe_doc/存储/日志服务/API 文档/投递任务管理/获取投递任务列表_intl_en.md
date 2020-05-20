## Feature Description

This API is used to get the shipping task information list.

## Request

#### Sample request

```shell
GET /tasks?shipper_id=xx-xx-xx-xxxx&start_time=2017-10-10+00%3A00%3A00&end_time=2017-10-10+23%3A59%3A59 HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
```

#### Request line

```shell
GET /tasks
```

#### Request header

There are only common request headers but no special request headers.

#### Request parameters

| Field Name | Type | Location | Required | Description |
|--------------|--------|------|---------|---------------------------------|
| shipper_id   | string | query| Yes      | ID of the shipping rule to be queried                  |
| start_time   | string | query| Yes      | Query start time, which can be within the last three days  |
| end_time     | string | query| Yes      | Query end time                     |

## Response

#### Sample response

```shell
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 123

{
  "tasks": [
    {
      "task_id": "xxxxx-xx-xx-xx",
      "shipper_id": "xxxxx-xx-xx-xx",
      "topic_id": "xxxxx-xx-xx-xx",
      "range_start": "2017-10-17 10:10:10",
      "range_end": "2017-10-17 10:10:10",
      "start_time": "2017-10-17 10:10:10",
      "end_time": "2017-10-17 10:10:10",
      "status": "success",
      "message": "success",
    }
  ]
}
```

#### Response header

There are only common response headers but no special response headers.

#### Response parameters

| Field Name | Type | Required | Description |
|-------------|-----------|---------|-------------------------------|
| tasks       | JsonArray | Yes      | Shipping task information array                |

`TaskInfo` is in the following format:

| Field Name | Type | Required | Description |
|------------|--------|---------|-------------------------------|
| task_id    | string | Yes      | Shipping task ID                     |
| shipper_id | string | Yes      | Shipping rule ID                     |
| topic_id         | string     | Yes       | Log topic ID                                                |
| range_start| string | Yes      | Start time of the current batch of shipped logs         |
| range_end  | string | Yes      | End time of the current batch of shipped logs         |
| start_time | string | Yes      | Start time of the current shipping task           |
| end_time   | string | Yes      | End time of the current shipping task           |
| status     | string | Yes      | Result of the current shipping task. Valid value: "success", "running", "failed", "wait" |
| message    | string | Yes      | Detailed result information                  |

## Error Codes

For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).
