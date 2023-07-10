## Feature Description

This API is used to get the machine group information list.

## Request

#### Sample request

```
GET /machinegroups HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>

```

#### Request line

```
GET /machinegroups
```

#### Request header

There are only common request headers but no special request headers.

#### Request parameters

None.

## Response

#### Sample response

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 123

{
  "machine_groups": [
    {
    "group_id": "xxxx-xx-xx-xx-xxxxxxxx",
    "group_name": "testname",
    "create_time": "2017-08-08 12:12:12"
    }
  ]
]
```

#### Response header

There are only common response headers but no special response headers.

#### Response parameters

| Field Name | Type | Required | Description |
|-------------|-----------|---------|-------------------------------|
| machine_groups|JsonArray| Yes      | Machine group information array                  |

`MachineGroupInfo` is in the following format:

| Field Name | Type | Required | Description |
|------------|--------|---------|-------------------------------|
| group_id   | string | Yes      | Machine group ID                  |
| group_name | string | Yes      | Machine group name                    |
| create_time| string | No   | Creation time                                                     |

## Error Codes

For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).
