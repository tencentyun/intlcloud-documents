## 功能说明
 App 管理员可以通过该接口获取群计数器。
 >! 该功能仅对旗舰版客户开放，需 [购买旗舰版](https://www.tencentcloud.com/document/product/1047/34577)。

## 接口调用说明
### 适用的群组类型

|群组类型 ID|是否支持此 REST API|
|-----------|------------|
|Private|支持，同新版本中的 Work（好友工作群）|
|Public|支持|
|ChatRoom|支持，同新版本中的 Meeting（临时会议群）|
|AVChatRoom|支持|
|Community（社群）|不支持|


即时通信 IM 内置上述群组类型，详情介绍请参见 [群组系统](https://intl.cloud.tencent.com/document/product/1047/33529)。

### 请求 URL 示例
```
https://xxxxxx/v4/group_open_http_svc/get_group_counter?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```
### 请求参数说明

下表仅列出调用本接口时涉及修改的参数及其说明，更多参数详情请参见 [REST API 简介](https://intl.cloud.tencent.com/document/product/1047/34620)。

| 参数               | 说明                                 |
| ------------------ | ------------------------------------ |
| xxxxxx | SDKAppID 所在国家/地区对应的专属域名：<br><li>中国：`console.tim.qq.com`</li><li>新加坡：`adminapisgp.im.qcloud.com`</li><li>首尔： `adminapikr.im.qcloud.com`</li><li>法兰克福：`adminapiger.im.qcloud.com`</li><li>孟买：`adminapiind.im.qcloud.com`</li><li>硅谷：`adminapiusa.im.qcloud.com`</li>|
| v4/group_open_http_svc/modify_group_attr | 请求接口                             |
| sdkappid           | 创建应用时即时通信 IM 控制台分配的 SDKAppID |
| identifier         | 必须为 App 管理员帐号，更多详情请参见 [App 管理员](https://intl.cloud.tencent.com/document/product/1047/33517)                |
| usersig            | App 管理员帐号生成的签名，具体操作请参见 [生成 UserSig](https://intl.cloud.tencent.com/document/product/1047/34385)    |
| random             | 请输入随机的32位无符号整数，取值范围0 - 4294967295                 |
|contenttype|请求格式固定值为`json`|

### 最高调用频率

200次/秒。

### 请求包示例

 **基础形式**
获取群计数器。
```
{
    "GroupId": "@TGS#aC5SZEAEF",
    "GroupCounterKeys":[    // 获取指定群计数器的 Key 列表，不填则全部返回
        "like",
        "unlike"
    ]
}
```

### 请求包字段说明

| 字段 | 类型 | 属性 | 说明 |
|---------|---------|---------|---------|
| GroupId | String | 必填 | 群组 ID |
| GroupCounterKeys | Array | 选填 | 获取指定群计数器的 Key 列表，不填则全部返回 |

### 应答包体示例
```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0,
    "GroupCounter":[
    	{
    		"Key":"like", // 群计数器Key
    		"Value":5 // 群计数器最新Value
    	}，
    	{
    		"Key":"unlike",
    		"Value":1
    	}
    ]
}
```

### 应答包字段说明

| 字段 | 类型 | 说明 |
|---------|---------|---------|
| ActionStatus | String | 请求处理的结果，OK 表示处理成功，FAIL 表示失败 |
| ErrorCode|	Integer	|错误码，0表示成功，非0表示失败 |
| ErrorInfo | String | 错误信息  |
| GroupCounter | Array | 获取的群计数器最新键值列表 |

## 错误码说明
除非发生网络错误（例如502错误），否则该接口的 HTTP 返回码均为200。真正的错误码，错误信息是通过应答包体中的 ErrorCode、ErrorInfo 来表示的。
公共错误码（60000到79999）参见 [错误码](https://intl.cloud.tencent.com/document/product/1047/34348) 文档。
本 API 私有错误码如下：

| 错误码 | 含义说明|
|---------|---------|
| 10002 | 服务器内部错误，请重试 |
| 10004 | 参数非法，请根据错误描述检查请求是否正确 |
| 10007 | 操作权限不足，例如非群成员等 |
| 10010 | 群组不存在，或者曾经存在过，但是目前已经被解散 |
| 10015 | 群组 ID 非法，请检查群组 ID 是否填写正确，群不存在 |
| 10059 | 该特性需要购买旗舰版才可以支持 |
