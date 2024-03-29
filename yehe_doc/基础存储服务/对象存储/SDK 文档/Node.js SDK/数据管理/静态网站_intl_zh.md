## 简介
本文档提供关于静态网站的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名         | 操作描述                         |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket website](https://intl.cloud.tencent.com/document/product/436/30617) | 设置静态网站 | 为已存在的存储桶设置静态网站配置信息         |
| [GET Bucket website](https://intl.cloud.tencent.com/document/product/436/30616) | 查询静态网站 | 查询指定存储桶的静态网站配置信息 |
| [DELETE Bucket website](https://intl.cloud.tencent.com/document/product/436/30629) | 删除静态网站 | 删除指定存储桶的静态网站配置信息             |


## 设置静态网站

#### 功能说明

为已存在的存储桶配置静态网站。

#### 请求示例

```js
cos.putBucketWebsite({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'ap-beijing',    /* 必须 */
    WebsiteConfiguration: {
        IndexDocument: {
            Suffix: "index.html"
        },
        ErrorDocument: {
            Key: "error.html"
        },
        RedirectAllRequestsTo: {
            Protocol: "https"
        },
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### 参数说明

| 参数名称    | 描述                                                     | 类型        | 是否必填 |
| --------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket    | 设置静态网站的存储桶，格式为 BucketName-APPID，此处填写的存储桶名称必须为此格式 | String      | 是   |
| Region    | 存储桶所在地域，枚举值请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224) | String      | 是   |
| WebsiteConfiguration   | 静态网站配置，包括索引文档、错误文档、协议转换和重定向规则                               | Object      | 是   |
| - IndexDocument    | 索引文档                                                     | Object      | 是   |
| - - Suffix   | 指定索引文档                                                       | String      | 是   |
| - ErrorDocument    | 错误文档                                                     | Object      | 否   |
| - - Key   | 指定通用错误返回                                                       | String      | 否   |
| - RedirectAllRequestsTo    | 重定向所有请求                                                     | Object      | 否   |
| - - Protocol   | 指定全站重定向的协议，只能设置为 https                                                       | String      | 否   |
| - RoutingRules    | 设置重定向规则，最多设置100条                                                      | ObjectArray      | 否   |
| - - Condition   | 指定重定向发生的条件，前缀匹配重定向和错误码重定向只能指定一个                                                       | Object      | 否   |
| - - - HttpErrorCodeReturnedEquals   | 指定重定向错误码，只支持配置4XX返回码，优先级高于ErrorDocument          | String      | 否   |
| - - - KeyPrefixEquals   | 指定前缀重定向的路径，替换指定的 folder/          | String      | 否   |
| - - Redirect   | 指定满足重定向 conditon 时重定向的具体替换规则                                                       | Object      | 否   |
| - - - ReplaceKeyWith   | 替换整个 Key 为指定的内容          | String      | 否   |
| - - - ReplaceKeyPrefixWith   | 替换匹配到的前缀为指定的内容，Conditon 为 KeyPrefixEquals 才可设置          | String      | 否   |

#### 回调函数说明

```
function(err, data) { ... }
```

| 参数名称&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;       | 描述                                                     | 类型   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 请求发生错误时返回的对象，包括网络错误和业务错误，如果请求成功则为空，更多详情请参见 [错误码](https://intl.cloud.tencent.com/document/product/436/7730) 文档 | Object |
| - statusCode | 请求返回的 HTTP 状态码，如200、403、404等                    | Number |
| - headers    | 请求返回的头部信息                                           | Object |
| data         | 请求成功时返回的对象，如果请求发生错误，则为空               | Object |
| - statusCode | 请求返回的 HTTP 状态码，如200、403、404等                    | Number |
| - headers    | 请求返回的头部信息                                           | Object |

## 查询静态网站配置

#### 功能说明

查询与指定存储桶关联的静态网站配置信息。

#### 请求示例

```js
cos.getBucketWebsite({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'ap-beijing',    /* 必须 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 返回示例

```json
{
    "WebsiteConfiguration": {
        "IndexDocument": {
            "Suffix": "index.html"
        },
        "ErrorDocument": {
            "Key": "error.html"
        },
        "RedirectAllRequestsTo": {
            "Protocol": "https"
        },
    },
    "statusCode": 200,
    "headers": {}
}
```

#### 参数说明

| 参数名称 | 描述          | 类型   | 是否必填 |
| ------ | ------------------------ | ------ | ---- |
| Bucket | 查询静态网站配置的存储桶，格式为 BucketName-APPID，此处填写的存储桶名称必须为此格式 | String | 是   |
| Region | 存储桶所在地域，枚举值请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224) | String | 是   |

#### 回调函数说明

```
function(err, data) { ... }
```

|  参数名称  | 描述  | 类型  |
| ------------ | ------------- | ----------- |
| err          | 请求发生错误时返回的对象，包括网络错误和业务错误，如果请求成功则为空，更多详情请参见 [错误码](https://intl.cloud.tencent.com/document/product/436/7730) 文档 | Object      |
| - statusCode | 请求返回的 HTTP 状态码，如200、403、404等                    | Number      |
| - headers    | 请求返回的头部信息                                           | Object      |
| data         | 请求成功时返回的对象，如果请求发生错误，则为空               | Object      |
| - statusCode | 请求返回的 HTTP 状态码，如200、403、404等                    | Number      |
| - headers    | 请求返回的头部信息                                           | Object      |
| - WebsiteConfiguration   | 静态网站配置，包括索引文档、错误文档、协议转换和重定向规则                               | Object      | 
| - - IndexDocument    | 索引文档                                                     | Object      | 
| - - - Suffix   | 指定索引文档                                                       | String      | 
| - - ErrorDocument    | 错误文档                                                     | Object      | 
| - - - Key   | 指定通用错误返回                                                       | String      | 
| - - RedirectAllRequestsTo    | 重定向所有请求                                                     | Object      | 
| - - - Protocol   | 指定全站重定向的协议，只能设置为 https                                                       | String      | 
| - - RoutingRules    | 设置重定向规则，最多设置100条                                                      | ObjectArray      |
| - - - Condition   | 指定重定向发生的条件，前缀匹配重定向和错误码重定向只能指定一个                                                       | Object      | 
| - - - - HttpErrorCodeReturnedEquals   | 指定重定向错误码，只支持配置4XX 返回码，优先级高于ErrorDocument          | String      | 
| - - - - KeyPrefixEquals   | 指定前缀重定向的路径，替换指定的 folder/          | String      | 
| - - - Redirect   | 指定满足重定向 conditon 时重定向的具体替换规则                                                       | Object      | 
| - - - - ReplaceKeyWith   | 替换整个 Key 为指定的内容          | String      | 
| - - - - ReplaceKeyPrefixWith   | 替换匹配到的前缀为指定的内容，Conditon 为 KeyPrefixEquals 才可设置          | String      | 



## 删除静态网站配置

#### 功能说明

删除指定存储桶中的静态网站配置。

#### 请求示例

```js
cos.deleteBucketWebsite({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'ap-beijing',    /* 必须 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 参数说明

| 参数名称 | 描述                                                     | 类型   | 是否必填 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 被删除静态网站配置的存储桶，格式为 BucketName-APPID，此处填写的存储桶名称必须为此格式 | String | 是   |
| Region | 存储桶所在地域，枚举值请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224) | String | 是   |

#### 回调函数说明

```
function(err, data) { ... }
```

| 参数名称&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;       | 描述                                                     | 类型   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 请求发生错误时返回的对象，包括网络错误和业务错误，如果请求成功则为空，更多详情请参见 [错误码](https://intl.cloud.tencent.com/document/product/436/7730) 文档 | Object |
| - statusCode | 请求返回的 HTTP 状态码，如200、403、404等                    | Number |
| - headers    | 请求返回的头部信息                                           | Object |
| data         | 请求成功时返回的对象，如果请求发生错误，则为空               | Object |
| - statusCode | 请求返回的 HTTP 状态码，如200、403、404等                    | Number |
| - headers    | 请求返回的头部信息                                           | Object |
