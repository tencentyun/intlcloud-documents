## Feature Description

This API is used to get the server group information.

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
  "ips": [
    "10.10.10.10","10.10.10.11"
  ],
  "create_time": "2017-08-08 12:12:12"
}
```

#### Response header

There are only common response headers but no special response headers.

#### Response parameters

| Field Name | Type | Required | Description |
|------------|--------|---------|-------------------------------|
| group_id   | string | Yes      | Server group ID                  |
| group_name | string | Yes      | Server group name                    |
| ips        | JsonArray| Yes    | List of IPs in server group            |
| create_time| string | No   | Creation time                                                     |

## Error Codes

For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).
