## Feature Description

This API is used to get the machine group information.

## Request

#### Sample request

```shell
GET /machinegroup?group_id=xxxx-xx-xx-xx-xxxxxxxx HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
```

#### Request line

```shell
GET /machinegroup
```

#### Request header

There are only common response headers but no special response headers.

#### Request parameters

| Field Name | Type | Location | Required | Description |
|--------------|--------|------|---------|--------------------------------|
| group_id     | string | query| Yes      | ID of the group to be queried                   |

## Response

#### Sample response

```shell
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 123

{
  "group_id": "xxxx-xx-xx-xx-xxxxxxxx",
  "group_name": "testname",
  "type":"label",
  "labels": [
    "defined_label_1",
    "defined_label_2"
  ],
  "create_time": "2017-08-08 12:12:12"
}
```

#### Response header

There are only common response headers but no special response headers.

#### Response parameters

| Field Name      | Type      | Required | Description                 |
| ----------- | --------- | ---- | -------------------- |
| group_id    | string    | Yes   | Machine group ID          |
| group_name  | string    | Yes  | Machine group name        |
| type        | string    | Yes   | Machine group type           |
| ips         | JsonArray | No   | List of IPs in the machine group |
| labels      | JsonArray | No   | List of labels in the machine group   |
| create_time | string    | No   | Creation time            |

>! Depending on the `type` value, either or both of `ips` and `labels` are returned.

## Error Codes

For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).
