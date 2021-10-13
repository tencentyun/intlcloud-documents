## Feature Description

This API is used to create a [machine group](https://intl.cloud.tencent.com/document/product/614/30449) and return its ID.

## Request

#### Sample request

```
POST /machinegroup HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
Content-Type: application/json

{
    "group_name": "testname", 
    "type": "label", 
    "labels": ["defined_label_1", "defined_label_2"]
}
```

#### Request line

```
POST /machinegroup
```

#### Request header

There are only common request headers but no special request headers.

#### Request parameters

| Field Name | Type | Location | Required | Description |
|--------------|--------|------|---------|--------------------------------|
| group_name   | string | body | Yes      | Machine group name, which must be unique             |
| type       | string    | body | No   | Machine group type. Valid values: ip and label. Default value: ip  |
| ips          | JsonArray| body| No   | List of IPs in machine group            |
| labels     | JsonArray | body | No   | List of labels in the machine group          |

## Response

#### Sample response

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 123

{"group_id": "xxxx-xx-xx-xx-xxxxxxxx"}
```

#### Response header

There are only common response headers but no special response headers.

#### Response parameters

| Field Name | Type   | Required | Description     |
|------------|--------|----------|-----------------|
| group_id   | string | Yes      | Machine group ID |

## Error Codes

For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).
