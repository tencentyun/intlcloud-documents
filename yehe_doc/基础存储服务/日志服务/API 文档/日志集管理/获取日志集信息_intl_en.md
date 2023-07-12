## Feature Description

This API is used to get the logset information.

## Request

#### Sample request

```shell
GET /logset?logset_id=xxxx-xx-xx-xx-xxxxxxxx HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
```

#### Request line

```shell
GET /logset
```

#### Request header

There are only common request headers but no special request headers.

#### Request parameters

| Field Name | Type | Location | Required | Description |
| --------- | ------ | ----- | ---- | ---------------- |
| logset_id | string | query | Yes       | ID of the logset to be queried |

## Response

#### Sample response

```shell
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 123

{
  "logset_id": "xxxx-xx-xx-xx-xxxxxxxx",
  "logset_name": "testname",
  "period": 15,
  "create_time": "2017-08-08 12:12:12",
  "assumer_uin": 1000088888,
  "assumer_name": "xxxxxx",
  "logset_modify_acl": 31
}
```

#### Response header

There are only common response headers but no special response headers.

#### Response parameters

| Field Name | Type | Required | Description |
| ----------------- | ------ | ---- | ------------------------------------------------------------ |
| logset_id        | string     | Yes       | Logset ID                                                  |
| logset_name       | string | Yes   | Logset name                                                 |
| period            | int    | Yes   | Retention period in days                                               |
| create_time       | string | No   | Creation time                                                     |
| assumer_uin      | uint64     | No       | `uin` of the service that creates the logset (this field is present only when a general account views the logsets created by a service account) |
| assumer_name     | string     | No       | Name of the service that creates the logset (this field is present only when a general account views the logsets created by a service account) |
| logset_modify_acl | int    | No   | General user's permission to modify logsets, i.e., `modify_acl` (0B00000: modification prohibited, 0B00001: modification allowed for basic information) (this field is present only when a general account views the logsets created by a service account) |

## Error Codes

For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).
