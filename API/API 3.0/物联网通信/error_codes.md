
## 功能说明

如果返回结果中存在 Error 字段，则表示调用 API 接口失败。例如：

```
 {
    "Response": {
        "Error": {
            "Code": "AuthFailure.SignatureFailure",
            "Message": "The provided credentials could not be validated. Please check your signature is correct."
        },
        "RequestId": "ed93f3cb-f35e-473f-b9f3-0d451b8b79c6"
    }
}
```

Error 中的 Code 表示错误码，Message 表示该错误的具体信息。

## 错误码列表

### 公共错误码

| 错误码 | 说明 |
|--------|------|
| AuthFailure.InvalidSecretId | 密钥非法（不是云 API 密钥类型）。 |
| AuthFailure.MFAFailure | MFA 错误。 |
| AuthFailure.SecretIdNotFound | 密钥不存在。 请在控制台检查密钥是否已被删除或者禁用，如状态正常，请检查密钥是否填写正确，注意前后不得有空格。|
| AuthFailure.SignatureExpire | 签名过期。Timestamp 和服务器时间相差不得超过五分钟，请检查本地时间是否和标准时间同步。|
| AuthFailure.SignatureFailure | 签名错误。 签名计算错误，请对照调用方式中的接口鉴权文档检查签名计算过程。|
| AuthFailure.TokenFailure | token 错误。 |
| AuthFailure.UnauthorizedOperation | 请求未 CAM 授权。 |
| DryRunOperation | DryRun 操作，代表请求将会是成功的，只是多传了 DryRun 参数。 |
| FailedOperation | 操作失败。 |
| InternalError | 内部错误。 |
| InvalidAction | 接口不存在。 |
| InvalidParameter | 参数错误。 |
| InvalidParameterValue | 参数取值错误。 |
| LimitExceeded | 超过配额限制。 |
| MissingParameter | 缺少参数错误。 |
| NoSuchVersion | 接口版本不存在。 |
| RequestLimitExceeded | 请求的次数超过了频率限制。 |
| ResourceInUse | 资源被占用。 |
| ResourceInsufficient | 资源不足。 |
| ResourceNotFound | 资源不存在。 |
| ResourceUnavailable | 资源不可用。 |
| UnauthorizedOperation | 未授权操作。 |
| UnknownParameter | 未知参数错误。 |
| UnsupportedOperation | 操作不支持。 |
| UnsupportedProtocol | http(s)请求协议错误，只支持 GET 和 POST 请求。 |
| UnsupportedRegion | 接口不支持所传地域。 |

### 业务错误码

| 错误码 | 说明 |
|:-------|:-----|
| FailedOperation.AsyncTaskAlreadyStarted | 任务已经开始。 |
| FailedOperation.InvalidMsgLen | 消息长度非法。 |
| FailedOperation.InvalidTopicName | 消息topic非法。 |
| FailedOperation.TaskIDNotMatch | 用户或产品不匹配任务ID。 |
| FailedOperation.UpdateVersionNotMatch | 更新版本不匹配。 |
| InternalError | 内部错误 |
| InvalidParameterValue | 参数取值错误 |
| InvalidParameterValue.DeviceAlreadyExist | 创建的设备名已存在。 |
| InvalidParameterValue.InvalidSQL | SQL语句含有非法字符。 |
| InvalidParameterValue.JSONHasInvalidNode | State JSON对象中包含非法节点。 |
| InvalidParameterValue.JSONLevelExceedLimit | State JSON对象的层数超过了限制，最大为 6 层。 |
| InvalidParameterValue.JSONSizeExceedLimit | State JSON对象超过大小限制，最大为 64k。 |
| InvalidParameterValue.ParamIncomplete | 请求中缺少关键字段信息。 |
| InvalidParameterValue.ProductAlreadyExist | 创建的产品名已存在。 |
| InvalidParameterValue.ProductTypeNotSupport | 产品类型不支持。 |
| InvalidParameterValue.TopicRuleAlreadyExist | 规则已存在。 |
| LimitExceeded.DeviceExceedLimit | 设备数量超过限制。 |
| LimitExceeded.PengingOrProcessingTasksExceedLimit | 等待和处理中的任务数过多。 |
| LimitExceeded.ProductExceedLimit | 超过产品数量限制。 |
| ResourceNotFound.DeviceNotExist | 设备不存在。 |
| ResourceNotFound.DeviceShadowNotExist | 设备影子不存在。 |
| ResourceNotFound.ProductNotExist | 产品不存在。 |
| ResourceNotFound.ProductOrDeviceNotExist | 用户不存在此产品或设备。 |
| ResourceNotFound.TaskNotExist | 任务不存在。 |
| UnauthorizedOperation.DeviceHasAlreadyBindGateway | 该设备绑定了网关设备，无法删除。 |
| UnauthorizedOperation.DevicesExistUnderProduct | 删除的产品下还包括未删除的设备。 |
| UnauthorizedOperation.GatewayHasBindedDevices | 该设备下仍有绑定的设备。 |
| UnauthorizedOperation.ProductCantHaveLoRaDevice | 该产品类型不能创建LoRa设备。 |
| UnauthorizedOperation.ProductCantHaveNotLoRaDevice | 该产品类型只能创建LoRa设备。 |
| UnauthorizedOperation.ProductNotSupportPSK | 产品不支持密钥认证。 |
| UnsupportedOperation.GatewayProductHasBindedProduct | 网关产品下存在绑定的子产品，无法删除。 |
| UnsupportedOperation.ProductHasBindGateway | 存在网关设备绑定当前产品，无法删除。 |
| UnsupportedOperation.ProductHasBindedGatewayProduct | 产品存在绑定的网关产品，无法删除。 |
