## Feature Description

This API is used to modify an existing shipping task.


## Request

### Request line

```
PUT /consumer
```

### Sample request

```
PUT /shipper?topic_id=xxxxxxxx HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>
Content-Type: application/json

{
  "effective": true,
  "ckafka": {
    "vip": "10.123.123.123",
    "vport": "8888",
    "instance_id": "xxxxxx",
    "instance_name": "myname",
    "topic_id": "xxxxx",
    "topic_name": "xxx",
    
  },
  "content": {"enable_tag":true,"meta_fields":["__SOURCE__"]},
  "need_content": true
}

```

### Request headers

No special response headers

### Request parameters

| Parameter | Type | Position | Required | Description |
|------------|--------|-------|---------|-------------------------------|
| topic_id | string | query | Yes | ID of the log topic associated with the shipping task |
| effective    | bool   | body  | No       | Whether the shipping task takes effect                      |
| ckafka    | object | body | No       | CKafka instance information |
| content   | object | body |  No       | CKafka metadata |
| need_content   | bool | body | No       | Whether to ship CKafka metadata. Default value: `true` |

Parameters in `ckafka`:

| Parameter  | Type    | Required | Description                                                        |
|------------|--------|---------|-------------------------------|
| vip        | string | Yes      | CKafka VIP          |
| vport      | string | Yes      | CKafka Vport          |
| instance_id| string | Yes | CKafka instance ID |
| instance_name| string | Yes | CKafka instance name |
| topic_id | string | Yes | CKafka topic ID |
| topic_name | string | Yes | CKafka topic name |

Parameters in `content`:

| Parameter  | Type    | Required | Description                                                        |
|------------|--------|---------|-------------------------------|
| enable_tag        | bool | Yes      | Whether to ship tag information          |
| meta_fields      | array(string) | Yes      | List of the metadata to be shipped. Supported: \_\_SOURCE\_\_, \_\_FILENAME\_\_, \_\_TIMESTAMP\_\_ |


At least one of the three parameters `effective`, `ckafka`, and `content` should be included.

## Response

### Sample response

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 0

```

### Response headers

No special response headers

### Response parameters

Free

## Error Codes

See [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).
