## Feature Description

This API is used to get the status of the machines in a specified machine group.

## Request
#### Sample request

```shell
GET /machines?group_id=xxxx-xx-xx-xx-xxxxxxxx HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
```

#### Request line

```shell
GET /machines
```

#### Request header

There are only common request headers but no special request headers.

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
  "machines": [
    {"ip": "10.10.10.10","status": 0},
    {"ip": "10.10.10.11","status": 1}
  ]
}
```

#### Response header

There are only common response headers but no special response headers.

#### Response parameters

| Field Name | Type | Required | Description |
|-------------|-----------|---------|-------------------------------|
| machines    |JsonArray  | Yes      | Machine information array                    |

`MachineInfo` is in the following format:

| Field Name | Type | Required | Description |
|------------|--------|---------|-------------------------------|
| ip         | string | Yes      | Machine IP                    |
| status     | int    | Yes      | 0: abnormal, 1: normal            |

## Error Codes

For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).
