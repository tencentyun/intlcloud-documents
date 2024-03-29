## 简介

本文档提供关于跨地域复制的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名         | 操作描述                   |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | 设置跨地域复制 | 设置存储桶的跨地域复制规则 |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | 查询跨地域复制 | 查询存储桶的跨地域复制规则 |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | 删除跨地域复制 | 删除存储桶的跨地域复制规则 |

## 设置跨地域复制

#### 功能说明

设置存储桶的跨地域复制规则。

> 存储桶必须开启版本控制才能使用跨地域复制功能。

#### 请求示例

[//]: # (.cssg-snippet-put-bucket-replication)
```js
cos.putBucketReplication({
    Bucket: 'examplebucket-1250000000',  /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
    ReplicationConfiguration: { /* 必须 */
        Role: "qcs::cam::uin/100000000001:uin/100000000001",
        Rules: [{
            ID: "1",
            Status: "Enabled",
            Prefix: "sync/",
            Destination: {
                Bucket: "qcs::cos:ap-beijing::destinationbucket-1250000000",
                StorageClass: "Standard",
            }
        }]
    }
}, function (err, data) {
    console.log(err || data);
});
```

#### 参数说明

| 参数名称                   | 描述                                                     | 类型        | 是否必填 |
| ------------------------ | ------------------------------------------------------------ | ----------- | ---- |
| Bucket                   | 源存储桶，格式：BucketName-APPID                            | String      | 是   |
| Region                   | 存储桶所在地域，枚举值请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224) | String      | 是   |
| ReplicationConfiguration | 定义跨地域复制规则                                           | Object      | 是   |
| - Role                   | 复制过程以什么角色的身份<br>格式：`qcs::cam::uin/100000000001:uin/100000000011`<br>其中100000000001是主账号，100000000011是子账号 | Object      | 否   |
| - Rules                  | 复制具体规则列表                                             | ObjectArray | 是   |
| - - ID                   | 标注具体 Rule 的 ID                                          | String      | 否   |
| - - Status               | 标识 Rule 是否生效，枚举值：Enabled、Disabled                | String      | 是   |
| - - Prefix               | 前缀匹配策略，不可重叠，重叠返回错误。前缀匹配根目录为空     | String      | 否   |
| - - Destination          | 目标存储桶信息                                               | Object      | 是   |
| - - - Bucket             | 目标存储桶的名称<br>格式：`qcs::cos:<Region>::<BucketName-APPID>`<br>例如：`qcs::cos:ap-beijing::destinationbucket-1250000000` | Object      | 是   |
| - - - StorageClass       | 复制后的存储类型，枚举值：STANDARD、STANDARD_IA、ARCHIVE，默认值：STANDARD | Object      | 否   |

#### 回调函数说明

```
function(err, data) { ... }
```

| 参数名称&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;                   | 描述                                                     | 类型    |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 请求发生错误时返回的对象，包括网络错误和业务错误，如果请求成功则为空，详情请参见 [错误码](https://intl.cloud.tencent.com/document/product/436/7730) 文档 | Object |
| - statusCode | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number |
| - headers    | 请求返回的头部信息                                           | Object |
| data         | 请求成功时返回的对象，如果请求发生错误，则为空               | Object |
| - statusCode | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number |
| - headers    | 请求返回的头部信息                                           | Object |

## 查询跨地域复制

#### 功能说明

查询存储桶的跨地域复制规则。

#### 请求示例

[//]: # (.cssg-snippet-get-bucket-replication)
```js
cos.getBucketReplication({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 返回示例

```json
{
    "ReplicationConfiguration": {
        "Role": "qcs::cam::uin/100000000001:uin/100000000001",
        "Rules": {
            "ID": "1",
            "Status": "Enabled",
            "Prefix": "sync/",
            "Destination": {
                "Bucket": "qcs::cos:ap-beijing::destinationbucket-1250000000",
                "StorageClass": "Standard"
            }
        }
    },
    "statusCode": 200,
    "headers": {}
}
```

#### 参数说明

| 参数名称                   | 描述                                                     | 类型    | 是否必填 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 查询跨地域复制的存储桶，格式：BucketName-APPID | String | 是   |
| Region | 存储桶所在地域，枚举值请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224) | String | 是   |

#### 回调函数说明

```
function(err, data) { ... }
```

| 参数名称&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;                     | 描述                                                     | 类型        |
| -------------------------- | ------------------------------------------------------------ | ----------- |
| err                        | 请求发生错误时返回的对象，包括网络错误和业务错误，如果请求成功则为空，详情请参见 [错误码](https://intl.cloud.tencent.com/document/product/436/7730) 文档 | Object      |
| data                       | 请求成功时返回的对象，如果请求发生错误，则为空               | Object      |
| - ReplicationConfiguration | 跨地域复制规则                                               | Object      |
| - - Role                   | 复制过程以什么角色的身份<br>格式：`qcs::cam::uin/100000000001:uin/100000000011`<br>其中100000000001是主账号，100000000011是子账号 | Object      |
| - - Rules                  | 复制具体规则列表                                             | ObjectArray |
| - - - ID                   | 标注具体 Rule 的 ID                                          | String      |
| - - - Status               | 标识 Rule 是否生效，枚举值：Enabled、Disabled                | String      |
| - - - Prefix               | 前缀匹配策略，不可重叠，重叠返回错误。前缀匹配根目录为空     | String      |
| - - - Destination          | 目标存储桶信息                                               | Object      |
| - - - - Bucket             | 目标存储桶的名称<br>格式：`qcs::cos:<Region>::<BucketName-APPID>`<br>例如：`qcs::cos:ap-beijing::destinationbucket-1250000000` | Object      |
| - - - - StorageClass       | 复制后的存储类型，枚举值：STANDARD、STANDARD_IA、ARCHIVE，默认值：STANDARD | Object      |


## 删除跨地域复制

#### 功能说明

删除存储桶的跨地域复制规则。

#### 请求示例

[//]: # (.cssg-snippet-delete-bucket-replication)
```js
cos.deleteBucketReplication({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 参数说明

| 参数名称 |描述                                                     | 类型   | 是否必填 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 删除跨地域复制的存储桶，格式：BucketName-APPID | String | 是   |
| Region | 存储桶所在地域，枚举值请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224) | String | 是   |

#### 回调函数说明

```
function(err, data) { ... }
```

| 参数名&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;       | 参数描述                                                     | 类型   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 请求发生错误时返回的对象，包括网络错误和业务错误，如果请求成功则为空，详情请参见 [错误码](https://intl.cloud.tencent.com/document/product/436/7730) 文档 | Object |
| - statusCode | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number |
| - headers    | 请求返回的头部信息                                           | Object |
| data         | 请求成功时返回的对象，如果请求发生错误，则为空               | Object |
| - statusCode | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number |
| - headers    | 请求返回的头部信息                                           | Object |
