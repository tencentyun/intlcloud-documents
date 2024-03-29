对象存储（Cloud Object Storage，COS）可以在上传对象时，对上传的文件类型、大小进行限制。限制上传的文件类型，可以保证您的存储桶中不会存放不符合预期的文件；限制上传的文件大小，可以方便您更加灵活管理存储空间，避免上传过大、过小文件浪费存储空间与网络带宽。下面列举了两个案例介绍如何精细化地控制上传文件的大小。

## 准备工作

在以下案例中，会使用到如下信息：
- 主账号的 APPID：1250000000
- 存储桶名称：examplebucket-1250000000




## 案例一：通过 POST Object 接口在上传对象时指定对象大小范围

在使用 POST Object 上传对象，可以在表单里添加字段 “content-length-range” 以限制此次请求的对象大小，格式如下所示：

```plaintext
[ "content-length-range", minNum, maxNum ]
```

示例如下：

```plaintext
[ "content-length-range", 1, 10]
```

该字段以 JSON 形式添加在 POST 请求表单中的策略（policy）-条件（condition）里。一个带有该字段的完整策略（policy）如下：

```plaintext
 {
    "expiration": "2021-12-31T12:00:00Z",
    "conditions": [
        { "bucket": "examplebucket-1250000000" },
        [ "starts-with", "$key", "exampleobject" ],
        { "q-ak": "AKIDQjz3ltompVjBni5LitkWHFlFpwkn****" },
        { "q-sign-algorithm": "sha1" },
        { "q-sign-time": "1567150692;1567157892" },
        [ "content-length-range", 1, 10 ]
    ]
}
```

如何构造完整的请求，请参见 [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) API 文档。

#### 响应

当上传的对象文件大小满足条件时，返回成功，例如：

```plaintext
HTTP/1.1 204 
Content-Length: 0
Connection: close
Date: Wed, 23 Aug 2020 08:14:53 GMT
ETag: "ee8de918d05640145b18f70f4c3aa602"
Location: http://examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject
Server: tencent-cos
x-cos-request-id: NWQ2NzgxMzZfMmViMDJhMDlfY2NjOF84NGQz****
```

当上传的对象文件大小超出指定范围时，返回失败。

若对象过大，则响应如下：

```plaintext
HTTP/1.1 400 Bad Request
Content-Type: application/xml
Content-Length: 498
Connection: keep-alive
Date: Wed, 23 Aug 2020 08:14:53 GMT
Server: tencent-cos
x-cos-request-id: NTk5ZDM5N2RfMjNiMjM1MGFfMmRiX2Y0****



<?xml version='1.0' encoding='utf-8' ?>
<Error>
        <Code>EntityTooLarge</Code>
        <Message>Condition key content-length-range doesn‘t match the value </Message>
        <Resource>examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject</Resource>
        <RequestId>NTk5ZDM5N2RfMjNiMjM1MGFfMmRiX2Y0****</RequestId>
</Error>
```

若对象过小，则响应如下：

```plaintext
HTTP/1.1 400 Bad Request
Content-Type: application/xml
Content-Length: 498
Connection: keep-alive
Date: Wed, 23 Aug 2020 08:14:53 GMT
Server: tencent-cos
x-cos-request-id: NTk5ZDM5N2RfMjNiMjM1MGFfMmRiX2Y0****



<?xml version='1.0' encoding='utf-8' ?>
<Error>
        <Code>EntityTooSmall</Code>
        <Message>Condition key content-length-range doesn‘t match the value </Message>
        <Resource>examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/exampleobject</Resource>
        <RequestId>NTk5ZDM5N2RfMjNiMjM1MGFfMmRiX2Y0****</RequestId>
</Error>
```



## 案例二：通过临时密钥指定对象大小范围

案例一的优点是使用简单，只需要在请求表单里添加一个参数即可实现。但缺点是只支持 POST Object 接口，不支持 PUT Object 接口；不利于统一管理，请求执行者可以在生成请求时修改限制参数，导致可上传限制范围之外的对象大小。

存储桶的管理人员可以在申请临时密钥时，使用以下字段来限制对象大小，COS 对象大小使用字段 cos:content_length 来表示：

| 条件字段                   | 含义         | 示例                                                         |
| -------------------------- | ------------ | ------------------------------------------------------------ |
| numeric_greater_than       | 数值大于     | {"numeric_greater_than": {"cos:content_length": 1}}，对象必须大于1byte |
| numeric_greater_than_equal | 数值大于等于 | {"numeric_greater_than_equal": {"cos:content_length": 1}}，对象必须大于或者等于1byte |
| numeric_less_than          | 数值小于     | {"numeric_less_than": {"cos:content_length": 1}}，对象必须小于1byte |
| numeric_less_than_equal    | 数值小于等于 | {"numeric_less_than_equal": {"cos:content_length": 1}}，对象必须小于或者等于1byte |

完整请求可参考STS 的获取临时访问凭证API 文档，一个完整的策略（policy）如下：

```plaintext
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cos:PutObject",
                "cos:PostObject",
            ],
            "resource": [
                "qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"
            ],

            "condition": {
                "numeric_greater_than_equal": {"cos:content_length": 1}
                , "numeric_less_than": {"cos:content_length": 10}
            }
        }
    ]
}
```

使用这个策略申请到的临时认证，可以使用 PUT Object 与 POST Object 接口将对象上传至存储桶 examplebucket-1250000000，但是对象大小的限制范围为[1, 10) byte。

>! 此策略当前只适用于 `cos:PutObject`、`cos:PostObject` 这两个 action，其他 action（例如 `cos:GetObject`）会失败。
>

通过这种机制，可以由存储桶的管理人员或者“认证中心”统一的向 STS 申请临时密钥，在申请时完成限定对象大小，再将临时密钥发放给操作人员或者业务模块。这样就能保证上传的对象符合我们预期，避免请求参数被篡改。

#### 响应

如果上传的对象符合限定大小，上传请求成功，则返回200或者204。如果上传对象超出了限定范围，则返回403失败，示例如下：

```plaintext
HTTP/1.1 403 Forbidden
Content-Type: application/xml
Content-Length: 298
Connection: keep-alive
Date: Wed, 23 Aug 2020 08:14:53 GMT
Server: tencent-cos
x-cos-request-id: NTk5ZDM5N2RfMjNiMjM1MGFfMmRiX2Y0****
```





