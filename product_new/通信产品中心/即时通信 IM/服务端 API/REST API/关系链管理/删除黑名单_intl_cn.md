## 功能说明
删除指定黑名单。

## 接口调用说明
### 请求 URL 示例
```
https://xxxxxx/v4/sns/black_list_delete?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```
其中 `xxxxxx` 是各国家/地区的专属域名，请填写您的 SDKAppID 所在国家/地区对应的专属域名：  

| 国家/地区   | 专属域名|
| ----- | ----- |
| 新加坡 | adminapisgp.im.qcloud.com      |

### 请求参数说明

下表仅列出调用本接口时涉及修改的参数及其说明，更多参数详情请参考 [REST API 简介](https://intl.cloud.tencent.com/document/product/1047/34620)。

| 参数               | 说明                                 |
| ------------------ | ------------------------------------ |
| v4/sns/black_list_delete  | 请求接口                             |
| sdkappid           | 创建应用时即时通信 IM 控制台分配的 SDKAppID |
| identifier         | 必须为 App 管理员帐号，更多详情请参见 [App 管理员](https://intl.cloud.tencent.com/document/product/1047/33517#app-.E7.AE.A1.E7.90.86.E5.91.98)                |
| usersig            | App 管理员帐号生成的签名，具体操作请参见 [生成 UserSig](https://intl.cloud.tencent.com/document/product/1047/34385)    |
| random             | 请输入随机的32位无符号整数，取值范围0 - 4294967295                 |

### 最高调用频率

200次/秒。

### 请求包示例

```
{
 "From_Account":"id",
 "To_Account":["id1","id2","id3"]
}
```


### 请求包字段说明

|字段|类型|属性|说明|
|----|----|----|-----|
| From_Account  | String  |  必填 | 需要删除该 Identifier 的黑名单  |
| To_Account  |  Array | 必填  |  待删除的黑名单的 Identifier 列表，单次请求的 To_Account 数不得超过1000 |

### 应答包体示例

```
{
	"ResultItem":
	[
		{
			"To_Account":"id1",
			"ResultCode":0,
			"ResultInfo":""
		},
		{
			"To_Account":"id2",
			"ResultCode":0,
			"ResultInfo":""
		},
		{
			"To_Account":"id3",
			"ResultCode":30006,
			"ResultInfo":"Err_SNS_BlackListCheck_Check_Reverse_BlackList_Fail"
		}
	],
	"Fail_Account":["id3"],
	"ActionStatus":"OK",
	"ErrorCode":0,
	"ErrorInfo":"",
	"ErrorDisplay":""
}
```

### 应答包字段说明

| 字段 | 类型 |说明|
|----|----|-----|
| ResultItem|	Array	|批量删除黑名单的结果对象数组|
| To_Account|	String	|请求删除的黑名单的 Identifier|
| ResultCode|	Integer	|To_Account 的处理结果，0表示成功，非0表示失败|
| ResultInfo|	String|	To_Account 的错误描述信息，成功时该字段为空|
| Fail_Account|Array|返回处理失败的用户列表，仅当存在失败用户时才返回该字段|
| ActionStatus	|String| 请求包的处理结果，“OK” 表示处理成功，“FAIL” 表示失败 |
| ErrorCode|	Integer	|错误码，0表示成功，非0表示失败 |
| ErrorInfo	|String| 详细错误信息 |
| ErrorDisplay|	String| 详细的客户端展示信息 |


### 错误码说明

除非发生网络错误（例如502错误），否则该接口的 HTTP 返回码均为200；真正的错误码、错误信息是通过应答包体中的 ErrorCode、ErrorInfo 来表示的。
公共错误码（60000到79999）参见 [错误码](https://intl.cloud.tencent.com/document/product/1047/34348) 文档。
本 API 私有错误码如下：

| 错误码 | 描述                                                         |
| ------ | ------------------------------------------------------------ |
| 30001  | 请求参数错误，请根据错误描述检查请求参数                     |
| 30003  | 请求的用户帐号不存在                                         |
| 30004  | 请求需要 App 管理员权限                                      |
| 30006  | 服务器内部错误，请重试                                       |
| 30007  | 网络超时，请稍后重试                                         |
| 30008  | 并发写导致写冲突，建议使用批量方式                           |


## 接口调试工具
通过 [REST API 在线调试工具](https://avc.cloud.tencent.com/im/APITester/APITester.html#v4/sns/black_list_delete) 调试本接口。

## 参考

- 删除黑名单（<a href="https://intl.cloud.tencent.com/document/product/1047/34912">v4/sns/black_list_delete</a>）
- 拉取黑名单（<a href="https://intl.cloud.tencent.com/document/product/1047/34914">v4/sns/black_list_get</a>）
- 校验黑名单（<a href="https://intl.cloud.tencent.com/document/product/1047/34913">v4/sns/black_list_check</a>）

## 可能触发的回调
<a href="https://intl.cloud.tencent.com/document/product/1047/34362">删除黑名单之后回调</a>
