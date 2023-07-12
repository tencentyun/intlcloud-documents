## Feature Description

This API is used to get shipping configuration details.

## Request

### Request line

```
GET /consumer
```

### Sample request

```
GET /consumer?topic_id=xxxx-xx-xx-xx-xxxxxxxx HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>

```

### Request headers

No special request headers

### Request parameters

| Parameter | Type | Position | Required | Description |
|------------  --|--- -----|----  --|----    ----|---------------------------|
| topic_id | string | query | Yes | ID of the log topic to be shipped |

## Response

### Sample response

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 123

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
  "content":{"enable_tag":true,"meta_fields":["__SOURCE__"]},
  "need_content": true
}
```

### Response headers

No special response headers

### Response parameters

| Parameter | Type | Required | Description |
|------------|--------|---------|-------------------------------|
| effective | bool | Yes | Whether to enable the task |
| ckafka     | object | Yes      | CKafka instance information              |
| content    | object | No      | Log metadata to be shipped             |
| need_content | bool  | No      | Whether to ship log metadata. Default value: `true` |

Parameters in `ckafka`:

| Parameter | Type | Required | Description |
|------------|--------|---------|-------------------------------|
| vip        | string | Yes      | CKafka VIP          |
| vport      | string | Yes      | CKafka Vport          |
| instance_id | string | Yes | CKafka instance ID |
| instance_name | string | Yes      | CKafka instance name          |
| topic_id | string | Yes | CKafka topic ID |
| topic_name | string | Yes      | CKafka  topic name          |

Parameters in `content`:

| Parameter | Type | Required | Description |
|------------|--------|---------|-------------------------------|
| enable_tag        | bool | Yes      | Whether to ship tag information          |
| meta_fields      | array(string) | Yes      | List of the metadata to be shipped. Supported: \_\_SOURCE\_\_, \_\_FILENAME\_\_, \_\_TIMESTAMP\_\_ |

## Error Codes

For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/42832).

