## 简介

本文档提供关于存储桶策略的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名         | 操作描述                 |
| ------------------------------------------------------------ | -------------- | ------------------------ |
| [PUT Bucket policy](https://intl.cloud.tencent.com/document/product/436/8282) | 设置存储桶策略 | 设置指定存储桶的权限策略 |
| [GET Bucket policy](https://intl.cloud.tencent.com/document/product/436/8276) | 查询存储桶策略 | 查询指定存储桶的权限策略 |
| [DELETE Bucket policy](https://intl.cloud.tencent.com/document/product/436/8285) | 删除存储桶策略 | 删除指定存储桶的权限策略 |

## 设置存储桶策略

#### 功能说明

设置指定存储桶的权限策略。

#### 请求示例

[//]: # (.cssg-snippet-put-bucket-policy)
```js
cos.putBucketPolicy({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
    Policy: {
        "version": "2.0",
        "Statement": [{
            "Effect": "allow",
            "Principal": {
                "qcs": ["qcs::cam::uin/100000000001:uin/100000000001"]
            },
            "Action": [
                "name/cos:PutObject",
                "name/cos:InitiateMultipartUpload",
                "name/cos:ListMultipartUploads",
                "name/cos:ListParts",
                "name/cos:UploadPart",
                "name/cos:CompleteMultipartUpload"
            ],
            "Resource": ["qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"],
        }]
    },
}, function(err, data) {
    console.log(err || data);
});
```

#### 参数说明

| 参数名称&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;        | 描述                                                     | 类型        | 是否必填 |
| ------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket        | 设置存储桶策略的存储桶，格式：BucketName-APPID  | String      | 是   |
| Region        | 存储桶所在地域，枚举值请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224) | String      | 是   |
| Policy        | 权限策略，详情请参见 [访问管理策略语法](https://intl.cloud.tencent.com/document/product/436/12469#.E7.AD.96.E7.95.A5.E8.AF.AD.E6.B3.95) | Object      | 是   |
| - version     | 版本号，固定2.0                                             | String      | 是   |
| - statement   | 权限策略生命列表                                             | ObjectArray | 是   |
| - - effect    | 效力，枚举值：allow、deny                                    | String      | 是   |
| - - principal | 身份信息                                                     | ObjectArray | 是   |
| - - - qcs     | 身份信息标识字符串<br>格式：`qcs::cam::uin/100000000001:uin/100000000011`<br>其中100000000001 是主账号，100000000011是子账号 | String      | 是   |
| - - action    | 策略生效的相关 Action 列表，支持通配符`*`                    | StringArray | 是   |
| - - resource  | 相关的资源标识字符串列表<br>格式：`qcs::cos:<Region>:uid/<AppId>:<ShortBucketName>/*`<br>例如：`qcs::cos:ap-beijing:uid/1250000000:examplebucket/*` | StringArray | 是   |
| - - condition | 约束条件，可以不填，具体说明请参见 [condition](https://intl.cloud.tencent.com/document/product/598/10603#6.-.E7.94.9F.E6.95.88.E6.9D.A1.E4.BB.B6.EF.BC.88condition.EF.BC.89) 说明 | String      | 否   |

#### 回调函数说明

```
function(err, data) { ... }
```

| 参数名&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;       | 参数描述                                                     | 类型   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 请求发生错误时返回的对象，包括网络错误和业务错误，如果请求成功则为空，更多详情请参见 [错误码](https://intl.cloud.tencent.com/document/product/436/7730) 文档 | Object |
| - statusCode | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number |
| - headers    | 请求返回的头部信息                                           | Object |
| data         | 请求成功时返回的对象，如果请求发生错误，则为空               | Object |
| - statusCode | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number |
| - headers    | 请求返回的头部信息                                           | Object |

## 查询存储桶策略

#### 功能说明

查询指定存储桶的权限策略。

#### 请求示例

[//]: # (.cssg-snippet-get-bucket-policy)
```js
cos.getBucketPolicy({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 返回示例

```json
{
    "Policy": {
        "version": "2.0",
        "Statement": [{
            "Action": [
                "name/cos:PutObject",
                "name/cos:InitiateMultipartUpload",
                "name/cos:ListMultipartUploads",
                "name/cos:ListParts",
                "name/cos:UploadPart",
                "name/cos:CompleteMultipartUpload"
            ],
            "Effect": "allow",
            "Principal": {
                "qcs": ["qcs::cam::uin/100000000001:uin/100000000001"]
            },
            "Resource": ["qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/*"],
            "Sid": "costs-1539833197000000307620-46518-39"
        }]
    },
    "statusCode": 200,
    "headers": {}
}
```

#### 参数说明

| 参数名称 | 描述                                                     | 类型   | 是否必填 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 查询存储桶权限策略的存储桶，格式：BucketName-APPID | String | 是   |
| Region | 存储桶所在地域，枚举值请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224) | String | 是   |

#### 回调函数说明

```
function(err, data) { ... }
```

| 参数名&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;          | 参数描述                                                     | 类型        |
| --------------- | ------------------------------------------------------------ | ----------- |
| err             | 请求发生错误时返回的对象，包括网络错误和业务错误，如果请求成功则为空，更多详情请参见 [错误码](https://intl.cloud.tencent.com/document/product/436/7730) 文档 | Object      |
| data            | 请求成功时返回的对象，如果请求发生错误，则为空               | Object      |
| - Policy        | 权限策略，详情请参见 [访问管理策略语法](https://intl.cloud.tencent.com/document/product/436/12469#.E7.AD.96.E7.95.A5.E8.AF.AD.E6.B3.95) | Object      |
| - - version     | 版本号，固定2.0                                              | String      |
| - - Statement   | 权限策略生命列表                                             | ObjectArray |
| - - - effect    | 效力，枚举值：allow、deny                                    | String      |
| - - - principal | 身份信息                                                     | ObjectArray |
| - - - - qcs     | 身份信息标识字符串<br>格式：`qcs::cam::uin/100000000001:uin/100000000011`<br>其中100000000001是主账号，100000000011是子账号 | String      |
| - - - action    | 策略生效的相关 Action 列表，支持通配符`*`                    | StringArray |
| - - - resource  | 相关的资源标识字符串列表<br>格式：`qcs::cos:<Region>:uid/&ltAppId>:<ShortBucketName>/*`<br>例如：`qcs::cos:ap-beijing:uid/1250000000:examplebucket/*` | StringArray |
| - - - condition | 约束条件，可以不填，具体说明请参见 [condition](https://intl.cloud.tencent.com/document/product/598/10603#6.-.E7.94.9F.E6.95.88.E6.9D.A1.E4.BB.B6.EF.BC.88condition.EF.BC.89) 说明 | ObjectArray |

## 删除存储桶策略

#### 功能说明

DELETE Bucket policy 请求删除指定存储桶的权限策略。

>只有 Bucket 所有者有权限发起该请求。如果权限策略不存在，将返回204 No Content。

#### 请求示例

[//]: # (.cssg-snippet-delete-bucket-policy)
```js
cos.deleteBucketPolicy({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 参数说明

| 参数名 | 参数描述                                                     | 类型   | 是否必填 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 被删除存储桶权限策略的存储桶，格式：BucketName-APPID | String | 是   |
| Region | 存储桶所在地域，枚举值请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224) | String | 是   |

#### 回调函数说明

```
function(err, data) { ... }
```

| 参数名&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;       | 参数描述                                                     | 类型   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 请求发生错误时返回的对象，包括网络错误和业务错误，如果请求成功则为空，更多详情请参见 [错误码](https://intl.cloud.tencent.com/document/product/436/7730) 文档 | Object |
| - statusCode | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number |
| - headers    | 请求返回的头部信息                                           | Object |
| data         | 请求成功时返回的对象，如果请求发生错误，则为空               | Object |
| - statusCode | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number |
| - headers    | 请求返回的头部信息                                           | Object |
