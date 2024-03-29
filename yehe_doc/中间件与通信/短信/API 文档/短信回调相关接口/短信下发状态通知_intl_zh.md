## 接口描述

### 功能描述
短信下发给用户后，腾讯云短信服务可以通过回调业务 URL 的方式，通知业务方短信下发的状态。

### URL 示例
```
POST http://example.com/sms/callback
```

## 请求参数
请求参数如下表所示。

| 参数              | 必选 | 类型   | 描述                                                    |
|-------------------|------|--------|---------------------------------------------------------|
| user_receive_time | 是   | string | 用户实际接收到短信的时间                                |
| nationcode        | 是   | string | 国家（或地区）码                                                  |
| mobile            | 是   | string | 手机号码                                                |
| report_status     | 是   | string | 实际是否收到短信接收状态，SUCCESS（成功）、FAIL（失败） |
| errmsg            | 是   | string | 用户接收短信状态码错误信息，参考 [回执状态错误码](https://intl.cloud.tencent.com/document/api/382/43546)  |
| description       | 是   | string | 用户接收短信状态描述                                    |
| sid               | 是   | string | 本次发送标识 ID（与发送接口返回的SerialNo对应）                                          |

>? 一次回调请求里可能有多次的短信请求结果。

请求示例：

```json
[
    {
        "user_receive_time": "2015-10-17 08:03:04",
        "nationcode": "86",
        "mobile": "13xxxxxxxxx",
        "report_status": "SUCCESS",
        "errmsg": "DELIVRD",
        "description": "用户短信送达成功",
        "sid": "xxxxxxx"
    }
]
```

## 响应参数
响应参数如下表所示。

| 参数   | 必选 | 类型   | 描述                                     |
|--------|------|--------|------------------------------------------|
| result | 是   | number | 错误码，0表示成功，非0表示失败 |
| errmsg | 是   | string | 错误消息，result 非0时的具体错误信息      |

响应示例：

```json
{
    "result": 0,
    "errmsg": "OK"
}
```

