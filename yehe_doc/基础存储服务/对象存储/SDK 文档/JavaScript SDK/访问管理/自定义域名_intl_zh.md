## 简介

本文档提供关于自定义域名的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名         | 操作描述                         |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| PUT Bucket domain | 设置自定义域名   | 设置存储桶的自定义域名信息 |
| GET Bucket domain | 查询自定义域名 | 查询存储桶的自定义域名信息 |
| DELETE Bucket domain | 删除自定义域名 | 删除存储桶的自定义域名信息 |


## 设置自定义域名

#### 功能说明

为已存在的存储桶绑定自定义域名。

#### 请求示例

```js
cos.putBucketDomain({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'ap-beijing',    /* 必须 */
    DomainRule: [{
        Status: "DISABLED",
        Name: "www.example.com",
        Type: "REST"
    },
    {
        Status: "DISABLED",
        Name: "www.example.net",
        Type: "WEBSITE",
    }]
}, function(err, data) {
    console.log(err || data);
});
```

#### 参数说明

| 参数名称&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    | 描述                                                     | 类型        | 是否必填 |
| --------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket    | 设置自定义域名的存储桶，格式为 BucketName-APPID，此处填写的存储桶名称必须为此格式 | String      | 是   |
| Region    | 存储桶所在地域，枚举值请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224) | String      | 是   |
| DomainRule   | 自定义域名配置                                                                             | Object      | 是   |
| - Status  | 域名上线/下线状态，枚举值： ENABLED、DISABLED                                                  | String      | 是   |
| - Name    | 用户的自定义域名                                                                               | String      | 是   |
| - Type    | 绑定的源站类型，枚举值：REST、WEBSITE                                                             | String      | 是   |
| - ForcedReplacement | 替换已存在的配置，枚举值：CNAME、TXT。填写则强制校验域名所有权后，再下发配置。                        | String      | 否   |

#### 回调函数说明

```
function(err, data) { ... }
```

| 参数名称&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;       | 描述                                                     | 类型   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 请求发生错误时返回的对象，包括网络错误和业务错误，如果请求成功则为空，更多详情请参见 [错误码](https://intl.cloud.tencent.com/document/product/436/7730) 文档 | Object |
| - statusCode | 请求返回的 HTTP 状态码，如200、403、404等                    | Number |
| - headers    | 请求返回的头部信息                                           | Object |
| data         | 请求成功时返回的对象，如果请求发生错误，则为空               | Object |
| - statusCode | 请求返回的 HTTP 状态码，如200、403、404等                    | Number |
| - headers    | 请求返回的头部信息                                           | Object |

## 查询自定义域名

#### 功能说明

查询与指定存储桶关联的自定义域名信息。

#### 请求示例

```js
cos.getBucketDomain({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'ap-beijing',    /* 必须 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 返回示例

```json
{
    "DomainRule": [{
        "Status": "DISABLED",
        "Name": "www.example.com",
        "Type": "REST"
    }, {
        "Status": "DISABLED",
        "Name": "www.example.net",
        "Type": "WEBSITE"
    }],
    "statusCode": 200,
    "headers": {}
}
```

#### 参数说明

| 参数名称 | 描述                                                     | 类型   | 是否必填 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 查询自定义域名的存储桶，格式为 BucketName-APPID，此处填写的存储桶名称必须为此格式 | String | 是   |
| Region | 存储桶所在地域，枚举值请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224) | String | 是   |

#### 回调函数说明

```
function(err, data) { ... }
```

| 参数名称&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;       | 描述                                                     | 类型        |
| ------------ | ------------------------------------------------------------ | ----------- |
| err          | 请求发生错误时返回的对象，包括网络错误和业务错误，如果请求成功则为空，更多详情请参见 [错误码](https://intl.cloud.tencent.com/document/product/436/7730) 文档 | Object      |
| - statusCode | 请求返回的 HTTP 状态码，如200、403、404等                    | Number      |
| - headers    | 请求返回的头部信息                                           | Object      |
| data         | 请求成功时返回的对象，如果请求发生错误，则为空               | Object      |
| - statusCode | 请求返回的 HTTP 状态码，如200、403、404等                    | Number      |
| - headers    | 请求返回的头部信息                                           | Object      |
| - DomainRule   | 自定义域名配置                                                                             | Object      | 
| - - Status  | 域名上线/下线状态，枚举值： ENABLED、DISABLED                                                  | String      | 
| - - Name    | 用户的自定义域名                                                                               | String      | 
| - - Type    | 绑定的源站类型，枚举值：REST、WEBSITE                                                             | String      | 
| - - ForcedReplacement | 替换已存在的配置，枚举值：CNAME、TXT。填写则强制校验域名所有权后，再下发配置。                        | String      | 

## 删除自定义域名

#### 功能说明

删除指定存储桶中的自定义域名配置。

#### 请求示例

```js
cos.deleteBucketDomain({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'ap-beijing',    /* 必须 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 参数说明

| 参数名称 | 描述                                                     | 类型   | 是否必填 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 被删除自定义域名的存储桶，格式为 BucketName-APPID，此处填写的存储桶名称必须为此格式 | String | 是   |
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
