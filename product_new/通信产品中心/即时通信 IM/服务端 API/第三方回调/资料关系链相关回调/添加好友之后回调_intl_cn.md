## 功能说明

App 后台可以通过该回调实时查看用户的新增好友信息。

## 注意事项

- 要启用回调，必须配置回调 URL，并打开本条回调协议对应的开关，配置方法详见 [第三方回调配置](https://intl.cloud.tencent.com/document/product/1047/34520) 文档。
- 回调的方向是即时通信 IM 后台向 App 后台发起 HTTP POST 请求。
- App 后台在收到回调请求之后，务必校验请求 URL 中的参数 SDKAppID 是否是自己的 SDKAppID。
- 其他安全相关事宜请参考 [第三方回调简介：安全考虑](https://intl.cloud.tencent.com/document/product/1047/34354#.E5.AE.89.E5.85.A8.E8.80.83.E8.99.91) 文档。

## 可能触发该回调的场景

- App 后台通过 REST API 发起加好友请求，请求添加双向好友，且对方的加好友验证方式是“允许任何人”。
- App 用户通过客户端发起加好友请求，请求添加双向好友，且对方的加好友验证方式是“允许任何人”。
- App 后台通过 REST API 发起加好友请求，请求添加单向好友。
- App 用户通过客户端发起加好友请求，请求添加单向好友。
- App 用户收到加好友请求后，同意添加对方为好友。
- App 后台通过 REST API 强制加好友。

## 回调发生时机

成功添加好友后触发。

>!通过调用 [导入好友](https://intl.cloud.tencent.com/zh/document/product/1047/34903)接口添加好友时，不会触发此回调。

## 接口说明
### 请求 URL 示例

以下示例中 App 配置的回调 URL 为 `https://www.example.com`。
**示例：**

```
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
```

### 请求参数说明

| 参数 | 说明 |
| --- | --- |
| https | 请求协议为 HTTPS，请求方式为 POST |
| www.example.com | 回调 URL |
| SdkAppid | 创建应用时在即时通信 IM 控制台分配的 SDKAppID |
| CallbackCommand | 固定为：Sns.CallbackFriendAdd |
| contenttype | 固定值为：json |
| ClientIP | 客户端 IP，格式如：127.0.0.1 |
| OptPlatform | 客户端平台，取值参见 [第三方回调简介：回调协议](https://intl.cloud.tencent.com/document/product/1047/34354#.E5.9B.9E.E8.B0.83.E5.8D.8F.E8.AE.AE) 中 OptPlatform 的参数含义 |

### 请求包示例

```
{
    "CallbackCommand": "Sns.CallbackFriendAdd",
    "PairList": [
        {
            "From_Account": "id",
            "To_Account": "id1",
            "Initiator_Account": "id"
        },
        {
            "From_Account": "id",
            "To_Account": "id2",
            "Initiator_Account": "id"
        },
        {
            "From_Account": "id",
            "To_Account": "id3",
            "Initiator_Account": "id"
        }
    ],
    "ClientCmd":"friend_add",
    "Admin_Account":"",
    "ForceFlag":1
}
```

### 请求包字段说明

| 字段 | 类型 | 说明 |
| --- | --- | --- |
| CallbackCommand | String | 回调命令|
| PairList | Array | 成功添加的好友对 |
| From_Account | String | From_Account 的好友表中增加了 To_Account |
| To_Account | String | To_Account 被增加到了 From_Account 的好友表中 |
| Initiator_Account | String | 发起加好友请求的用户的 UserID |
| ClientCmd | String | 触发回调的命令字：<br>加好友请求，合理的取值如下：friend_add、FriendAdd<br>加好友回应，合理的取值如下：friend_response、FriendResponse |
| Admin_Account | String | 如果当前请求是后台触发的加好友请求，则该字段被赋值为管理员帐号；否则为空 |
| ForceFlag | Integer | 管理员强制加好友标记：1 表示强制加好友；0 表示常规加好友方式 |

### 应答包示例

```
{
    "ActionStatus": "OK",
    "ErrorCode": 0,
    "ErrorInfo": ""
}
```

### 应答包字段说明

| 字段 | 类型 | 属性 | 说明 |
| --- | --- | --- | --- |
| ActionStatus | String | 必填 | 请求处理的结果，OK 表示处理成功，FAIL 表示失败 |
| ErrorCode | Integer | 必填 | 错误码，0表示 App 后台处理成功，1表示 App 后台处理失败 |
| ErrorInfo | String | 必填 | 错误信息 |

## 参考

- [第三方回调简介](https://intl.cloud.tencent.com/document/product/1047/34354)
- REST API：[添加好友](https://intl.cloud.tencent.com/document/product/1047/34902)

