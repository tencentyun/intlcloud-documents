## 简介

本文档提供关于存储桶、对象的访问控制列表（ACL）的 API 概览以及 SDK 示例代码。

**存储桶 ACL**

| API                                                          | 操作名         | 操作描述                                |
| :----------------------------------------------------------- | :------------- | :-------------------------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | 设置存储桶 ACL | 设置指定存储桶的访问权限控制列表（ACL） |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | 查询存储桶 ACL | 查询指定存储桶的访问权限控制列表（ACL） |

**对象 ACL**

| API                                                          | 操作名       | 操作描述                           |
| :----------------------------------------------------------- | :----------- | :--------------------------------- |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | 设置对象 ACL | 设置存储桶中某个对象的访问控制列表 |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | 查询对象 ACL | 查询对象的访问控制列表             |

## 存储桶 ACL

### 设置存储桶 ACL

#### 功能说明

PUT Bucket acl 接口用来设置指定存储桶访问权限控制列表（ACL）。

#### 使用示例

设置存储桶公有读：

[//]: # (.cssg-snippet-put-bucket-acl)
```js
cos.putBucketAcl({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
    ACL: 'public-read'
}, function(err, data) {
    console.log(err || data);
});
```

为某个用户赋予存储桶所有权限：

[//]: # (.cssg-snippet-put-bucket-acl-user)
```js
cos.putBucketAcl({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
    GrantFullControl: 'id="qcs::cam::uin/100000000001:uin/100000000001",id="qcs::cam::uin/100000000011:uin/100000000011"' // 100000000001是 uin
}, function(err, data) {
    console.log(err || data);
});
```

通过 AccessControlPolicy 修改存储桶权限：

[//]: # (.cssg-snippet-put-bucket-acl-acp)
```js
cos.putBucketAcl({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
    AccessControlPolicy: {
        "Owner": { // AccessControlPolicy 里必须有 owner
            "ID": 'qcs::cam::uin/100000000001:uin/100000000001' // 100000000001 是 Bucket 所属用户的 Uin
        },
        "Grants": [{
            "Grantee": {
                "ID": "qcs::cam::uin/100000000011:uin/100000000011", // 100000000011 是 Uin
            },
            "Permission": "WRITE"
        }]
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### 参数说明

| 参数名              | 参数描述                                                     | 类型        | 是否必填 |
| ------------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket              | 存储桶的名称，命名规则为 BucketName-APPID，此处填写的存储桶名称必须为此格式 | String      | 是   |
| Region              | 存储桶所在地域，枚举值请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224) | String      | 是   |
| ACL                 | 定义存储桶的访问控制列表（ACL）属性。枚举值请参见 [ACL 概述](https://intl.cloud.tencent.com/document/product/436/30583) 文档中存储桶的预设 ACL 部分，例如 private，public-read 等，默认为 private | String      | 否   |
| GrantRead           | 赋予被授权者读取存储桶的权限，格式：id="[OwnerUin]"<br>可使用半角逗号（,）分隔多组被授权者：<br><li>当需要给子账号授权时，`id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br/><li>当需要给主账号授权时，`id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>例如`'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"' ` | String      | 否   |
| GrantWrite          | 赋予被授权者写入存储桶的权限，格式：id="[OwnerUin]"<br>可使用半角逗号（,）分隔多组被授权者：<br><li>当需要给子账号授权时，`id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br/><li>当需要给主账号授权时，`id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>例如`'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"' ` | String      | 否   |
| GrantReadAcp        | 赋予被授权者读取存储桶的访问控制列表（ACL）和存储桶策略（Policy）的权限。格式：id="[OwnerUin]"，可使用半角逗号（,）分隔多组被授权者：<br><li>当需要给子账号授权时，`id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>当需要给主账号授权时，`id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>例如`'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"' ` | String      | 否   |
| GrantWriteAcp       | 赋予被授权者写入存储桶的访问控制列表（ACL）和存储桶策略（Policy）的权限。格式：id="[OwnerUin]"，可使用半角逗号（,）分隔多组被授权者：<br><li>当需要给子账号授权时，`id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>当需要给主账号授权时，`id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`<br>例如`'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String      | 否   |
| GrantFullControl    | 赋予被授权者操作存储桶的所有权限，格式：id="[OwnerUin]"，可使用半角逗号（,）分隔多组被授权者：<br><li>当需要给子账号授权时，`id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`<br><li>当需要给主账号授权时，`id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`</br>例如`'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String      | 否   |
| AccessControlPolicy | 跨域资源共享配置的所有信息列表                               | Object      | 否   |
| - Owner             | 存储桶持有者的信息                                           | Object      | 否   |
| - - ID              | 存储桶持有者的完整 ID，格式为`qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`<br>例如`qcs::cam::uin/100000000001:uin/100000000001`，其中100000000001为 uin | String      | 否   |
| - Grants            | 被授权者信息与权限信息列表                                   | ObjectArray | 否   |
| - - Permission      | 授予的权限信息，可选项 READ、WRITE、READ_ACP、WRITE_ACP、FULL_CONTROL。枚举值详情参见 [ACL 概述](https://intl.cloud.tencent.com/document/product/436/30583) 文档中存储桶的操作部分 | String      | 否   |
| - - Grantee         | 被授权者的信息                                               | Object      | 否   |
| - - - ID            | 被授权者的完整 ID，格式为`qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`</br>例如`qcs::cam::uin/100000000001:uin/100000000001`，其中100000000001为 uin | String      | 否   |
| - - - DisplayName   | 被授权者的名称，一般填写成和 ID 一致的字符串                 | String      | 否   |
| - - - URI           | 预设用户组，请参见 [ACL 概述](https://intl.cloud.tencent.com/document/product/436/30583) 文档中预设用户组部分，例如`http://cam.qcloud.com/groups/global/AllUsers`或 `http://cam.qcloud.com/groups/global/AuthenticatedUsers` | String      | 否     |

#### 回调函数说明

```
function(err, data) { ... }
```

| 参数名&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | 参数描述                                                     | 类型   |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------ |
| err                                                          | 请求发生错误时返回的对象，包括网络错误和业务错误，如果请求成功则为空，更多详情请参见 [错误码](https://intl.cloud.tencent.com/document/product/436/7730) 文档 | Object |
| - statusCode                                                 | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number |
| - headers                                                    | 请求返回的头部信息                                           | Object |
| data                                                         | 请求成功时返回的对象，如果请求发生错误，则为空               | Object |
| - statusCode                                                 | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number |
| - headers                                                    | 请求返回的头部信息                                           | Object |

### 查询存储桶 ACL

#### 功能说明

GET Bucket acl 接口用来查询存储桶的访问控制列表（ACL）。该 API 的请求者需要对存储桶有写入 ACL 权限。

#### 使用示例

[//]: # (.cssg-snippet-get-bucket-acl)
```js
cos.getBucketAcl({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 返回示例

```json
{
    "GrantFullControl": "",
    "GrantWrite": "",
    "GrantRead": "",
    "GrantReadAcp": "id=\"qcs::cam::uin/100000000011:uin/100000000011\"",
    "GrantWriteAcp": "id=\"qcs::cam::uin/100000000011:uin/100000000011\"",
    "ACL": "private",
    "Owner": {
        "ID": "qcs::cam::uin/100000000001:uin/100000000001",
        "DisplayName": "qcs::cam::uin/100000000001:uin/100000000001"
    },
    "Grants": [{
        "Grantee": {
            "ID": "qcs::cam::uin/100000000011:uin/100000000011",
            "DisplayName": "qcs::cam::uin/100000000011:uin/100000000011"
        },
        "Permission": "READ"
    }],
    "statusCode": 200,
    "headers": {}
}
```

#### 参数说明

| 参数名 | 参数描述                                                     | 类型   | 必填 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 存储桶的名称，命名格式为 BucketName-APPID，此处填写的存储桶名称必须为此格式 | String | 是   |
| Region | 存储桶所在地域，枚举值请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224) | String | 是   |

#### 回调函数说明

```
function(err, data) { ... }
```

| 参数名&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | 参数描述                                                     | 类型        |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ----------- |
| err                                                          | 请求发生错误时返回的对象，包括网络错误和业务错误，如果请求成功则为空，更多详情请参见 [错误码](https://intl.cloud.tencent.com/document/product/436/7730) 文档 | Object      |
| - statusCode                                                 | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number      |
| - headers                                                    | 请求返回的头部信息                                           | Object      |
| data                                                         | 请求成功时返回的对象，如果请求发生错误则为空                 | Object      |
| - statusCode                                                 | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number      |
| - headers                                                    | 请求返回的头部信息                                           | Object      |
| - ACL                                                        | 定义存储桶的访问控制列表（ACL）属性。枚举值请参见 [ACL 概述](https://intl.cloud.tencent.com/document/product/436/30583) 文档中存储桶的预设 ACL 部分，例如 private，public-read 等，默认为 private | String      |
| - GrantRead                                                  | 具有读取存储桶权限的被授权者 ID 信息                         | String      |
| - GrantWrite                                                 | 具有写入存储桶权限的被授权者 ID 信息                         | String      |
| - GrantReadAcp                                               | 具有读取存储桶的访问控制列表（ACL）和存储桶策略（Policy）权限的被授权者 ID 信息 | String      |
| - GrantWriteAcp                                              | 具有写入存储桶的访问控制列表（ACL）和存储桶策略（Policy）权限的被授权者 ID 信息 | String      |
| - GrantFullControl                                           | 具有存储桶所有权限的被授权者 ID 信息                         | String      |
| - Owner                                                      | 存储桶持有者的信息                                           | Object      |
| - - DisplayName                                              | 存储桶持有者的名称                                           | String      |
| - - ID                                                       | 存储桶持有者的完整 ID<br>格式为`qcs::cam::uin/<OwnerUin>:uin/<SubUin>` <br>如果是主帐号，&lt;OwnerUin> 和 &lt;SubUin> 是同一个值 | String      |
| - Grants                                                     | 被授权者信息与权限信息列表                                   | ObjectArray |
| - - Permission                                               | 指明授予被授权者的权限信息，枚举值：READ、WRITE、READ_ACP、WRITE_ACP、FULL_CONTROL | String      |
| - - Grantee                                                  | 被授权者的信息                                               | Object      |
| - - - DisplayName                                            | 被授权者的名称                                               | String      |
| - - - ID                                                     | 被授权者的完整 ID，<br>如果是主账号，格式为`qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>` <br>或 `qcs::cam::anyone:anyone` （指代所有用户）<br>如果是子帐号，格式为`qcs::cam::uin/<OwnerUin>:uin/<SubUin>` | String      |
| - - - URI                                                    | 预设用户组，请参见 [ACL 概述](https://intl.cloud.tencent.com/document/product/436/30583) 文档中预设用户组部分，例如 `http://cam.qcloud.com/groups/global/AllUsers` 或 `http://cam.qcloud.com/groups/global/AuthenticatedUsers` | String      |


## 对象 ACL

### 设置对象 ACL

#### 功能说明

PUT Object acl 接口用来设置特定存储桶中某个对象的访问控制列表（ACL）。

> !每个主账号（即同一个 APPID），存储桶的 ACL、Policy 和 CAM 关联的策略数量总和最多为1000条，对象访问控制列表（ACL）规则数量不限制。如果您不需要进行对象访问控制列表（ACL）控制，请不要设置，默认继承存储桶权限。

#### 使用示例

[//]: # (.cssg-snippet-put-object-acl)
```js
cos.putObjectAcl({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
    Key: 'exampleobject',              /* 必须 */
    ACL: 'public-read',        /* 非必须 */
}, function(err, data) {
    console.log(err || data);
});
```

为某个用户赋予对象的所有权限：

[//]: # (.cssg-snippet-put-object-acl-user)
```js
cos.putObjectAcl({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
    Key: 'exampleobject',              /* 必须 */
    GrantFullControl: 'id="100000000001"' // 100000000001是主账号 uin
}, function(err, data) {
    console.log(err || data);
});
```

通过 AccessControlPolicy 赋予对象写权限：

[//]: # (.cssg-snippet-put-object-acl-acp)
```js
cos.putObjectAcl({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
    Key: 'exampleobject',              /* 必须 */
    AccessControlPolicy: {
        "Owner": { // AccessControlPolicy 里必须有 owner
            "ID": 'qcs::cam::uin/100000000001:uin/100000000001' // 100000000001 是 Bucket 所属用户的 UIN 账号
        },
        "Grants": [{
            "Grantee": {
                "ID": "qcs::cam::uin/100000000011:uin/100000000011", // 100000000011 是 Bucket 所属用户下的子账号 UIN
            },
            "Permission": "WRITE"
        }]
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### 参数说明

| 参数名              | 参数描述                                                     | 类型        | 是否必填 |
| ------------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket              | 存储桶的名称，命名格式为 BucketName-APPID，此处填写的存储桶名称必须为此格式 | String      | 是   |
| Region              | 存储桶所在地域，枚举值请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224) | String      | 是   |
| Key                 | 对象键（Object 的名称），对象在存储桶中的唯一标识，详情请参见 [[对象概述](https://intl.cloud.tencent.com/document/product/436/13324)](https://intl.cloud.tencent.com/document/product/436/13324) | String      | 是   |
| ACL                 | 定义对象的访问控制列表（ACL）属性，枚举值请参见 [ACL 概述](https://intl.cloud.tencent.com/document/product/436/30583) 文档中对象的预设 ACL 部分，如 default，private，public-read 等 <br>**注意：如果您不需要进行对象 ACL 控制，请设置为 default 或者此项不进行设置，默认继承存储桶权限** | String      | 否   |
| GrantRead           | 赋予被授权者读取对象的权限。格式：id="[OwnerUin]"，可使用半角逗号（,）分隔多组被授权者：<ul  style="margin: 0;"><li>当需要给子账户授权时，<code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code><br><li>当需要给主账号授权时，<code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code><br>例如<code>'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'</code></li></ul>| String      | 否   |
| GrantFullControl    | 赋予被授权者操作对象的所有权限，格式：id="[OwnerUin]"，可使用半角逗号（,）分隔多组被授权者：<ul  style="margin: 0;"><li>当需要给子账户授权时，<code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;"</code></li><li>当需要给主账号授权时，<code>id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"</code><br>例如<code>'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'</code></li></ul>| String      | 否   |
| AccessControlPolicy | 设置对象的访问控制列表（ACL）属性信息                        | Object      | 否   |
| - Owner             | 对象持有者的信息                                             | Object      | 否   |
| - - ID              | 对象持有者 ID，格式：`qcs::cam::uin/<OwnerUin>:uin/<SubUin>` <br>如果是主账号，&lt;OwnerUin> 和 &lt;SubUin> 是同一个值 | String      | 否   |
| - - DisplayName     | 对象持有者的名称                                             | String      | 否   |
| - Grants            | 被授权者信息与权限信息列表                                   | ObjectArray | 否   |
| - - Permission      | 指明授予被授权者的权限信息，枚举值：READ、WRITE、READ_ACP、WRITE_ACP、FULL_CONTROL | String      | 否   |
| - - Grantee         | 被授权者的信息                                               | Object      | 否   |
| - - - DisplayName   | 被授权者的名称                                               | String      | 否   |
| - - - ID            | 被授权者的 ID，格式：`qcs::cam::uin/<OwnerUin>:uin/<;SubUin>`<br>如果是主账号，&lt;OwnerUin> 和 &lt;SubUin> 是同一个值 | String      | 否   |

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
| - statusCode | 请求返回的 HTTP 状态码，例如200，204，403，404等             | Number |
| - headers    | 请求返回的头部信息                                           | Object |

### 查询对象 ACL

#### 功能说明

GET Object acl 接口用来查询某个 Bucket 下的某个 Object 的访问权限。只有 Bucket 的持有者才有权限操作。

#### 使用示例

[//]: # (.cssg-snippet-get-object-acl)
```js
cos.getObjectAcl({
    Bucket: 'examplebucket-1250000000', /* 必须 */
    Region: 'COS_REGION',     /* 存储桶所在地域，必须字段 */
    Key: 'exampleobject',              /* 必须 */
}, function(err, data) {
    console.log(err || data);
});
```

#### 参数说明

| 参数名 | 参数描述                                                     | 类型   | 是否必填 |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | 存储桶的名称，命名格式为 BucketName-APPID，此处填写的存储桶名称必须为此格式 | String | 是   |
| Region | 存储桶所在地域，枚举值请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224) | String | 是   |
| Key    | 对象键（Object 的名称），对象在存储桶中的唯一标识，详情请参见 [对象概述](https://intl.cloud.tencent.com/document/product/436/13324) | String | 是   |

#### 回调函数说明

```
function(err, data) { ... }
```

| 参数名            | 参数描述                                                     | 类型        |
| ----------------- | ------------------------------------------------------------ | ----------- |
| err               | 请求发生错误时返回的对象，包括网络错误和业务错误。如果请求成功则为空，更多详情请参见 [错误码](https://intl.cloud.tencent.com/document/product/436/7730) | Object      |
| - statusCode      | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number      |
| - headers         | 请求返回的头部信息                                           | Object      |
| data              | 请求成功时返回的对象，如果请求发生错误，则为空               | Object      |
| - statusCode      | 请求返回的 HTTP 状态码，例如200、403、404等                  | Number      |
| - headers         | 请求返回的头部信息                                           | Object      |
| - ACL             | 定义对象的访问控制列表（ACL）属性，枚举值请参见 [ACL 概述](https://intl.cloud.tencent.com/document/product/436/30583) 文档中对象的预设 ACL 部分，如 default，private，public-read 等 <br>**注意：如果您不需要进行对象 ACL 控制，请设置为 default 或者此项不进行设置，默认继承存储桶权限** | String      |
| - Owner           | 标识资源的所有者                                             | Object      |
| - - ID            | 对象持有者 ID，格式为：`qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>如果是主账号 ID，&lt;OwnerUin> 和 &lt;SubUin>是同一个值 | String      |
| - - DisplayName   | 对象持有者的名称                                             | String      |
| - Grants          | 被授权者信息与权限信息列表                                   | ObjectArray |
| - - Permission    | 指明授予被授权者的权限信息，枚举值：READ、READ_ACP、WRITE_ACP、FULL_CONTROL | String      |
| - - Grantee       | 说明被授权者的信息                                           | Object      |
| - - - DisplayName | 用户的名称                                                   | String      |
| - - - ID          | 用户的 ID，格式为：`qcs::cam::uin/<OwnerUin>:uin/<SubUin>`</br> 如果是主账号 ID，&lt;OwnerUin> 和 &lt;SubUin> 是同一个值 | String      |





