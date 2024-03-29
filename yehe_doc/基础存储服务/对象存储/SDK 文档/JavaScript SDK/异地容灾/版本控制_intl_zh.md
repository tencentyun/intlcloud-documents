## 简介

本文档提供关于版本控制的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名       | 操作描述                 |
| ------------------------------------------------------------ | ------------ | ------------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | 设置版本控制 | 设置存储桶的版本控制功能 |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | 查询版本控制 | 查询存储桶的版本控制信息 |

## 设置版本控制

#### 功能说明

PUT Bucket versioning 接口实现启用或者暂停存储桶的版本控制功能。

>
> 1. 如果您从未在存储桶上启用过版本控制，则 GET Bucket versioning 请求不返回版本状态值。
> 2. 开启版本控制功能后，只能暂停，不能关闭。
> 3. 设置版本控制状态值为 Enabled 或者 Suspended，表示开启版本控制和暂停版本控制。
> 4. 设置存储桶的版本控制功能，您需要有存储桶的写权限。

#### 请求示例

[//]: # ".cssg-snippet-put-bucket-versioning"
```js
cos.putBucketVersioning({
    Bucket: 'examplebucket-1250000000',  /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
    VersioningConfiguration: {
        Status: "Enabled"
    }
}, function (err, data) {
    console.log(err || data);
});
```

#### 参数说明

| 参数名称    | 描述                                                     | 类型        | 是否必填 |
| ----------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket                  | 开启或暂停版本控制的存储桶，格式：BucketName-APPID | String | 是   |
| Region                  | 存储桶所在地域，枚举值请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224) | String | 是   |
| VersioningConfiguration | 定义存储桶的版本控制配置信息                                 | Object | 是   |
| - Status                | 版本控制是否打开的状态，枚举值：Enabled、Suspended。<br><li>Enabled 表示打开<br><li>Suspended 表示暂停 | String | 否   |

#### 回调函数说明

```
function(err, data) { ... }
```

| 参数名&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;       | 参数描述                                                     | 类型   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 请求发生错误时返回的对象，包括网络错误和业务错误，如果请求成功则为空，更多详情请参见 [错误码](https://intl.cloud.tencent.com/document/product/436/7730) 文档 | Object |
| - statusCode | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number |
| - headers    | 请求返回的头部信息                                           | Object |
| data         | 请求成功时返回的对象，如果请求发生错误，则为空               | Object |
| - statusCode | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number |
| - headers    | 请求返回的头部信息                                           | Object |

## 查询版本控制

#### 功能说明

查询存储桶的版本控制信息。

#### 请求示例

[//]: # ".cssg-snippet-get-bucket-versioning"
```js
cos.getBucketVersioning({
    Bucket: 'examplebucket-1250000000',  /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
}, function (err, data) {
    console.log(err || data);
});
```

#### 参数说明

| 参数名称    | 描述                                                     | 类型        | 是否必填 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 查询版本控制的存储桶，格式：BucketName-APPID | String | 是   |
| Region | 存储桶所在地域，枚举值请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224) | String | 是   |

#### 回调函数说明

```
function(err, data) { ... }
```

| 参数名&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;                    | 参数描述                                                     | 类型   |
| ------------------------- | ------------------------------------------------------------ | ------ |
| err                       | 请求发生错误时返回的对象，包括网络错误和业务错误，如果请求成功则为空，更多详情请参见 [错误码](https://intl.cloud.tencent.com/document/product/436/7730) 文档 | Object |
| - statusCode              | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number |
| - headers                 | 请求返回的头部信息                                           | Object |
| data                      | 请求成功时返回的对象，如果请求发生错误，则为空               | Object |
| - statusCode              | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number |
| - headers                 | 请求返回的头部信息                                           | Object |
| - VersioningConfiguration | 存储桶的版本控制配置信息，若从未开启过，则为空对象 '{}'      | Object |
| - - Status                | 版本控制是否打开的状态，枚举值：Enabled、Suspended           | String |
