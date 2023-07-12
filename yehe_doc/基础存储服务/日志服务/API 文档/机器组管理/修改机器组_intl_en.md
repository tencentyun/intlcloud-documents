## Feature Description

This API is used to modify a machine group.

## Request

#### Sample request

```shell
PUT /machinegroup HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
Content-Type: application/json

{
    "group_id": "xxxx-xx-xx-xx-xxxxxxx", 
    "group_name": "testname", 
    "type"： "ip", 
    "ips": ["10.10.10.10", "10.10.10.11"]
}
```

#### Request line

```shell
PUT /machinegroup
```

#### Request header

There are only common request headers but no special request headers.

#### Request parameters

| Field Name | Type | Location | Required| Description |
|------------|----------|------|---------|--------------------------------|
| group_id   | string   | body | Yes     | ID of the machine group to be modified                |
| group_name | string   | body | No      | Machine group name, which must be unique             |
| type       | string   | body | No      | Machine group type. Valid values: ip and label. Default value: ip  |
| ips        | JsonArray| body | No      | List of IPs in machine group                  |
| labels     | JsonArray| body | No      | List of labels in the machine group          |

>Either `group_name`, `ips` or `labels` must be provided.

## Response

#### Sample response

```shell
HTTP/1.1 200 OK
Content-Length: 0
```

#### Response header

There are only common response headers but no special response headers.

#### Response parameters

None.

## Error Codes

For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).

