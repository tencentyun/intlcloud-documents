
## Getting Consumption Configuration

#### Overview

This example shows you how to obtain details of a specified consumption policy.

#### Request line

```
GET /consumer
```

#### Sample request 

```
GET /consumer?topic_id=xxxx-xx-xx-xx-xxxxxxxx HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>
```

#### Request headers

No special request headers

#### Request parameters

| Parameter | Type | Location | Required | Description |
| -------- | ------ | ----- | -------- | ----------------- |
| topic_id | string | query | Yes | ID of the log topic to be queried |

#### Sample response

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
  "content":{"enable_tag":true,"meta_fields":["__SOURCE__"]}，
  "need_content":true
}
```

#### Response headers

No special response headers

#### Response parameters

| Parameter | Type | Required | Description |
| --------- | ------ | -------- | ------------------ |
| effective | bool | Yes | Whether the configuration takes effect |
| ckafka    | object | Yes       | CKafka consumption information |
| content   | object | No       | CKafka metadata |
| need_content   | bool    | body| No       | Whether to ship CKafka metadata. Default value: `true` |

Parameters in `ckafka`:

| Parameter | Type | Required | Description |
|------------|--------|---------|-------------------------------|
| vip | string | Yes | CKafka virtual IP |
| vport | string | Yes | CKafka virtual port |
| instance_id| string | Yes | CKafka instance ID |
| instance_name| string | Yes | CKafka instance name |
| topic_id | string | Yes | CKafka topic ID |
| topic_name | string | Yes | CKafka topic name |

#### Error codes

For details, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).

## Creating a Consumption Task

#### Overview

This example shows you how to create a consumption task.

#### Request line

```
POST /consumer
```

#### Sample request 

```
POST /consumer?topic_id=xxxxx HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>
Content-Type: application/json
{
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

#### Request headers

No special request headers

#### Request parameters

| Parameter | Type | Location | Required | Description |
| ------------ | ------ | ----- | -------- | -------------------------------------- |
| topic_id | string | query | Yes | ID of the topic associated with the consumption task |
| ckafka    | object | body | Yes       | CKafka consumption information |
| content   | object | body |  No       | CKafka metadata |
| need_content   | bool    | body | No       | Whether to ship CKafka metadata. Default value: `true` |

Parameters in `ckafka`:

| Parameter | Type | Required | Description |
|------------|--------|---------|-------------------------------|
| vip | string | Yes | CKafka virtual IP |
| vport | string | Yes | CKafka virtual port |
| instance_id | string | Yes | CKafka instance ID |
| instance_name | string | Yes | CKafka instance name |
| topic_id | string | Yes | CKafka topic ID |
| topic_name | string | Yes | CKafka topic name |

#### Sample response

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 0
```

#### Response headers

No special response headers

#### Response parameters

N/A

#### Error codes

For details, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).

## Modifying a Consumption Task

#### Overview

This example shows you how to modify a consumption task.

#### Request line

```
PUT /consumer
```

#### Sample request 

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

#### Request headers

No special request headers

#### Request parameters

| Parameter | Type | Location | Required | Description |
| ------------ | ------ | ----- | -------- | -------------------------------------- |
| topic_id | string | query | Yes | ID of the topic associated with the consumption task |
| effective    | bool   | body  | No       | Whether the consumption task takes effect                      |
| ckafka    | object | body  | No      | CKafka consumption information |
| content   | object | body | No       | CKafka metadata  |
| need_content   | bool | body | No       | Whether to ship CKafka metadata. Default value: `true` |

Parameters in `ckafka`:

| Parameter | Type | Required | Description |
|------------|--------|---------|-------------------------------|
| vip | string | Yes | CKafka virtual IP |
| vport | string | Yes | CKafka virtual port |
| instance_id| string | Yes | CKafka instance ID |
| instance_name| string | Yes | CKafka instance name |
| topic_id | string | Yes | CKafka topic ID |
| topic_name | string | Yes | CKafka topic name |

At least one of the two parameters `effective` and `ckafka` should be included.

#### Sample response

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 0
```

#### Response headers

No special response headers

#### Response parameters

N/A

#### Error codes

For details, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).

## Deleting a Consumption Task

#### Overview

This example shows you how to delete a consumption task.

#### Request line

```
DELETE /consumer
```

#### Sample request 

```
DELETE /consumer?topic_id=xxxx-xx-xx-xx-xxxxxxxx HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>
```

#### Request headers

No special request headers

#### Request parameters

| Parameter | Type | Location | Required | Description |
| -------- | ------ | ----- | -------- | -------------------------- |
| topic_id | string | query | Yes | ID of the log topic associated with consumption tasks to delete |

#### Sample response

```
HTTP/1.1 200 OK
Content-Length: 0
```

#### Response headers

No special response headers

#### Response parameters

N/A

#### Error codes

For details, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).
