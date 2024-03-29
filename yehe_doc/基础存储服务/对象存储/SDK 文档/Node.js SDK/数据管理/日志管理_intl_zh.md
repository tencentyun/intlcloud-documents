## 简介


本文档提供关于日志管理的 API 概览以及 SDK 示例代码。


| API            | 操作名       | 操作描述 |
| --------------------------- | ------------ | -------- |
| [PUT Bucket logging](https://intl.cloud.tencent.com/document/product/436/17054) | 设置日志管理 | 为源存储桶开启日志记录 |
| [GET Bucket logging](https://intl.cloud.tencent.com/document/product/436/17053) | 查询日志管理 | 查询源存储桶的日志配置信息 |


## 设置日志管理

#### 功能说明

PUT Bucket Logging 用于为源存储桶开启日志记录，将源存储桶的访问日志保存到指定的目标存储桶中。

>只有源存储桶拥有者才可进行该请求操作。

#### 请求示例

示例1：设置将源存储桶`sourcebucket-1250000000`的日志信息投递到目标存储桶`targetbucket-1250000000`的 `bucket-logging-prefix/`路径下。

```js
cos.putBucketLogging({
    Bucket: 'sourcebucket-1250000000',  /* 必须 */
    Region: 'ap-beijing',               /* 必须 */
    BucketLoggingStatus: {              /* 必须 */
        LoggingEnabled: {
            TargetBucket: 'targetbucket-1250000000',
            TargetPrefix: 'bucket-logging-prefix/'
        }
    }
}, function(err, data) {
    console.log(err || data);
});
```

示例2：关闭目标存储桶`sourcebucket-1250000000`的日志投递。

```js
cos.putBucketLogging({
    Bucket: 'sourcebucket-1250000000',  /* 必须 */
    Region: 'ap-beijing',               /* 必须 */
    BucketLoggingStatus: {}             /* 必须 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 参数说明

| 参数名称              | 描述                                                     | 类型        | 是否必填 |
| ------------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket              | 设置日志管理的存储桶，格式为 BucketName-APPID，此处填写的存储桶名称必须为此格式 | String      | 是   |
| Region              | 存储桶所在地域，枚举值请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224) | String      | 是   |
| BucketLoggingStatus | 说明日志记录配置的状态，如果为空字符串则意为关闭日志记录                            | Object     | 是   |
| - LoggingEnabled             | 存储桶 logging 设置的具体信息，主要是目标存储桶                                           | Object      | 否   |
| - - TargetBucket             | 存放日志的目标存储桶，可以是同一个存储桶（但不推荐），或同一账户下、同一地域的存储桶                                           | String      | 否   |
| - - TargetPrefix             | 日志存放在目标存储桶的指定路径                                           | String      | 否   |

#### 回调函数说明

```
function(err, data) { ... }
```

| 参数名称&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | 描述                                                     | 类型   |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------ |
| err                                                          | 请求发生错误时返回的对象，包括网络错误和业务错误，如果请求成功则为空，更多详情请参见 [错误码](https://intl.cloud.tencent.com/document/product/436/7730) 文档 | Object |
| - statusCode                                                 | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number |
| - headers                                                    | 请求返回的头部信息                                           | Object |
| data                                                         | 请求成功时返回的对象，如果请求发生错误，则为空               | Object |
| - statusCode                                                 | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number |
| - headers                                                    | 请求返回的头部信息                                           | Object |

## 查询日志管理

#### 功能说明

GET Bucket logging 用于查询源存储桶的日志配置信息。

>只有源存储桶拥有者才可进行该请求操作。

#### 请求示例

```js
cos.getBucketLogging({
    Bucket: 'sourcebucket-1250000000',  /* 必须 */
    Region: 'ap-beijing'                /* 必须 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 返回示例

```json
{
    "BucketLoggingStatus": {
        "LoggingEnabled": {
            "TargetBucket": "targetbucket-1250000000",
            "TargetPrefix": "bucket-logging-prefix/"
        }
    },
    "statusCode": 200,
    "headers": {}
}
```

#### 参数说明

| 参数名称 | 描述                                                     | 类型   | 是否必填 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 查询日志管理的存储桶，格式为 BucketName-APPID，此处填写的存储桶名称必须为此格式 | String | 是   |
| Region | 存储桶所在地域，枚举值请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224) | String | 是   |

#### 回调函数说明

```
function(err, data) { ... }
```

| 参数名称&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | 描述                                                     | 类型        |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ----------- |
| err                                                          | 请求发生错误时返回的对象，包括网络错误和业务错误，如果请求成功则为空，更多详情请参见 [错误码](https://intl.cloud.tencent.com/document/product/436/7730) 文档 | Object      |
| - statusCode                                                 | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number      |
| - headers                                                    | 请求返回的头部信息                                           | Object      |
| data                                                         | 请求成功时返回的对象，如果请求发生错误则为空                 | Object      |
| - statusCode                                                 | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number      |
| - headers                                                    | 请求返回的头部信息                                           | Object      |
| - BucketLoggingStatus                                                        | 说明日志记录配置的状态，如果为空字符串则意为关闭日志记录 | Object/String      |
| - - LoggingEnabled                                                  | 存储桶 logging 设置的具体信息，主要是目标存储桶                         | Object      |
| - - - TargetBucket                                                  | 存放日志的目标存储桶，可以是同一个存储桶（但不推荐），或同一账户下、同一地域的存储桶                         | String      |
| - - - TargetPrefix                                                  | 日志存放在目标存储桶的指定路径                         | String      |
