## 简介

本文档提供关于生命周期的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名       | 操作描述                       |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | 设置生命周期 | 设置存储桶的生命周期管理的配置 |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | 查询生命周期 | 查询存储桶生命周期管理的配置   |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | 删除生命周期 | 删除存储桶生命周期管理的配置   |

## 设置生命周期

#### 功能说明

设置指定存储桶的生命周期配置信息（PUT Bucket lifecycle）。

#### 请求示例

示例一：上传30天后，当前版本沉降至低频存储。

[//]: # (.cssg-snippet-put-bucket-lifecycle)
```js
cos.putBucketLifecycle({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
    Rules: [{
        "ID": "1",
        "Status": "Enabled",
        "Filter": {},
        "Transition": {
            "Days": "30",
            "StorageClass": "STANDARD_IA"
        }
    }],
}, function(err, data) {
    console.log(err || data);
});
```

示例二：指定目录前缀`dir/`，上传90天后，当前版本沉降至归档存储。

[//]: # (.cssg-snippet-put-bucket-lifecycle-archive)
```js
cos.putBucketLifecycle({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
    Rules: [{
        "ID": "2",
        "Filter": {
            "Prefix": "dir/",
        },
        "Status": "Enabled",
        "Transition": {
            "Days": "90",
            "StorageClass": "ARCHIVE"
        }
    }],
}, function(err, data) {
    console.log(err || data);
});
```

示例三：上传180天后，清理过期文件删除标记。

[//]: # (.cssg-snippet-put-bucket-lifecycle-expired)
```js
cos.putBucketLifecycle({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
    Rules: [{
        "ID": "3",
        "Status": "Enabled",
        "Filter": {},
        "Expiration": {
            "Days": "180"
        }
    }],
}, function(err, data) {
    console.log(err || data);
});
```

示例四：上传30天后，删除碎片。

[//]: # (.cssg-snippet-put-bucket-lifecycle-cleanAbort)
```js
cos.putBucketLifecycle({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
    Rules: [{
        "ID": "4",
        "Status": "Enabled",
        "Filter": {},
        "AbortIncompleteMultipartUpload": {
            "DaysAfterInitiation": "30"
        }
    }],
}, function(err, data) {
    console.log(err || data);
});
```

示例五：历史版本生成30天后沉降至归档存储。

[//]: # (.cssg-snippet-put-bucket-lifecycle-historyArchive)
```js
cos.putBucketLifecycle({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
    Rules: [{
        "ID": "5",
        "Status": "Enabled",
        "Filter": {},
        "NoncurrentVersionTransition": {
            "NoncurrentDays": "30",
            "StorageClass": 'ARCHIVE'
        }
    }],
}, function(err, data) {
    console.log(err || data);
});
```

#### 参数说明

| 参数名称  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;                       | 描述                                                     | 类型        | 是否必填 |
| -------------------------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket                           | 设置生命周期的存储桶，格式：BucketName-APPID  | String      | 是   |
| Region                           | 存储桶所在地域，枚举值请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224) | String      | 是   |
| Rules                            | 指定生命周期规则列表                                         | ObjectArray | 是   |
| - ID                             | 规则的唯一标识 ID                                            | String      | 是   |
| - Status                         | 规则的开启状态，枚举值：Enabled、Disabled                    | String      | 是   |
| - Filter                         | 指定过滤条件                                                 | Object      | 是   |
| - - Prefix                       | 规则要匹配上的对象键前缀                                     | String      | 否   |
| - Transition                     | 规则转换属性，表示对象存储级别何时转换为 Standard_IA 或 Archive | Object      | 否   |
| - - Days                         | 指明规则对应的动作在对象最后的修改日期过后多少天执行，该字段有效值是非负整数，最大支持3650天 | Number      | 是   |
| - - StorageClass                 | 表示规则对应的动作执行后变更对象的存储级别，枚举值：STANDARD、STANDARD_IA、ARCHIVE，默认值：STANDARD | String      | 是   |
| - NoncurrentVersionTransition    | 指明历史版本对象转换属性                                     | ObjectArray | 否   |
| - - NoncurrentDays               | 指明历史版本对象在该值确定的生效天数后进行转换               | Number      | 是   |
| - - StorageClass                 | 表示规则对应的动作执行后变更对象的存储级别，枚举值：STANDARD、STANDARD_IA、ARCHIVE | String      | 是   |
| - Expiration                     | 规则过期属性                                                 | Object      | 否   |
| - - ExpiredObjectDeleteMarker    | 删除过期对象删除标记，枚举值 true，false，与 Days 不可并存   | Boolean     | 是   |
| - - Days                         | 指明规则对应的动作在对象最后的修改日期过后多少天进行删除操作，与 ExpiredObjectDeleteMarker 不可并存 | Number      | 是   |
| - AbortIncompleteMultipartUpload | 表示删除碎片                                                 | Object      | 否   |
| - - DaysAfterInitiation          | 碎片在该值所确定的生效天数后被删除，按文件上传时间开始算，必须为正整数 | Number      | 是   |

#### 回调函数说明

```
function(err, data) { ... }
```

| 参数名&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;       | 描述                                                     | 类型   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 请求发生错误时返回的对象，包括网络错误和业务错误，如果请求成功则为空，详情请参见 [错误码](https://intl.cloud.tencent.com/document/product/436/7730) 文档 | Object |
| - statusCode | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number |
| - headers    | 请求返回的头部信息                                           | Object |
| data         | 请求成功时返回的对象，如果请求发生错误，则为空               | Object |
| - statusCode | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number |
| - headers    | 请求返回的头部信息                                           | Object |

## 查询生命周期

#### 功能说明

GET Bucket lifecycle 接口可以查询存储桶生命周期管理的配置。

#### 请求示例

[//]: # (.cssg-snippet-get-bucket-lifecycle)
```js
cos.getBucketLifecycle({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 返回示例

```json
{
    "Rules": [{
        "ID": "1",
        "Filter": "",
        "Status": "Enabled",
        "Transition": {
            "Days": "30",
            "StorageClass": "STANDARD_IA"
        }
    }, {
        "ID": "2",
        "Filter": {
            "Prefix": "dir/"
        },
        "Status": "Enabled",
        "Transition": {
            "Days": "90",
            "StorageClass": "ARCHIVE"
        }
    }, {
        "ID": "3",
        "Filter": "",
        "Status": "Enabled",
        "Expiration": {
            "Days": "180"
        }
    }, {
        "ID": "4",
        "Filter": "",
        "Status": "Enabled",
        "AbortIncompleteMultipartUpload": {
            "DaysAfterInitiation": "30"
        }
    }, {
        "ID": "5",
        "Filter": "",
        "Status": "Enabled",
        "NoncurrentVersionTransition:": {
            "NoncurrentDays": "30",
            "StorageClass": "ARCHIVE"
        }
    }],
    "statusCode": 200,
    "headers": {}
}
```

#### 参数说明

| 参数名称 | 描述                                                     | 类型   | 是否必填 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket |   查询生命周期的存储桶，格式：BucketName-APPID               | String | 是   |
| Region | 存储桶所在地域，枚举值请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224) | String | 是   |

#### 回调函数说明

```
function(err, data) { ... }
```

| 参数名&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;                            | 参数描述                                                     | 类型        |
| ---------------------------------- | ------------------------------------------------------------ | ----------- |
| err                                | 请求发生错误时返回的对象，包括网络错误和业务错误，如果请求成功则为空，详情请参见 [错误码](https://intl.cloud.tencent.com/document/product/436/7730) 文档 | Object      |
| - statusCode                       | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number      |
| - headers                          | 请求返回的头部信息                                           | Object      |
| data                               | 请求成功时返回的对象，如果请求发生错误，则为空               | Object      |
| - statusCode                       | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number      |
| - headers                          | 请求返回的头部信息                                           | Object      |
| - Rules                            | 指定生命周期规则列表                                         | ObjectArray |
| - - ID                             | 规则的唯一标识 ID                                            | String      |
| - - Status                         | 规则的开启状态，枚举值：Enabled、Disabled                    | String      |
| - - Filter                         | 指定过滤条件                                                 | Object      |
| - - - Prefix                       | 规则要匹配上的对象键前缀                                     | String      |
| - - Transition                     | 规则转换属性，表示对象存储级别何时转换为 Standard_IA 或 Archive | ObjectArray |
| - - - Days                         | 指明规则对应的动作在对象最后的修改日期过后多少天执行，该字段有效值是非负整数，最大支持3650天 | Number      |
| - - - StorageClass                 | 表示规则对应的动作执行后变更对象的存储类型，枚举值：STANDARD、STANDARD_IA、ARCHIVE | String      |
| - - NoncurrentVersionTransition    | 指明历史版本对象转换属性                                     | ObjectArray |
| - - - NoncurrentDays               | 指明历史版本对象在该值确定的生效天数后进行转换               | Number      |
| - - - StorageClass                 | 表示规则对应的动作执行后变更对象的存储级别，枚举值：STANDARD、STANDARD_IA、ARCHIVE | String      |
| - - Expiration                     | 规则过期属性                                                 | Object      |
| - - - ExpiredObjectDeleteMarker    | 删除过期对象删除标记，枚举值 true，false，与 Days 不可并存   | Boolean     |
| - - - Days                         | 指明规则对应的动作在对象最后的修改日期过后多少天进行删除操作，与 ExpiredObjectDeleteMarker 不可并存 | Number      |
| - - AbortIncompleteMultipartUpload | 表示删除碎片                                                 | Object      |
| - - - DaysAfterInitiation          | 碎片在该值所确定的生效天数后被删除，按文件上传时间开始算，必须为正整数 | Number      |

## 删除生命周期

#### 功能说明

DELETE Bucket lifecycle 接口可以删除存储桶生命周期管理的配置。

#### 请求示例

[//]: # (.cssg-snippet-delete-bucket-lifecycle)
```js
cos.deleteBucketLifecycle({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 参数说明

| 参数名称 | 描述                                                     | 类型   | 是否必填 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 被删除生命周期配置的存储桶，格式：BucketName-APPID           | String | 是   |
| Region | 存储桶所在地域，枚举值请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224) | String | 是   |

#### 回调函数说明

```
function(err, data) { ... }
```

| 参数名称&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;       | 描述                                                     | 类型   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 请求发生错误时返回的对象，包括网络错误和业务错误，如果请求成功则为空，详情请参见 [错误码](https://intl.cloud.tencent.com/document/product/436/7730) 文档 | Object |
| - statusCode | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number |
| - headers    | 请求返回的头部信息                                           | Object |
| data         | 请求成功时返回的对象，如果请求发生错误，则为空               | Object |
| - statusCode | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number |
| - headers    | 请求返回的头部信息                                           | Object |
