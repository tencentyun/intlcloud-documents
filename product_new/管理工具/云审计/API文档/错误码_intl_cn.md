
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
| UnsupportedOperation | 操作不支持。 |
| ResourceInUse | 资源被占用。 |
| InternalError | 内部错误。 |
| RequestLimitExceeded | 请求的次数超过了频率限制。 |
| AuthFailure.SecretIdNotFound | 密钥不存在。 请在控制台检查密钥是否已被删除或者禁用，如状态正常，请检查密钥是否填写正确，注意前后不得有空格。 |
| LimitExceeded | 超过配额限制。 |
| NoSuchVersion | 接口版本不存在。 |
| ResourceNotFound | 资源不存在。 |
| AuthFailure.SignatureFailure | 签名错误。 签名计算错误，请对照调用方式中的接口鉴权文档检查签名计算过程。 |
| AuthFailure.SignatureExpire | 签名过期。Timestamp 和服务器时间相差不得超过五分钟，请检查本地时间是否和标准时间同步。 |
| UnsupportedRegion | 接口不支持所传地域。 |
| UnauthorizedOperation | 未授权操作。 |
| InvalidParameter | 参数错误。 |
| ResourceUnavailable | 资源不可用。 |
| AuthFailure.MFAFailure | MFA 错误。 |
| AuthFailure.UnauthorizedOperation | 请求未授权。请参考 [CAM](https://intl.cloud.tencent.com/document/product/598) 文档对鉴权的说明。 |
| AuthFailure.InvalidSecretId | 密钥非法（不是云 API 密钥类型）。 |
| AuthFailure.TokenFailure | token 错误。 |
| DryRunOperation | DryRun 操作，代表请求将会是成功的，只是多传了 DryRun 参数。 |
| FailedOperation | 操作失败。 |
| UnknownParameter | 未知参数错误。 |
| UnsupportedProtocol | HTTP(S)请求协议错误，只支持 GET 和 POST 请求。 |
| InvalidParameterValue | 参数取值错误。 |
| InvalidAction | 接口不存在。 |
| MissingParameter | 缺少参数错误。 |
| ResourceInsufficient | 资源不足。 |


### 业务错误码



| 错误码 | 说明 |
|:-------|:-----|
| InternalError.CmqError | 创建cmq时发生异常，可能您准备创建的cmq队列已经存在，也有可能您没有权限或者欠费。 |
| InternalError.CreateAuditError | 创建跟踪集错误，请联系开发人员。 |
| InternalError.DeleteAuditError | 删除跟踪集失败，请联系开发人员 |
| InternalError.DescribeAuditError | 查看跟踪集详情错误，请联系开发人员 |
| InternalError.InquireAuditCreditError | 查询可创建跟踪集的数量错误，请联系开发人员 |
| InternalError.ListAuditsError | 查询跟踪集概要内部错误，请联系开发人员。 |
| InternalError.ListCmqEnableRegionError | 内部错误，请联系开发人员 |
| InternalError.ListCosEnableRegionError | 内部错误，请联系开发人员 |
| InternalError.SearchError | 内部错误，请联系开发人员 |
| InternalError.StartLoggingError | 内部错误，请联系开发人员 |
| InternalError.StopLoggingError | 内部错误，请联系开发人员 |
| InternalError.UpdateAuditError | 内部错误，请联系开发人员 |
| InvalidParameter.Time | 必须包含开始时间和结束时间，且必须为整形时间戳（精确到秒） |
| InvalidParameterValue.AuditNameError | 跟踪集名称不符合规则 |
| InvalidParameterValue.CmqRegionError | 云审计目前不支持输入的cmq地域 |
| InvalidParameterValue.CosNameError | 输入的cos存储桶名称不符合规范 |
| InvalidParameterValue.CosRegionError | 云审计目前不支持输入的cos地域 |
| InvalidParameterValue.IsCreateNewBucketError | IsCreateNewBucket的有效取值范围是0和1，0代表不创建新的存储桶，1代表创建新的存储桶。 |
| InvalidParameterValue.IsCreateNewQueueError | IsCreateNewQueue的有效取值范围是0和1，0代表不新创建，1代表新创建。 |
| InvalidParameterValue.IsEnableCmqNotifyError | IsEnableCmqNotify的有效取值范围是0和1，0代表不开启投递cmq,1代表开启cmq投递。 |
| InvalidParameterValue.LogFilePrefixError | 日志前缀格式错误 |
| InvalidParameterValue.MaxResult | 单次检索支持的最大返回条数是50 |
| InvalidParameterValue.QueueNameError | 输入的队列名称不符合规范 |
| InvalidParameterValue.ReadWriteAttributeError | 读写属性值仅支持：1,2,3。1代表只读，2代表只写，3代表全部。 |
| InvalidParameterValue.Time | 开始时间不能大于结束时间 |
| InvalidParameterValue.attributeKey | AttributeKey的有效取值范围是:RequestId、EventName、ReadOnly、Username、ResourceType、ResourceName和AccessKeyId |
| LimitExceeded.OverAmount | 超过跟踪集的最大值 |
| LimitExceeded.OverTime | 检索支持的有效时间范围是7天 |
| MissingParameter.MissAuditName | 缺少跟踪集名称 |
| MissingParameter.MissCosBucketName | 缺少cos存储桶参数 |
| MissingParameter.MissCosRegion | 缺少cos地域参数 |
| MissingParameter.cmq | IsEnableCmqNotify输入1的话，IsCreateNewQueue、CmqQueueName和CmqRegion都是必须参数。 |
| ResourceInUse.AlreadyExistsSameAudit | 已经存在相同名称的跟踪集 |
| ResourceInUse.AlreadyExistsSameAuditCmqConfig | 已经存在相同cmq投递配置的跟踪集 |
| ResourceInUse.AlreadyExistsSameAuditCosConfig | 已经存在相同cos投递配置的跟踪集 |
| ResourceInUse.CosBucketExists | cos存储桶已经存在 |
| ResourceNotFound.AuditNotExist | 跟踪集不存在 |
