## 简介

本文档提供关于存储桶 Referer 白名单或者黑名单的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名         | 操作描述                 |
| ------------------------------------------------------------ | -------------- | ------------------------ |
| [PUT Bucket referer](https://intl.cloud.tencent.com/document/product/436/31423) | 设置存储桶 Referer | 设置存储桶 Referer 白名单或者黑名单 |
| [GET Bucket referer](https://intl.cloud.tencent.com/document/product/436/30615) | 查询存储桶 Referer | 查询存储桶 Referer 白名单或者黑名单 |

## 设置存储桶 Referer

#### 功能说明

设置指定存储桶的 Referer 白名单或者黑名单（PUT Bucket referer）。

#### 请求示例

[//]: # ".cssg-snippet-put-bucket-referer"
```js
cos.putBucketReferer({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
    RefererConfiguration: {
        Status: 'Enabled',
        RefererType: 'White-List',
        DomainList: {
            Domains: [
                '*.qq.com',
                '*.qcloud.com',
            ]
        },
        EmptyReferConfiguration: 'Allow',
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### 参数说明

| 参数名称&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;        | 描述                                                     | 类型        | 是否必填 |
| ------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket        | 设置存储桶策略的存储桶，格式：BucketName-APPID  | String      | 是   |
| Region        | 存储桶所在地域，枚举值请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224) | String      | 是   |
| RefererConfiguration        | 防盗链配置信息，详情请参见 [PUT Bucket referer](https://intl.cloud.tencent.com/document/product/436/31423) | Object      | 是   |
| - Status     | 是否开启防盗链，枚举值：Enabled、Disabled    | String      | 是   |
| - RefererType   | 防盗链类型，枚举值：Black-List、White-List      | String | 是   |
| - DomainList   | 生效域名列表， 支持多个域名且为前缀匹配， 支持带端口的域名和 IP， 支持通配符\*，做二级域名或多级域名的通配   | Object | 是   |
| - - Domains    | 生效域名，支持两种写法：单条'\*.qq.com'或多条['\*.qq.com', '\*.qcloud.com']                              | String\Array      | 是   |
| -  EmptyReferConfiguration  | 是否允许空 Referer 访问，枚举值：Allow、Deny，默认值为 Deny | String | 否   |

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

## 查询存储桶 Referer

#### 功能说明

查询指定存储桶 Referer 白名单或者黑名单（GET Bucket referer）。

#### 请求示例

[//]: # ".cssg-snippet-get-bucket-referer"
```js
cos.getBucketReferer({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 返回示例

```json
{
    "RefererConfiguration": {
        "Status": "Enabled",
        "RefererType": "White-List",
        "DomainList": {
            "Domains": [
                "*.qq.com",
                "*.qcloud.com"
            ]
        },
        "EmptyReferConfiguration": "Allow"
    },
    "statusCode": 200,
    "headers": {},
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
| - RefererConfiguration        | 防盗链配置信息，详情请参见 [GET Bucket referer](https://intl.cloud.tencent.com/document/product/436/30615) | Object      |
| - - Status     | 是否开启防盗链，枚举值：Enabled、Disabled    | String      |
| - - RefererType   | 防盗链类型，枚举值：Black-List、White-List      | String |
| - - DomainList   | 生效域名列表， 支持多个域名且为前缀匹配， 支持带端口的域名和 IP， 支持通配符*，做二级域名或多级域名的通配   | Object |
| - - - Domains    | 生效域名                            | Array      |
| - - EmptyReferConfiguration  | 是否允许空 Referer 访问，枚举值：Allow、Deny，默认值为 Deny | String |
