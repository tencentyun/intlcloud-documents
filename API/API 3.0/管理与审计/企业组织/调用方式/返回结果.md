## 正确返回结果

以云服务器的接口查看实例状态列表 (DescribeInstancesStatus) 2017-03-12 版本为例，若调用成功，其可能的返回如下为：

    {
        "Response": {
            "TotalCount": 0,
            "InstanceStatusSet": [],
            "RequestId": "b5b41468-520d-4192-b42f-595cc34b6c1c"
        }
    }

* Response 及其内部的 RequestId 是固定的字段，无论请求成功与否，只要 API 处理了，则必定会返回。
* RequestId 用于一个 API 请求的唯一标识，如果 API 出现异常，可以联系我们，并提供该 ID 来解决问题。
* 除了固定的字段外，其余均为具体接口定义的字段，不同的接口所返回的字段参见接口文档中的定义。此例中的 TotalCount 和 InstanceStatusSet 均为 DescribeInstancesStatus 接口定义的字段，由于调用请求的用户暂时还没有云服务器实例，因此 TotalCount 在此情况下的返回值为 0， InstanceStatusSet 列表为空。

## 错误返回结果

若调用失败，其返回值示例如下为：

    {
        "Response": {
            "Error": {
                "Code": "AuthFailure.SignatureFailure",
                "Message": "The provided credentials could not be validated. Please check your signature is correct."
            },
            "RequestId": "ed93f3cb-f35e-473f-b9f3-0d451b8b79c6"
        }
    }

* Error 的出现代表着该请求调用失败。Error 字段连同其内部的 Code 和 Message 字段在调用失败时是必定返回的。
* Code 表示具体出错的错误码，当请求出错时可以先根据该错误码在公共错误码和当前接口对应的错误码列表里面查找对应原因和解决方案。
* Message 显示出了这个错误发生的具体原因，随着业务发展或体验优化，此文本可能会经常保持变更或更新，用户不应依赖这个返回值。
* RequestId 用于一个 API 请求的唯一标识，如果 API 出现异常，可以联系我们，并提供该 ID 来解决问题。


## 公共错误码


返回结果中如果存在 Error 字段，则表示调用 API 接口失败。 Error 中的 Code 字段表示错误码，所有业务都可能出现的错误码为公共错误码，下表列出了公共错误码。


| 错误码 | 错误描述 |
|----------|----------|
| AuthFailure.InvalidSecretId | 密钥非法（不是云 API 密钥类型）。 |
| AuthFailure.MFAFailure | MFA 错误。 |
| AuthFailure.SecretIdNotFound | 密钥不存在。 |
| AuthFailure.SignatureExpire | 签名过期。 |
| AuthFailure.SignatureFailure | 签名错误。 |
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
| UnsupportedProtocol | HTTPS 请求方法错误，只支持 GET 和 POST 请求。 |
| UnsupportedRegion | 接口不支持所传地域。 |
