## 功能描述

本接口用于获取指定日志主题下的日志游标，并进行下载。

## 请求

#### 请求示例

```shell
GET /cursor?topic_id=xxxxxxxx-xxxx-xxxx-xxxx&start=2017-12-28%2014%3A13%3A00 HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
```

#### 请求行

```shell
GET /cursor
```

#### 请求头

除公共头部外，无特殊请求头部。

#### 请求参数

| 字段名   | 类型   | 位置  | 必须 | 含义                                                 |
| -------- | ------ | ----- | ---- | ---------------------------------------------------- |
| topic_id | string | query | 是   | 日志主题的 ID                                        |
| start    | string | query | 是   | 日志的开始时间，精确到分钟，格式 YYYY-mm-dd HH:MM:SS |

## 响应

#### 响应示例

```shell
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 23

{
    "cursor": "1212ssssxxxxxx"
}
```

#### 响应头

除公共响应头部外，无特殊响应头部。

#### 响应参数

| 字段名 | 类型   | 必有 | 含义 |
| ------ | ------ | ---- | ---- |
| cursor | string | 是   | 游标 |

## 错误码

参见 [错误码](https://intl.cloud.tencent.com/document/product/614/12402)。