## 功能描述

本接口用于获取机器组信息。

## 请求

#### 请求示例

```shell
GET /machinegroup?group_id=xxxx-xx-xx-xx-xxxxxxxx HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
```

#### 请求行

```shell
GET /machinegroup
```

#### 请求头

除公共响应头部外，无特殊响应头部。

#### 请求参数

| 字段名   | 类型   | 位置  | 必须 | 含义            |
| -------- | ------ | ----- | ---- | --------------- |
| group_id | string | query | 是   | 查询的 group ID |

## 响应

#### 响应示例

```shell
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 123

{
  "group_id": "xxxx-xx-xx-xx-xxxxxxxx",
  "group_name": "testname",
  "type":"label",
  "labels": [
    "defined_label_1",
    "defined_label_2"
  ],
  "create_time": "2017-08-08 12:12:12"
}
```

#### 响应头

除公共响应头部外，无特殊响应头部。

#### 响应参数

| 字段名      | 类型      | 必有 | 含义                 |
| ----------- | --------- | ---- | -------------------- |
| group_id    | string    | 是   | 机器组的 ID          |
| group_name  | string    | 是   | 机器组的名字         |
| type        | string    | 是   | 机器组类型           |
| ips         | JsonArray | 否   | ip 机器组下的 IP 列表 |
| labels      | JsonArray | 否   | label 机器组的标签表  |
| create_time | string    | 否   | 创建时间             |

>!ips 和 labels 根据 type 至少返回一个。


## 错误码

参见 [错误码](https://intl.cloud.tencent.com/document/product/614/12402)。
