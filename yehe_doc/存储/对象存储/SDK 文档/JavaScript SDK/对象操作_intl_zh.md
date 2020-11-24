## 简介

本文档提供关于对象的简单操作、分块操作以及其他操作相关的 API 概览以及 SDK 示例代码，并举例如何使用。

**简单操作**

| API                                                          | 操作名         | 操作描述                                 |
| ------------------------------------------------------------ | -------------- | ---------------------------------------- |
| [GET Bucket（List Objects）](https://intl.cloud.tencent.com/document/product/436/30614) | 查询对象列表   | 查询存储桶下的部分或者全部对象           |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | 简单上传对象   | 上传一个对象至存储桶                     |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | 表单上传对象   | 使用表单请求上传对象                     |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | 查询对象元数据 | 查询对象的元数据信息                     |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | 下载对象       | 下载一个对象至本地                       |
| [OPTIONS Object](https://intl.cloud.tencent.com/document/product/436/8288) | 预请求跨域配置 | 用预请求来确认是否可以发送真正的跨域请求 |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | 设置对象复制   | 复制对象到目标路径                       |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | 删除单个对象   | 在存储桶中删除指定对象                   |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | 删除多个对象   | 在存储桶中批量删除对象                   |

**分块操作**

| API                                                          | 操作名         | 操作描述                             |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | 查询分块上传   | 查询正在进行中的分块上传信息         |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | 初始化分块上传 | 初始化分块上传任务                   |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | 上传分块       | 分块上传对象                         |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | 复制分块       | 将其他对象复制为一个分块             |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | 查询已上传块   | 查询特定分块上传操作中已上传的块     |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | 完成分块上传   | 完成整个对象的分块上传               |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | 终止分块上传   | 终止一个分块上传操作并删除已上传的块 |

**其他操作**

| API                                                          | 操作名       | 操作描述                           |
| ------------------------------------------------------------ | ------------ | ---------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | 恢复归档对象 | 将归档类型的对象取回访问           |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | 设置对象 ACL | 设置存储桶中某个对象的访问控制列表 |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | 查询对象 ACL | 查询对象的访问控制列表             |

## 简单操作

### 查询对象列表

#### 功能说明

查询存储桶下的部分或者全部对象。

#### 使用示例

示例一：列出目录 a 的所有文件。

[//]: # ".cssg-snippet-get-bucket"
```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
    Prefix: 'a/',           /* 非必须 */
}, function(err, data) {
    console.log(err || data.Contents);
});
```

返回值格式：

```json
{
    "Name": "examplebucket-1250000000",
    "Prefix": "",
    "Marker": "a/",
    "MaxKeys": "1000",
    "Delimiter": "",
    "IsTruncated": "false",
    "Contents": [{
        "Key": "a/3mb.zip",
        "LastModified": "2018-10-18T07:08:03.000Z",
        "ETag": "\"05a9a30179f3db7b63136f30aa6aacae-3\"",
        "Size": "3145728",
        "Owner": {
            "ID": "1250000000",
            "DisplayName": "1250000000"
        },
        "StorageClass": "STANDARD"
    }],
    "statusCode": 200,
    "headers": {}
}
```

示例二：列出目录 a 的文件，不深度遍历。

[//]: # ".cssg-snippet-get-bucket-with-delimiter"
```js
cos.getBucket({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
    Prefix: 'a/',              /* 非必须 */
    Delimiter: '/',            /* 非必须 */
}, function(err, data) {
    console.log(err || data.CommonPrefixes);
});
```

返回值格式：

```json
{
    "Name": "examplebucket-1250000000",
    "Prefix": "a/",
    "Marker": "",
    "MaxKeys": "1000",
    "Delimiter": "/",
    "IsTruncated": "false",
    "CommonPrefixes": [{
        "Prefix": "a/1/"
    }],
    "Contents": [{
        "Key": "a/3mb.zip",
        "LastModified": "2018-10-18T07:08:03.000Z",
        "ETag": "\"05a9a30179f3db7b63136f30aa6aacae-3\"",
        "Size": "3145728",
        "Owner": {
            "ID": "1250000000",
            "DisplayName": "1250000000"
        },
        "StorageClass": "STANDARD"
    }],
    "statusCode": 200,
    "headers": {}
}
```

#### 参数说明

| 参数名       | 参数描述                                                     | 类型   | 是否必填 |
| ------------ | ------------------------------------------------------------ | ------ | -------- |
| Bucket       | 存储桶的名称，命名规则为 BucketName-APPID，此处填写的存储桶名称必须为此格式 | String | 是       |
| Region       | 存储桶所在地域，枚举值请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224) | String | 是       |
| Prefix       | 对象键前缀匹配，限定返回中只包含指定前缀的对象键             | String | 否       |
| Delimiter    | 定界符。为一个分隔符号，用于对对象键进行分组。一般是传`/`。所有对象键从 Prefix 或从头（如未指定 Prefix）到首个 delimiter 之间相同部分的路径归为一类，定义为 Common Prefix，然后列出所有 Common Prefix | String | 否       |
| Marker       | 起始对象键标记。列出从 Marker 开始 MaxKeys 条目，默认顺序为 UTF-8 字典序 | String | 否       |
| MaxKeys      | 单次返回最大的条目数量，默认1000，最大为1000                 | String | 否       |
| EncodingType | 规定返回值的编码方式，可选值：url，代表返回的对象键为 URL 编码（百分号编码）后的值，例如“腾讯云”将被编码为`%E8%85%BE%E8%AE%AF%E4%BA%91` | String | 否       |

#### 回调函数说明

```
function(err, data) { ... }
```

| 参数名            | 参数描述                                                     | 类型        |
| ----------------- | ------------------------------------------------------------ | ----------- |
| err               | 请求发生错误时返回的对象，包括网络错误和业务错误，如果请求成功则为空，更多详情请参见 [错误码](https://intl.cloud.tencent.com/document/product/436/7730) 文档 | Object      |
| - statusCode      | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number      |
| - headers         | 请求返回的头部信息                                           | Object      |
| data              | 请求成功时返回的对象，如果请求发生错误，则为空               | Object      |
| - headers         | 请求返回的头部信息                                           | Object      |
| - statusCode      | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number      |
| - Name            | 存储桶的名称，格式为 BucketName-APPID，例如 examplebucket-1250000000 | String      |
| - Prefix          | 对象键前缀匹配，从该标记之后（不含）按照 UTF-8 字典序返回对象键条目 | String      |
| - Marker          | 默认以 UTF-8 二进制顺序列出条目，所有列出条目从 Marker 开始  | String      |
| - MaxKeys         | 单次响应请求内返回结果的最大的条目数量                       | String      |
| - Delimiter       | 定界符                                                       | String      |
| - IsTruncated     | 响应请求条目是否被截断，值为 'true' 或者 'false'             | String      |
| - NextMarker      | 假如返回条目被截断，则返回 NextMarker 表示下一个条目的起点   | String      |
| - CommonPrefixes  | 将 Prefix 到 delimiter 之间的相同路径归为一类，定义为 Common Prefix | ObjectArray |
| - - Prefix        | 单条 Common Prefix 的前缀                                    | String      |
| - EncodingType    | 返回值的编码方式，作用于 Delimiter，Marker，Prefix，NextMarker，Key | String      |
| - Contents        | 对象元数据信息列表                                           | ObjectArray |
| - - Key           | 对象键，即对象的名称                                         | String      |
| - - ETag          | 根据对象内容计算出的 MD5 算法校验值，<br>例如`"22ca88419e2ed4721c23807c678adbe4c08a7880"`，**注意前后携带双引号** | String      |
| - - Size          | 对象大小，单位 Byte                                          | String      |
| - - LastModified  | 对象最后修改时间，为 ISO8601 格式，例如2019-05-24T10:56:40Z  | String      |
| - - Owner         | 对象持有者信息                                               | Object      |
| - - - ID          | 对象持有者的完整 ID，格式为`qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`，<br>例如 `qcs::cam::uin/100000000001:uin/100000000001`，其中100000000001为 uin | String      |
| - - - DisplayName | 对象持有者的名称                                             | String      |
| - - StorageClass  | 对象存储级别，枚举值为：STANDARD、STANDARD_IA、ARCHIVE，详情参见 [存储类型](https://intl.cloud.tencent.com/document/product/436/30925) 文档 | String      |

### 简单上传对象

#### 功能说明

PUT Object 接口可以上传一个对象至指定存储桶中。该操作需要请求者对存储桶有 WRITE 权限。

> !
> 1. Key（文件名）不能以`/`结尾，否则会被识别为文件夹。
> 2. 每个主账号（即同一个 APPID），存储桶的 ACL 规则数量最多为1000条，对象 ACL 规则数量不限制。如果您不需要进行对象 ACL 控制，请在上传时不要设置，默认继承存储桶权限。
> 3. 上传之后，您可以用同样的 Key 生成预签名链接（下载请指定 method 为 GET，具体接口说明见下文，分享到其他端来进行下载。但注意如果您的文件是私有读权限，那么预签名链接只有一定的有效期。

#### 使用示例

简单上传文件，适用于小文件上传。

[//]: # ".cssg-snippet-put-object"
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
    Key: 'exampleobject',              /* 必须 */
    StorageClass: 'STANDARD',
    Body: fileObject, // 上传文件对象
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    console.log(err || data);
});
```

上传字符串作为文件内容：

[//]: # ".cssg-snippet-put-object-string"
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
    Key: 'exampleobject',              /* 必须 */
    Body: 'hello!',
}, function(err, data) {
    console.log(err || data);
});
```

创建目录：

[//]: # ".cssg-snippet-put-object-folder"
```js
cos.putObject({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
    Key: 'a/',              /* 必须 */
    Body: '',
}, function(err, data) {
    console.log(err || data);
});
```

#### 参数说明

| 参数名                 | 参数描述                                                     | 类型             | 是否必填 |
| ---------------------- | ------------------------------------------------------------ | ---------------- | -------- |
| Bucket                 | 存储桶的名称，命名格式为 BucketName-APPID，此处填写的存储桶名称必须为此格式 | String           | 是       |
| Region                 | 存储桶所在地域，枚举值请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224) | String           | 是       |
| Key                    | 对象键（Object 的名称），对象在存储桶中的唯一标识，详情请参见 [对象概述](https://intl.cloud.tencent.com/document/product/436/13324) | String           | 是       |
| Body                   | 上传文件的内容，可以为字符串，File 对象或者 Blob 对象        | String\File\Blob | 是       |
| CacheControl           | RFC 2616中定义的缓存策略，将作为对象的元数据保存             | String           | 否       |
| ContentDisposition     | RFC 2616中定义的文件名称，将作为对象的元数据保存             | String           | 否       |
| ContentEncoding        | RFC 2616中定义的编码格式，将作为对象的元数据保存             | String           | 否       |
| ContentLength          | RFC 2616中定义的 HTTP 请求内容长度（字节）                   | String           | 否       |
| ContentType            | RFC 2616中定义的内容类型（MIME），将作为对象的元数据保存     | String           | 否       |
| Expires                | RFC 2616中定义的过期时间，将作为对象的元数据保存             | String           | 否       |
| Expect                 | 当使用 Expect: 100-continue 时，在收到服务端确认后，才会发送请求内容 | String           | 否       |
| ACL                    | 定义对象的访问控制列表（ACL）属性，枚举值请参见 [ACL 概述](https://intl.cloud.tencent.com/document/product/436/30583) 文档中对象的预设 ACL 部分，例如 default，private，public-read 等 <br>**注意：如果您不需要进行对象 ACL 控制，请设置为 default 或者此项不进行设置，默认继承存储桶权限** | String           | 否       |
| GrantRead              | 赋予被授权者读取对象的权限，格式：id="[OwnerUin]"，可使用半角逗号（,）分隔多组被授权者：<br><li>当需要给子账户授权时，`id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>当需要给主账号授权时，`id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>例如`'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String           | 否       |
| GrantReadAcp           | 赋予被授权者读取对象的访问控制列表（ACL）的权限，格式：id="[OwnerUin]"，可使用半角逗号（,）分隔多组被授权者：<br><li>当需要给子账户授权时，`id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>当需要给主账号授权时，`id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>例如`'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String           | 否       |
| GrantWriteAcp          | 赋予被授权者写入对象的访问控制列表（ACL）的权限，格式：id="[OwnerUin]"，可使用半角逗号（,）分隔多组被授权者：<br><li>当需要给子账户授权时，`id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>当需要给主账号授权时，`id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>例如`'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String           | 否       |
| GrantFullControl       | 赋予被授权者操作对象的所有权限，格式：id="[OwnerUin]"，可使用半角逗号（,）分隔多组被授权者：<br><li>当需要给子账户授权时，`id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>当需要给主账号授权时，`id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>例如`'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String           | 否       |
| StorageClass           | 设置对象的存储级别，枚举值：STANDARD、STANDARD_IA、ARCHIVE，默认值：STANDARD | String           | 否       |
| x-cos-meta-*           | 允许用户自定义的头部信息，将作为对象的元数据保存。大小限制2KB | String           | 否       |
| UploadAddMetaMd5       | 当上传时，给对象的元数据信息增加 x-cos-meta-md5 赋值为对象内容的 MD5 值，格式为32位小写字符串。例如`4d00d79b6733c9cc066584a02ed03410` | String           | 否       |
| onTaskReady            | 上传任务创建时的回调函数，返回一个 taskId，唯一标识上传任务，可用于上传任务的取消（cancelTask），停止（pauseTask）和重新开始（restartTask） | Function         | 否       |
| - taskId               | 上传任务的编号                                               | String           | 否       |
| onProgress             | 进度的回调函数，进度回调响应对象（progressData）属性如下     | Function         | 否       |
| - progressData.loaded  | 已经上传的文件部分大小，以字节（Bytes）为单位                | Number           | 否       |
| - progressData.total   | 整个文件的大小，以字节（Bytes）为单位                        | Number           | 否       |
| - progressData.speed   | 文件的上传速度，以字节/秒（Bytes/s）为单位                   | Number           | 否       |
| - progressData.percent | 文件上传的百分比，以小数形式呈现，例如，上传50%即为0.5       | Number           | 否       |

#### 回调函数说明

```
function(err, data) { ... }
```

| 参数名       | 参数描述                                                     | 类型   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 请求发生错误时返回的对象，包括网络错误和业务错误。如果请求成功则为空，更多详情请参见 [错误码](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number |
| - headers    | 请求返回的头部信息                                           | Object |
| data         | 请求成功时返回的对象，如果请求发生错误，则为空               | Object |
| - statusCode | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number |
| - headers    | 请求返回的头部信息                                           | Object |
| - ETag       | 返回文件的 MD5 算法校验值。ETag 的值可以用于检查对象在上传过程中是否有损坏<br>例如`"09cba091df696af91549de27b8e7d0f6"`，**注意：这里的 ETag 值字符串前后带有双引号** | String |
| - Location   | 上传完的文件访问地址                                         | String |
| - VersionId  | 在开启过版本控制的存储桶中上传对象返回对象的版本 ID，存储桶从未开启则不返回该参数 | String |

### 表单上传对象

JS SDK 未提供 POST Object 接口对应的方法，如果需要使用该接口，请参见 [Web 端直传实践](https://intl.cloud.tencent.com/document/product/436/9067) 里的“方案 B：使用 Form 表单上传”。

### 查询对象元数据

#### 功能说明

查询对象的元数据信息。

#### 使用示例

[//]: # ".cssg-snippet-head-object"
```js
cos.headObject({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
    Key: 'exampleobject',               /* 必须 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 参数说明

| 参数名          | 参数描述                                                     | 类型   | 是否必填 |
| --------------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket          | 存储桶的名称，命名格式为 BucketName-APPID，此处填写的存储桶名称必须为此格式 | String | 是       |
| Region          | 存储桶所在地域，枚举值请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224) | String | 是       |
| Key             | 对象键（Object 的名称），对象在存储桶中的唯一标识，详情请参见 [对象概述](https://intl.cloud.tencent.com/document/product/436/13324) | String | 是       |
| IfModifiedSince | 当对象在指定时间后被修改，返回对应对象的元数据信息，否则返回304 | String | 否       |

#### 回调函数说明

```
function(err, data) { ... }
```

| 参数名                | 参数描述                                                     | 类型    |
| --------------------- | ------------------------------------------------------------ | ------- |
| err                   | 请求发生错误时返回的对象，包括网络错误和业务错误。如果请求成功则为空，更多详情请参见 [错误码](https://intl.cloud.tencent.com/document/product/436/7730) | Object  |
| - statusCode          | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number  |
| - headers             | 请求返回的头部信息                                           | Object  |
| data                  | 请求成功时返回的对象，如果请求发生错误，则为空               | Object  |
| - statusCode          | 请求返回的 HTTP 状态码，例如200，304等，如果在指定时间后未被修改，则返回304 | Number  |
| - headers             | 请求返回的头部信息                                           | Object  |
| - x-cos-object-type   | 用来表示对象是否可以被追加上传，枚举值：normal、appendable，默认 normal 不显示在返回中 | String  |
| - x-cos-storage-class | 对象的存储级别，枚举值：STANDARD、STANDARD_IA、ARCHIVE，默认值：STANDARD 不显示在返回中 | String  |
| - x-cos-meta-*        | 用户自定义的 meta                                            | String  |
| - NotModified         | 对象是否在指定时间后未被修改                                 | Boolean |
| - ETag                | 返回文件的 MD5 算法校验值。ETag 的值可以用于检查对象在上传过程中是否有损坏<br>例如`"09cba091df696af91549de27b8e7d0f6"`，**注意：这里的 ETag 值字符串前后带有双引号** | String  |
| - VersionId           | 在开启过版本控制的存储桶中上传对象返回对象的版本 ID，存储桶从未开启则不返回该参数 | String  |

### 下载对象

> !该接口用于读取对象内容，如果需要发起浏览器下载文件，可以通过 cos.getObjectUrl 获取 url 再触发浏览器下载，具体参见 [预签名 URL](https://intl.cloud.tencent.com/document/product/436/31540) 文档。

#### 功能说明

GET Object 接口请求可以获取存储桶里指定文件的内容，得到文件内容是字符串格式。

#### 使用示例

[//]: # ".cssg-snippet-get-object"
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
    Key: 'exampleobject',              /* 必须 */
}, function(err, data) {
    console.log(err || data.Body);
});
```

指定 Range 获取文件内容：

[//]: # ".cssg-snippet-get-object-range"
```js
cos.getObject({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
    Key: 'exampleobject',              /* 必须 */
    Range: 'bytes=1-3',        /* 非必须 */
}, function(err, data) {
    console.log(err || data.Body);
});
```

#### 参数说明

| 参数名                     | 参数描述                                                     | 类型     | 是否必填 |
| -------------------------- | ------------------------------------------------------------ | -------- | -------- |
| Bucket                     | 存储桶的名称，命名格式为 BucketName-APPID，此处填写的存储桶名称必须为此格式 | String   | 是       |
| Region                     | 存储桶所在地域，枚举值请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224) | String   | 是       |
| Key                        | 对象键（Object 的名称），对象在存储桶中的唯一标识，详情请参见 [对象概述](https://intl.cloud.tencent.com/document/product/436/13324) | String   | 是       |
| ResponseContentType        | 设置响应头部中的 Content-Type 参数                           | String   | 否       |
| ResponseContentLanguage    | 设置返回头部中的 Content-Language 参数                       | String   | 否       |
| ResponseExpires            | 设置返回头部中的 Content-Expires 参数                        | String   | 否       |
| ResponseCacheControl       | 设置返回头部中的 Cache-Control 参数                          | String   | 否       |
| ResponseContentDisposition | 设置返回头部中的 Content-Disposition 参数                    | String   | 否       |
| ResponseContentEncoding    | 设置返回头部中的 Content-Encoding 参数                       | String   | 否       |
| Range                      | RFC 2616 中定义的字节范围，范围值必须使用 bytes=first-last 格式，first 和 last 都是基于0开始的偏移量。例如 bytes=0-9 表示下载对象的开头10个字节的数据 ，如果不指定，则表示下载整个对象 | String   | 否       |
| IfModifiedSince            | 当对象在指定时间后被修改，则返回对象，否则返回304（Not Modified） | String   | 否       |
| IfUnmodifiedSince          | 当对象在指定时间后未被修改，则返回对象，否则返回412（precondition failed） | String   | 否       |
| IfMatch                    | 当对象的 ETag 与指定的值一致，则返回对象，否则返回412（precondition failed） | String   | 否       |
| IfNoneMatch                | 当对象的 ETag 与指定的值不一致，则返回对象，否则返回304（not modified） | String   | 否       |
| VersionId                  | 指定要下载的对象的版本 ID                                    | String   | 否       |
| onProgress                 | 进度的回调函数，进度回调响应对象（progressData）属性如下     | Function | 否       |
| - progressData.loaded      | 已经下载的对象部分大小，以字节（Bytes）为单位                | Number   | 否       |
| - progressData.total       | 整个对象的大小，以字节（Bytes）为单位                        | Number   | 否       |
| - progressData.speed       | 对象的下载速度，以字节/秒（Bytes/s）为单位                   | Number   | 否       |
| - progressData.percent     | 对象下载的百分比，以小数形式呈现，例如，下载50%即为0.5       | Number   | 否       |

#### 回调函数说明

```
function(err, data) { ... }

```

| 参数名&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | 参数描述                                                     | 类型    |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------- |
| err                                                          | 请求发生错误时返回的对象，包括网络错误和业务错误。如果请求成功则为空，更多详情请参见 [错误码](https://intl.cloud.tencent.com/document/product/436/7730) | Object  |
| - statusCode                                                 | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number  |
| - headers                                                    | 请求返回的头部信息                                           | Object  |
| data                                                         | 请求成功时返回的对象，如果请求发生错误，则为空               | Object  |
| - statusCode                                                 | 请求返回的 HTTP 状态码，例如200，304，403，404等             | Number  |
| - headers                                                    | 请求返回的头部信息                                           | Object  |
| - CacheControl                                               | RFC 2616 中定义的缓存指令，仅当对象元数据包含此项或通过请求参数指定了此项时才会返回该头部 | String  |
| - ContentDisposition                                         | RFC 2616 中定义的文件名称，仅当对象元数据包含此项或通过请求参数指定了此项时才会返回该头部 | String  |
| - ContentEncoding                                            | RFC 2616 中定义的编码格式，仅当对象元数据包含此项或通过请求参数指定了此项时才会返回该头部 | String  |
| - Expires                                                    | RFC 2616 中定义的缓存失效时间，仅当对象元数据包含此项或通过请求参数指定了此项时才会返回该头部 | String  |
| - x-cos-storage-class                                        | 对象的存储级别，枚举值：STANDARD、STANDARD_IA、ARCHIVE，<br>**注意：如果没有返回该头部，则说明文件存储级别为 STANDARD （标准存储）** | String  |
| - x-cos-meta-*                                               | 用户自定义的元数据                                           | String  |
| - NotModified                                                | 如果请求时带有 IfModifiedSince 则返回该属性，如果文件未被修改，则为 true，否则为 false | Boolean |
| - ETag                                                       | 返回文件的 MD5 算法校验值。ETag 的值可以用于检查对象在上传过程中是否有损坏<br>例如`"09cba091df696af91549de27b8e7d0f6"`，**注意：这里的 ETag 值字符串前后带有双引号** | String  |
| - VersionId                                                  | 在开启过版本控制的存储桶中上传对象返回对象的版本 ID，存储桶从未开启则不返回该参数 | String  |
| - Body                                                       | 返回的文件内容，默认为 String 形式                           | String  |

### 预请求跨域配置

#### 功能说明

OPTIONS Object 接口实现对对象进行跨域访问配置的预请求。即在发送跨域请求之前会发送一个 OPTIONS 请求并带上特定的来源域，HTTP 方法和 HEADER 信息等给 COS，以决定是否可以发送真正的跨域请求。当 CORS 配置不存在时，请求返回403 Forbidden。**用户可以通过 PUT Bucket cors 接口来开启存储桶的 CORS 支持。**

#### 使用示例

[//]: # ".cssg-snippet-option-object"
```js
cos.optionsObject({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
    Key: 'exampleobject',              /* 必须 */
    Origin: 'https://www.qq.com',      /* 必须 */
    AccessControlRequestMethod: 'PUT', /* 必须 */
    AccessControlRequestHeaders: 'origin,accept,content-type' /* 非必须 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 参数说明

| 参数名                      | 参数描述                                                     | 类型   | 是否必填 |
| --------------------------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket                      | 存储桶的名称，命名格式为 BucketName-APPID，此处填写的存储桶名称必须为此格式 | String | 是       |
| Region                      | 存储桶所在地域，枚举值请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224) | String | 是       |
| Key                         | 对象键（Object 的名称），对象在存储桶中的唯一标识，详情请参见 [对象概述](https://intl.cloud.tencent.com/document/product/436/13324) | String | 是       |
| Origin                      | 模拟跨域访问的请求来源域名                                   | String | 是       |
| AccessControlRequestMethod  | 模拟跨域访问的请求 HTTP 方法                                 | String | 是       |
| AccessControlRequestHeaders | 模拟跨域访问的请求头部                                       | String | 否       |

#### 回调函数说明

```
function(err, data) { ... }
```

| 参数名&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | 参数描述                                                     | 类型    |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------- |
| err                                                          | 请求发生错误时返回的对象，包括网络错误和业务错误。如果请求成功则为空，更多详情请参见 [错误码](https://intl.cloud.tencent.com/document/product/436/7730) | Object  |
| - statusCode                                                 | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number  |
| - headers                                                    | 请求返回的头部信息                                           | Object  |
| data                                                         | 请求成功时返回的对象，如果请求发生错误，则为空               | Object  |
| - headers                                                    | 请求返回的头部信息                                           | Object  |
| - statusCode                                                 | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number  |
| - AccessControlAllowOrigin                                   | 模拟跨域访问的请求来源域名，中间用逗号间隔，当来源不允许的时候，此 Header 不返回，例如`*` | String  |
| - AccessControlAllowMethods                                  | 模拟跨域访问的请求 HTTP 方法，中间用逗号间隔，当请求方法不允许的时候，此 Header 不返回，例如 PUT，GET，POST，DELETE，HEAD | String  |
| - AccessControlAllowHeaders                                  | 模拟跨域访问的请求头部，中间用逗号间隔，当模拟任何请求头部不允许的时候，此 Header 不返回该请求头部。例如：accept，content-type，origin，authorization | String  |
| - AccessControlExposeHeaders                                 | 跨域支持返回头部，中间用逗号间隔。例如：ETag                 | String  |
| - AccessControlMaxAge                                        | 设置 OPTIONS 请求得到结果的有效期。例如：3600                | String  |
| - OptionsForbidden                                           | OPTIONS 请求是否被禁止，如果返回的 HTTP 状态码为403，则为 true | Boolean |

### 设置对象复制

#### 功能说明

PUT Object - Copy 请求创建一个已存在 COS 的对象的副本，即将一个对象从源路径（对象键）复制到目标路径（对象键）。在复制的过程中，对象元数据和访问控制列表（ACL）可以被修改。
用户可以通过该接口创建副本、修改对象元属性（源对象和目标文件的属性相同）、移动或重命名对象（先复制，再单独调用删除接口）。

> !建议对象大小1MB - 5GB，超过5GB的对象请使用高级接口复制对象 [Slice Copy File](#.E5.A4.8D.E5.88.B6.E5.AF.B9.E8.B1.A12)。

#### 使用示例

[//]: # ".cssg-snippet-copy-object"
```js
cos.putObjectCopy({
    Bucket: 'examplebucket-1250000000',                               /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
    Key: 'exampleobject',                                            /* 必须 */
    CopySource: 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject', /* 必须 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 参数说明

| 参数名                      | 参数描述                                                     | 类型   | 是否必填 |
| --------------------------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket                      | 存储桶的名称，命名格式为 BucketName-APPID，此处填写的存储桶名称必须为此格式 | String | 是       |
| Region                      | 存储桶所在地域，枚举值请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224) | String | 是       |
| Key                         | 对象键（Object 的名称），对象在存储桶中的唯一标识，详情请参见 [[对象概述](https://intl.cloud.tencent.com/document/product/436/13324)](https://intl.cloud.tencent.com/document/product/436/13324) | String | 是       |
| CopySource                  | 源对象 URL 路径，可以通过 URL 参数 ?versionId=&lt;versionId> 参数指定指定历史版本 | String | 是       |
| ACL                         | 定义对象的访问控制列表（ACL）属性，枚举值请参见 [ACL 概述](https://intl.cloud.tencent.com/document/product/436/30583) 文档中对象的预设 ACL 部分，例如 default，private，public-read 等 <br>**注意：如果您不需要进行对象 ACL 控制，请设置为 default 或者此项不进行设置，默认继承存储桶权限** | String | 否       |
| GrantRead                   | 赋予被授权者读取对象的权限。格式：id="[OwnerUin]"，可使用半角逗号（,）分隔多组被授权者：<br><li>当需要给子账户授权时，`id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>当需要给主账号授权时，`id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>例如`'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | 否       |
| GrantWrite                  | 赋予被授权者写入对象的权限。格式：id="[OwnerUin]"，可使用半角逗号（,）分隔多组被授权者：<br><li>当需要给子账户授权时，`id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>当需要给主账号授权时，`id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>例如`'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | 否       |
| GrantFullControl            | 赋予被授权者操作对象的所有权限，格式：id="[OwnerUin]"，可使用半角逗号（,）分隔多组被授权者：<br><li>当需要给子账户授权时，`id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>当需要给主账号授权时，`id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>例如`'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | 否       |
| MetadataDirective           | 是否拷贝元数据，枚举值：Copy，Replaced，默认值 Copy。假如标记为 Copy，忽略 Header 中的用户元数据信息直接复制；假如标记为 Replaced，按 Header 信息修改元数据。**当目标路径和原路径一致，即用户试图修改元数据时，必须为 Replaced** | String | 否       |
| CopySourceIfModifiedSince   | 当对象在指定时间后被修改，则执行操作，否则返回412。**可与 CopySourceIfNoneMatch 一起使用，与其他条件联合使用返回冲突** | String | 否       |
| CopySourceIfUnmodifiedSince | 当对象在指定时间后未被修改，则执行操作，否则返回412。**可与 CopySourceIfMatch 一起使用，与其他条件联合使用返回冲突** | String | 否       |
| CopySourceIfMatch           | 当对象的 Etag 和给定一致时，则执行操作，否则返回412。**可与CopySourceIfUnmodifiedSince 一起使用，与其他条件联合使用返回冲突** | String | 否       |
| CopySourceIfNoneMatch       | 当对象的 Etag 和给定不一致时，则执行操作，否则返回412。**可与 CopySourceIfModifiedSince 一起使用，与其他条件联合使用返回冲突** | String | 否       |
| StorageClass                | 设置对象的存储级别，枚举值：STANDARD、STANDARD_IA、ARCHIVE，默认值：STANDARD | String | 否       |
| x-cos-meta-*                | 其他自定义的文件头部                                         | String | 否       |

#### 回调函数说明

```
function(err, data) { ... }
```

| 参数名         | 参数描述                                                     | 类型   |
| -------------- | ------------------------------------------------------------ | ------ |
| err            | 请求发生错误时返回的对象，包括网络错误和业务错误。如果请求成功则为空，更多详情请参见 [错误码](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode   | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number |
| - headers      | 请求返回的头部信息                                           | Object |
| data           | 请求成功时返回的对象，如果请求发生错误，则为空               | Object |
| - statusCode   | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number |
| - headers      | 请求返回的头部信息                                           | Object |
| - ETag         | 文件的 MD5 算法校验值，例如`"22ca88419e2ed4721c23807c678adbe4c08a7880"`，**注意前后携带双引号** | String |
| - LastModified | 返回对象最后被修改时间，例如2017-06-23T12:33:27.000Z         | String |
| - VersionId    | 在开启过版本控制的存储桶中上传对象返回对象的版本 ID，存储桶从未开启则不返回该参数 | String |

### 删除单个对象

#### 功能说明

DELETE Object 接口请求可以在 COS 的存储桶中将一个对象（Object）删除。该操作需要请求者对存储桶有 WRITE 权限。

#### 使用示例

[//]: # ".cssg-snippet-delete-object"
```js
cos.deleteObject({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
    Key: 'exampleobject'        /* 必须 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 参数说明

| 参数名    | 参数描述                                                     | 类型   | 是否必填 |
| --------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket    | 存储桶的名称，命名格式为 BucketName-APPID，此处填写的存储桶名称必须为此格式 | String | 是       |
| Region    | 存储桶所在地域，枚举值请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224) | String | 是       |
| Key       | 对象键（Object 的名称），对象在存储桶中的唯一标识，详情请参见 [对象概述](https://intl.cloud.tencent.com/document/product/436/13324) | String | 是       |
| VersionId | 要删除的对象版本 ID 或 DeleteMarker 版本 ID                  | String | 否       |

#### 回调函数说明

```
function(err, data) { ... }
```

| 参数名       | 参数描述                                                     | 类型   |
| ------------ | ------------------------------------------------------------ | ------ |
| err          | 请求发生错误时返回的对象，包括网络错误和业务错误。如果请求成功则为空，更多详情请参见 [错误码](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number |
| - headers    | 请求返回的头部信息                                           | Object |
| data         | 请求成功时返回的对象，如果请求发生错误，则为空               | Object |
| - statusCode | 请求返回的 HTTP 状态码，例如200，204，403，404等，**如果删除成功或者文件不存在则返回204或200，如果找不到指定的 Bucket，则返回404** | Number |
| - headers    | 请求返回的头部信息                                           | Object |

### 删除多个对象

#### 功能说明

DELETE Multiple Objects 接口请求实现在指定存储桶中批量删除对象，单次请求最大支持批量删除1000个对象。对于响应结果，COS 提供 Verbose 和 Quiet 两种模式： Verbose 模式将返回每个对象的删除结果，Quiet 模式只返回报错的对象信息。

#### 使用示例

删除多个文件：

[//]: # ".cssg-snippet-delete-multi-object"
```js
cos.deleteMultipleObject({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
    Objects: [
        {Key: 'exampleobject'},
        {Key: 'exampleobject2'},
    ]
}, function(err, data) {
    console.log(err || data);
});
```

#### 参数说明

| 参数名      | 参数描述                                                     | 类型        | 是否必填 |
| ----------- | ------------------------------------------------------------ | ----------- | -------- |
| Bucket      | 存储桶的名称，命名格式为 BucketName-APPID，此处填写的存储桶名称必须为此格式 | String      | 是       |
| Region      | 存储桶所在地域，枚举值请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224) | String      | 是       |
| Quiet       | 布尔值，这个值决定了是否启动 Quiet 模式。值为 true 启动 Quiet 模式，值为 false 则启动 Verbose 模式，默认值为 false | Boolean     | 否       |
| Objects     | 要删除的对象列表                                             | ObjectArray | 是       |
| - Key       | 对象键（Object 的名称），对象在存储桶中的唯一标识，详情请参见 [对象概述](https://intl.cloud.tencent.com/document/product/436/13324) | String      | 是       |
| - VersionId | 要删除的对象版本 ID 或 DeleteMarker 版本 ID                  | String      | 否       |

#### 回调函数说明

```
function(err, data) { ... }
```

| 参数名&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | 参数描述                                                     | 类型        |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ----------- |
| err                                                          | 请求发生错误时返回的对象，包括网络错误和业务错误。如果请求成功则为空，更多详情请参见 [错误码](https://intl.cloud.tencent.com/document/product/436/7730) | Object      |
| - statusCode                                                 | 请求返回的 HTTP 状态码，例如200，204，403，404等             | Number      |
| - headers                                                    | 请求返回的头部信息                                           | Object      |
| data                                                         | 请求成功时返回的对象，如果请求发生错误，则为空               | Object      |
| - statusCode                                                 | 请求返回的 HTTP 状态码，例如200，204，403，404等             | Number      |
| - headers                                                    | 请求返回的头部信息                                           | Object      |
| - Deleted                                                    | 说明本次删除成功的对象信息列表                               | ObjectArray |
| - - Key                                                      | 对象键（Object 的名称），对象在存储桶中的唯一标识，详情请参见 [对象概述](https://intl.cloud.tencent.com/document/product/436/13324) | String      |
| - - VersionId                                                | 如果参数传入了 VersionId，返回也会带上 VersionId，表示刚操作的对象版本或 DeleteMarker 版本 | String      |
| - - DeleteMarker                                             | 如果开启了版本控制，并且参数没有 VersionId，本次删除不会真正抹去文件内容，只新增一个 DeleteMarker 代表可见的文件已删除，枚举值：true、false | String      |
| - - DeleteMarkerVersionId                                    | 当返回的 DeleteMarker 为 true 时，返回刚新增的 DeleteMarker 的 VersionId | String      |
| - Error                                                      | 说明本次删除失败的对象信息列表                               | ObjectArray |
| - - Key                                                      | 对象键（Object 的名称），对象在存储桶中的唯一标识，详情请参见 [对象概述](https://intl.cloud.tencent.com/document/product/436/13324) | String      |
| - - Code                                                     | 删除失败的错误码                                             | String      |
| - - Message                                                  | 删除错误信息                                                 | String      |

## 分块操作

### 查询分块上传

#### 功能说明

List Multipart Uploads 用来查询正在进行中的分块上传信息。单次最多列出1000个正在进行中的分块上传。

#### 使用示例

获取前缀为 exampleobject 的未完成的 UploadId 列表，示例如下：

[//]: # ".cssg-snippet-list-multi-upload"
```js
cos.multipartList({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
    Prefix: 'exampleobject',                        /* 非必须 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 参数说明

| 参数名         | 参数描述                                                     | 类型   | 是否必填 |
| -------------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket         | 存储桶的名称，命名格式为 BucketName-APPID，此处填写的存储桶名称必须为此格式 | String | 是       |
| Region         | 存储桶所在地域，枚举值请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224) | String | 是       |
| Prefix         | 对象键前缀匹配，限定返回中只包含指定前缀的对象键。注意使用 prefix 查询时，返回的对象键 中仍会包含 Prefix | String | 否       |
| Delimiter      | 定界符。为一个分隔符号，，用于对对象键进行分组。一般是传`/`。所有对象键从 Prefix 或从头（例如未指定 Prefix）到首个 delimiter 之间相同部分的路径归为一类，定义为 Common Prefix，然后列出所有 Common Prefix | String | 否       |
| EncodingType   | 规定返回值的编码格式，合法值：url                            | String | 否       |
| MaxUploads     | 设置最大返回的条目数量，合法取值为1 - 1000，默认1000         | String | 否       |
| KeyMarker      | 与 upload-id-marker 一起使用<br><li> 当 upload-id-marker 未被指定时：<br>&emsp;- ObjectName 字母顺序大于 key-marker 的条目将被列出<br><li>当 upload-id-marker 被指定时：<br>&emsp;- ObjectName 字母顺序大于 key-marker 的条目被列出<br>&emsp;- ObjectName 字母顺序等于 key-marker 且 UploadID 大于 upload-id-marker 的条目将被列出 | String | 否       |
| UploadIdMarker | 与 key-marker 一起使用<br><li>当 key-marker 未被指定时：<br>&emsp;- upload-id-marker 将被忽略<br><li>当 key-marker 被指定时：<br>&emsp;- ObjectName 字母顺序大于 key-marker 的条目被列出<br>&emsp;- ObjectName 字母顺序等于 key-marker 且 UploadID 大于 upload-id-marker 的条目将被列出 | String | 否       |

#### 回调函数说明

```
function(err, data) { ... }
```

| 参数名&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | 参数描述                                                     | 类型        |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ----------- |
| err                                                          | 请求发生错误时返回的对象，包括网络错误和业务错误，如果请求成功则为空，更多详情请参见 [错误码](https://intl.cloud.tencent.com/document/product/436/7730) | Object      |
| - statusCode                                                 | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number      |
| - headers                                                    | 请求返回的头部信息                                           | Object      |
| data                                                         | 请求成功时返回的对象，如果请求发生错误，则为空               | Object      |
| - statusCode                                                 | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number      |
| - headers                                                    | 请求返回的头部信息                                           | Object      |
| - Bucket                                                     | 分块上传的目标存储桶                                         | String      |
| - Encoding-Type                                              | 规定返回值的编码格式，合法值：url                            | String      |
| - KeyMarker                                                  | 列出条目从该 key 值开始                                      | String      |
| - UploadIdMarker                                             | 列出条目从该 UploadId 值开始                                 | String      |
| - NextKeyMarker                                              | 假如返回条目被截断，则返回 NextKeyMarker 就是下一个条目的起点 | String      |
| - NextUploadIdMarker                                         | 假如返回条目被截断，则返回 UploadId 就是下一个条目的起点     | String      |
| - MaxUploads                                                 | 设置最大返回的条目数量，合法取值为 1 - 1000                  | String      |
| - IsTruncated                                                | 返回条目是否被截断，'true' 或者 'false'                      | String      |
| - Prefix                                                     | 对象键前缀匹配，限定返回中只包含指定前缀的对象键。           | String      |
| - Delimiter                                                  | 定界符。为一个分隔符号，，用于对对象键进行分组。一般是传`/`。所有对象键从 Prefix 或从头（如未指定 Prefix）到首个 delimiter 之间相同部分的路径归为一类，定义为 Common Prefix，然后列出所有 Common Prefix | String      |
| - CommonPrefixs                                              | 将 prefix 到 delimiter 之间的相同路径归为一类，定义为 Common Prefix | ObjectArray |
| - - Prefix                                                   | 显示具体的 Common Prefixs                                    | String      |
| - Upload                                                     | 分块上传的信息集合                                           | ObjectArray |
| - - Key                                                      | 对象的名称，即对象键                                         | String      |
| - - UploadId                                                 | 表示本次分块上传的 ID                                        | String      |
| - - StorageClass                                             | 表示分块的存储级别，枚举值：STANDARD、STANDARD_IA、ARCHIVE   | String      |
| - - Initiator                                                | 表示本次上传发起者的信息                                     | Object      |
| - - - DisplayName                                            | 上传发起者的名称                                             | String      |
| - - - ID                                                     | 上传发起者 ID，格式：`qcs::cam::uin/<OwnerUin>:uin/<SubUin>` <br>如果是主账号，&lt;OwnerUin> 和 &lt;SubUin> 是同一个值 | String      |
| - - Owner                                                    | 表示这些分块持有者的信息                                     | Object      |
| - - - DisplayName                                            | 分块持有者的名称                                             | String      |
| - - - ID                                                     | 分块持有者 ID，格式：`qcs::cam::uin/<OwnerUin>:uin/<SubUin>` <br>如果是主账号，&lt;OwnerUin> 和 &lt;SubUin> 是同一个值 | String      |
| - - Initiated                                                | 分块上传的起始时间                                           | String      |

### 初始化分块上传

#### 功能说明

Initiate Multipart Upload 请求实现初始化分块上传，成功执行此请求后会返回 Upload ID ，用于后续的 Upload Part 请求。

#### 使用示例

[//]: # ".cssg-snippet-init-multi-upload"
```js
cos.multipartInit({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
    Key: 'exampleobject',              /* 必须 */
    UploadId: 'exampleUploadId',
    Body: fileObject
}, function(err, data) {
    console.log(err || data);
    if (data) {
      uploadId = data.UploadId;
    }
});
```

#### 参数说明

| 参数名             | 参数描述                                                     | 类型   | 是否必填 |
| ------------------ | ------------------------------------------------------------ | ------ | -------- |
| Bucket             | 存储桶的名称，命名格式为 BucketName-APPID，此处填写的存储桶名称必须为此格式 | String | 是       |
| Region             | 存储桶所在地域，枚举值请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224) | String | 是       |
| Key                | 对象键（Object 的名称），对象在存储桶中的唯一标识，详情请参见 [对象概述](https://intl.cloud.tencent.com/document/product/436/13324) | String | 是       |
| CacheControl       | RFC 2616 中定义的缓存策略，将作为对象的元数据保存            | String | 否       |
| ContentDisposition | RFC 2616 中定义的文件名称，将作为对象的元数据保存            | String | 否       |
| ContentEncoding    | RFC 2616 中定义的编码格式，将作为对象的元数据保存            | String | 否       |
| ContentType        | RFC 2616 中定义的内容类型（MIME），将作为对象的元数据保存    | String | 否       |
| Expires            | RFC 2616 中定义的过期时间，将作为对象的元数据保存            | String | 否       |
| ACL                | 定义对象的访问控制列表（ACL）属性，枚举值请参见 [ACL 概述](https://intl.cloud.tencent.com/document/product/436/30583) 文档中对象的预设 ACL 部分，如 default，private，public-read 等 <br>**注意：如果您不需要进行对象 ACL 控制，请设置为 default 或者此项不进行设置，默认继承存储桶权限** | String | 否       |
| GrantRead          | 赋予被授权者读取对象的权限，格式：id="[OwnerUin]"，可使用半角逗号（,）分隔多组被授权者：<br><li>当需要给子账户授权时，`id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>当需要给主账号授权时，`id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>例如`'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | 否       |
| GrantFullControl   | 赋予被授权者操作对象的所有权限，格式：id="[OwnerUin]"，可使用半角逗号（,）分隔多组被授权者：<br><li>当需要给子账户授权时，`id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>当需要给主账号授权时，`id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>例如`'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | 否       |
| StorageClass       | 设置对象的存储级别，枚举值：STANDARD、STANDARD_IA、ARCHIVE，默认值：STANDARD | String | 否       |
| x-cos-meta-*       | 允许用户自定义的头部信息，将作为对象的元数据返回。大小限制2KB | String | 否       |
| UploadAddMetaMd5   | 当上传时，给对象的元数据信息增加 x-cos-meta-md5 赋值为对象内容的 MD5 值，格式为 32 位小写字符串。例如：4d00d79b6733c9cc066584a02ed03410 | String | 否       |

#### 回调函数说明

```
function(err, data) { ... }
```

| 参数名   | 参数描述                                                     | 类型   |
| -------- | ------------------------------------------------------------ | ------ |
| err      | 请求发生错误时返回的对象，包括网络错误和业务错误。如果请求成功则为空，更多详情请参见 [错误码](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| data     | 请求成功时返回的对象，如果请求发生错误，则为空               | Object |
| Bucket   | 分块上传的目标存储桶，由用户自定义字符串和系统生成 APPID 数字串由中划线连接而成，例如 examplebucket-1250000000 | String |
| Key      | 对象键（Object 的名称），对象在存储桶中的唯一标识，详情请参见 [对象概述](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| UploadId | 在后续上传中使用的 ID                                        | String |

### 上传分块

#### 功能说明

Upload Part 接口请求实现在初始化以后的分块上传，支持的块的数量为1 - 10000，块的大小为1MB - 5GB。
<li>分块上传首先要进行初始化，用 Initiate Multipart Upload 接口初始化分块上传，得到一个 uploadId，该 ID 不但唯一标识这一分块数据，也标识了这分块数据在整个文件内的相对位置。</li>
<li>在每次请求 Upload Part 时候，需要携带 partNumber 和 uploadId，partNumber 为块的编号，支持乱序上传。</li>
<li>当传入 uploadId 和 partNumber 都相同的时候，后传入的块将覆盖之前传入的块。当 uploadId 不存在时会返回404错误，错误码为 NoSuchUpload。</li>

#### 使用示例

[//]: # ".cssg-snippet-upload-part"
```js
cos.multipartUpload({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
    Key: 'exampleobject',       /* 必须 */
    UploadId: 'exampleUploadId',
    PartNumber: '1',
    Body: fileObject
}, function(err, data) {
    console.log(err || data);
    if (data) {
      eTag = data.ETag;
    }
});
```

#### 参数说明

| 参数名 | 参数描述                                                     | 类型   | 必填 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 存储桶的名称，命名格式为 BucketName-APPID，此处填写的存储桶名称必须为此格式 | String  | 是   |