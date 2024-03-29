## 功能描述

本接口用于获取投递配置的详细信息。

## 请求

### 请求行

```
GET /consumer
```

### 请求示例

```
GET /consumer?topic_id=xxxx-xx-xx-xx-xxxxxxxx HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>

```

### 请求头

无特殊。

### 请求参数

| 字段名        |  类型  | 位置  |是否必须 |      含义                  |
|------------  --|--- -----|----  --|----    ----|---------------------------|
| topic_id     | string | query | 是      | 投递的日志主题 ID           |

## 响应

### 响应示例

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

### 响应头

无特殊。

### 响应参数

|  字段名     |  类型  | 是否必须 |        含义                    |
|------------|--------|---------|-------------------------------|
| effective  | bool   | 是      | 是否生效                       |
| ckafka     | object | 是      | Ckafka 实例信息              |
| content    | object | 否      | 投递日志的元数据信息             |
| need_content| bool  | 否      | 是否投递日志的元数据信息，默认为 true |

ckafka 格式如下：

|  字段名     |  类型  | 是否必须 |        含义                    |
|------------|--------|---------|-------------------------------|
| vip        | string | 是      | Ckafka 的 vip          |
| vport      | string | 是      | Ckafka 的 vport          |
| instance_id| string | 是      | Ckafka 的实例 ID          |
| instance_name| string | 是      | Ckafka 的实例名称          |
| topic_id   | string | 是      | Ckafka 的主题 ID          |
| topic_name | string | 是      | Ckafka 的主题名称          |

content 格式如下：

|  字段名     |  类型  | 是否必须 |        含义                    |
|------------|--------|---------|-------------------------------|
| enable_tag        | bool | 是      | 是否投递 TAG 信息          |
| meta_fields      | array(string) | 是      | 需要投递的元数据列表，目前仅支持：\_\_SOURCE\_\_，\_\_FILENAME\_\_和\_\_TIMESTAMP\_\_ |

## 错误码

参见 [错误码](https://intl.cloud.tencent.com/document/product/614/42832)。

