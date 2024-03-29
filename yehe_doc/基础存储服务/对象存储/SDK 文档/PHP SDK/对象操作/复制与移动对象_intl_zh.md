## 简介

本文档提供关于复制与移动对象的相关的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名                       | 操作描述               |
| ------------------------------------------------------------ | ---------------------------- | ---------------------- |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | 设置对象复制（修改对象属性） | 复制文件到目标路径     |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | 复制分块       | 将其他对象复制为一个分块             |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | 删除单个对象                 | 在存储桶中删除指定对象 |

## 高级接口（推荐）

### 复制对象

#### 功能说明

该接口内部会根据文件大小，对小文件调用设置对象复制接口，对大文件调用分块复制接口。该功能常用于修改对象属性。接口参数可参照`PUT Object - Copy`和`Upload Part - Copy`接口。

#### 请求示例

#### 示例一：复制对象

[//]: # (.cssg-snippet-transfer-copy-object)

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //替换为用户的 secretId，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //替换为用户的 secretKey，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //替换为用户的 region，已创建桶归属的region可以在控制台查看，https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', //协议头部，默认为http
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));

try {
    $result = $cosClient->Copy(
        $bucket = 'examplebucket-1250000000', //存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
        $key = 'exampleobject', //此处的 key 为对象键
        $copySorce = array(
            'Region' => 'COS_REGION', 
            'Bucket' => 'sourcebucket-1250000000', 
            'Key' => 'sourceobject', 
        )
    );
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo($e);
}
```

[//]: # (.cssg-snippet-transfer-copy-object-update-storage-class)

#### 示例二：转换对象存储类型

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //替换为用户的 secretId，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //替换为用户的 secretKey，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //替换为用户的 region，已创建桶归属的region可以在控制台查看，https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', //协议头部，默认为http
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));

try {
    $result = $cosClient->Copy(
        $bucket = 'examplebucket-1250000000', //存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
        $key = 'exampleobject', //此处的 key 为对象键
        $copySorce = array(
            'Region' => 'COS_REGION', 
            'Bucket' => 'examplebucket-1250000000', 
            'Key' => 'exampleobject', 
        ),
        $options = array(
            'StorageClass' => 'Archive'
        )
    );
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo($e);
}
```

[//]: # (.cssg-snippet-transfer-copy-object-update-metadata)

#### 示例三：修改对象存储属性

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //替换为用户的 secretId，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //替换为用户的 secretKey，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //替换为用户的 region，已创建桶归属的region可以在控制台查看，https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', //协议头部，默认为http
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));

try {
    $result = $cosClient->Copy(
        $bucket = 'examplebucket-1250000000', //存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
        $key = 'exampleobject', //此处的 key 为对象键
        $copySorce = array(
            'Region' => 'COS_REGION', 
            'Bucket' => 'sourcebucket-1250000000', 
            'Key' => 'sourceObject', 
        ),
        $options = array(
            'MetadataDirective' => 'Replaced',
            'Metadata' => array(
                'string' => 'string',
            ),
        )
    );
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo($e);
}
```
## 简单复制
### 设置对象复制

将一个对象复制到目标路径（PUT Object - Copy）。

#### 方法原型

```php
public Guzzle\Service\Resource\Model copyObject(array $args = array());
```

#### 请求示例

#### 示例一：复制对象

[//]: # (.cssg-snippet-copy-object)

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //替换为用户的 secretId，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //替换为用户的 secretKey，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //替换为用户的 region，已创建桶归属的region可以在控制台查看，https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', //协议头部，默认为http
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));

try {
    $result = $cosClient->copyObject(array(
        'Bucket' => 'examplebucket-1250000000', //存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
        'CopySource' => 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject',
    )); 
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo($e);
}
```

#### 示例二：复制指定版本的对象

[//]: # (.cssg-snippet-copy-object-with-versionId)

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //替换为用户的 secretId，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //替换为用户的 secretKey，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //替换为用户的 region，已创建桶归属的region可以在控制台查看，https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', //协议头部，默认为http
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));

try {
    $result = $cosClient->copyObject(array(
        'Bucket' => 'examplebucket-1250000000', //存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
        'CopySource' => 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject?versionId=MTg0NDUxNjI3NTM0ODE2Njc0MzU',
    )); 
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo($e);
}
```

#### 示例三：修改存储类型为归档

[//]: # (.cssg-snippet-copy-object-update-storage-class)

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //替换为用户的 secretId，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //替换为用户的 secretKey，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //替换为用户的 region，已创建桶归属的region可以在控制台查看，https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', //协议头部，默认为http
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));

try {
    $result = $cosClient->copyObject(array(
        'Bucket' => 'examplebucket-1250000000', //存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
        'CopySource' => 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject',
        'StorageClass' => 'Archive'
    )); 
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo($e);
}
```

#### 示例四：修改 meta 属性

[//]: # (.cssg-snippet-copy-object-update-metadata)

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //替换为用户的 secretId，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //替换为用户的 secretKey，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //替换为用户的 region，已创建桶归属的region可以在控制台查看，https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', //协议头部，默认为http
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));

try {
    $result = $cosClient->copyObject(array(
        'Bucket' => 'examplebucket-1250000000', //存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
        'CopySource' => 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject',
        'MetadataDirective' => 'Replaced',
        'Metadata' => array(
            'key1' => 'value1',
            'key2' => 'value2',
        )
    )); 
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo($e);
}
```

#### 参数说明

| 参数名称          | 类型   | 描述                                                         | 是否必填 |
| ----------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket            | String | 存储桶名称，格式：BucketName-APPID                           | 是       |
| Key               | String | 此处的 Key 为对象键，对象键是对象在存储桶中的唯一标识。例如，在对象的访问域名<br>`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`中，对象键为`doc/pic.jpg` | 是       |
| CopySource        | String | 描述拷贝源文件的路径，包含 Appid、Bucket、Key、Region，<br>例如`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg` | 是       |
| MetadataDirective | String | 可选值为 Copy、Replaced。设置为 Copy 时，忽略设置的用户元数据信息直接复制，设置为 Replaced 时，按设置的元信息修改元数据，当目标路径和源路径一样时，必须设置为 Replaced | 否       |

## 分块复制

>? 如果为了方便查看理解分块复制接口，这里会罗列其相关所有接口，与上传对象文档中一致。
>

### 查询分块

#### 功能说明

查询指定存储桶中正在进行的分块上传（List Multipart Uploads）。

#### 方法原型

```php
public Guzzle\Service\Resource\Model listMultipartUploads(array $args = array());
```

#### 请求示例

[//]: # (.cssg-snippet-list-multi-upload)

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //替换为用户的 secretId，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //替换为用户的 secretKey，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //替换为用户的 region，已创建桶归属的region可以在控制台查看，https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', //协议头部，默认为http
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));

try {
    $result = $cosClient->listMultipartUploads(array(
        'Bucket' => 'examplebucket-1250000000', //存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
        'Delimiter' => '/',
        'EncodingType' => 'url',
        'KeyMarker' => 'prfixKeyMarker',
        'UploadIdMarker' => 'string',
        'Prefix' => 'prfix',
        'MaxUploads' => 1000,
    )); 
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo($e);
}
```

#### 参数说明

| 参数名称       | 类型   | 描述                                                         | 是否必填 |
| -------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket         | String | 存储桶名称，格式：BucketName-APPID                           | 是       |
| Delimiter      | String | 默认为空，设置分隔符，例如设置`/`来模拟文件夹                | 否       |
| EncodingType   | String | 默认不编码，规定返回值的编码方式，可选值：url                | 否       |
| KeyMarker      | String | 标记返回 parts 的 list 的起点位置                            | 否       |
| UploadIdMarker | String | 标记返回 parts 的 list 的起点位置                            | 否       |
| Prefix         | String | 默认为空，对 parts 的 key 进行筛选，匹配指定前缀（prefix）的 objects | 否       |
| MaxUploads     | Int    | 最多返回的 parts 数量，默认为最大的1000                      | 否       |


#### 返回结果说明

| 参数名称     | 类型   | 描述                               | 父节点  |
| ------------ | ------ | ---------------------------------- | ------- |
| Bucket       | String | 存储桶名称，格式：BucketName-APPID | 无      |
| IsTruncated  | Int    | 表示返回的 objects 否被截断        | 无      |
| Uploads      | Array  | 返回的分块列表                     | 无      |
| Upload       | Array  | 返回的分块属性                     | Uploads |
| Key          | String | 对象键                           | Upload  |
| UploadId     | String | 对象的分块上传 ID                  | Upload  |
| Initiator    | String | 初始化该分块的操作者               | Upload  |
| Owner        | String | 分块拥有者                         | Upload  |
| StorageClass | String | 分块的存储类型                       | Upload  |
| Initiated    | String | 分块初始化时间                     | Upload  |



### 初始化分块

#### 功能说明

初始化 Multipart Upload 上传操作（Initiate Multipart Upload）。

#### 方法原型

```php
public Guzzle\Service\Resource\Model createMultipartUpload(array $args = array());
```

#### 请求示例

[//]: # (.cssg-snippet-init-multi-upload)

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //替换为用户的 secretId，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //替换为用户的 secretKey，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //替换为用户的 region，已创建桶归属的region可以在控制台查看，https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', //协议头部，默认为http
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));

try {
    $result = $cosClient->createMultipartUpload(array(
        'Bucket' => 'examplebucket-1250000000', //存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
    )); 
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo($e);
}
```

#### 参数说明

| 参数名称             | 类型   | 描述                                                         | 是否必填 |
| -------------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket               | String | 存储桶名称，格式：BucketName-APPID                           | 是       |
| Key                  | String | 此处的 Key 为对象键，对象键是对象在存储桶中的唯一标识。例如，在对象的访问域名<br>`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`中，对象键为`doc/pic.jpg` | 是       |
| CacheControl         | String | 缓存策略，设置 Cache-Control                                 | 否       |
| ContentDisposition   | String | 文件名称，设置 Content-Disposition                           | 否       |
| ContentEncoding      | String | 编码格式，设置 Content-Encoding                              | 否       |
| ContentLanguage      | String | 语言类型，设置 Content-Language                              | 否       |
| ContentLength        | Int    | 设置传输长度                                                 | 否       |
| ContentType          | String | 内容类型，设置 Content-Type                                  | 否       |
| Expires              | String | 设置 Content-Expires                                         | 否       |
| Metadata             | Array  | 用户自定义的文件元信息                                       | 否       |
| StorageClass         | String | 文件的存储类型，例如 STANDARD、STANDARD_IA、ARCHIVE，默认值：STANDARD。更多存储类型请参见 [存储类型概述](https://intl.cloud.tencent.com/document/product/436/30925)       |    否       |
| ContentMD5           | Boolean | 是否自动生成上传文件的 MD5 值用于校验                           | 否       |
| ServerSideEncryption | String | 服务端加密方法                                               | 否       |


#### 返回结果说明

| 参数名称 | 类型   | 描述                               | 父节点 |
| -------- | ------ | ---------------------------------- | ------ |
| Bucket   | String | 存储桶名称，格式：BucketName-APPID | 无     |
| Key      | String | 对象键                             | 无     |
| UploadId | String | 对象分块上传的 ID                   | 无     |


### 复制分块

#### 功能说明

将其他对象复制为一个分块（Upload Part - Copy）。

#### 方法原型

```php
public Guzzle\Service\Resource\Model uploadPartCopy(array $args = array());
```

#### 请求示例

[//]: # (.cssg-snippet-upload-part-copy)

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //替换为用户的 secretId，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //替换为用户的 secretKey，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //替换为用户的 region，已创建桶归属的region可以在控制台查看，https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', //协议头部，默认为http
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));

try {
    $result = $cosClient->uploadPartCopy(array(
        'Bucket' => 'examplebucket-1250000000', //存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject', 
        'CopySource' => 'sourcebucket-1250000000.cos.ap-guangzhou.myqcloud.com/sourceObject',
        'CopySourceRange' => 'bytes=0-1', //这里举例只拷贝前两个字节
        'UploadId' => 'exampleUploadId', //UploadId 为对象分块上传的 ID，在分块上传初始化的返回参数里获得 
        'PartNumber' => 1, //PartNumber 为分块的序列号，COS 会根据携带序列号合并分块
    )); 
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo($e);
}
```

#### 参数说明

| 参数名称      | 类型   | 描述                                                         | 是否必填 |
| ------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket        | String | 存储桶名称，格式：BucketName-APPID                           | 是       |
| Key           | String | 对象键                                                       | 是       |
| UploadId      | String | UploadId 为对象分块上传的 ID，在分块上传初始化的返回参数里获得 | 是       |
| CopySource    | String | 描述拷贝源文件的路径，包含 APPID、Bucket、Key、Region，<br>例如`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg` | 是       |
| CopySourceRange    | String | 描述拷贝源对象的范围，格式为 bytes=first-last。不指定时，默认拷贝整个源对象 | 否       |
| PartNumber    | Int    | PartNumber 为分块的序列号，COS 会根据携带序列号合并分块      | 是       |
| ContentLength | Int    | 设置传输长度                                                 | 否       |
| ContentMD5    | Boolean | 是否自动生成上传文件的 MD5 值用于校验                             | 否       |

#### 返回结果示例

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [ETag] => "96e79218965eb72c92a549dd5a330112"
            [LastModified] => "2017-09-04T04:45:45"
            [RequestId] => NWNhNDdjYWFfNjNhYjM1MGFfMjk2NF8xY2ViMWM=
            [CRC] => 16749565679157681890
        )

)
```

#### 返回结果说明

| 参数名称     | 类型   | 描述                           | 父节点 |
| ------------ | ------ | ------------------------------ | ------ |
| ETag         | String | 分块的 MD5 值                  | 无     |
| LastModified | String | 返回对象最后修改时间，GMT 格式 | 无     |
| CRC     | String | CRC64 检验码来进行 [数据校验](https://intl.cloud.tencent.com/document/product/436/34078) | 无     |


### 完成分块

#### 功能说明

完成整个文件的分块上传（Complete Multipart Upload）。

#### 方法原型

```php
public Guzzle\Service\Resource\Model completeMultipartUpload(array $args = array());

```

#### 请求示例

[//]: # (.cssg-snippet-complete-multi-upload)

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //替换为用户的 secretId，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //替换为用户的 secretKey，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //替换为用户的 region，已创建桶归属的region可以在控制台查看，https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', //协议头部，默认为http
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));

try {
    $result = $cosClient->completeMultipartUpload(array(
        'Bucket' => 'examplebucket-1250000000', //存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject', 
        'UploadId' => 'exampleUploadId',
        'Parts' => array(
            array(
                'ETag' => 'exampleETag',
                'PartNumber' => 1,
            )), 
            // ... repeated
    )); 
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo($e);
}
```

#### 参数说明

| 参数名称   | 类型   | 描述                               | 是否必填 |
| ---------- | ------ | ---------------------------------- | -------- |
| Bucket     | String | 存储桶名称，格式：BucketName-APPID | 是       |
| Key        | String | 对象键                             | 是       |
| UploadId   | String | 对象分块上传的 ID                  | 是       |
| Parts      | Array  | 分块信息列表                       | 是       |
| Part       | Array  | 上传分块的内容信息                 | 是       |
| ETag       | String | 分块内容的 MD5                     | 是       |
| PartNumber | Int    | 分块编号                           | 是       |

## 移动对象

移动对象主要包括两个操作：复制源对象到目标位置，删除源对象。

由于 COS 通过存储桶名称（Bucket）和对象键（ObjectKey）来标识对象。移动对象也就意味着修改这个对象的标识，COS PHP SDK 目前没有提供修改对象唯一标识名的单独接口，但是可以通过组合**复制对象**加上**删除对象**的基本操作，来达到修改对象标识的目的，从而实现移动对象。

例如将 mybucket-1250000000 这个存储桶中的 picture.jpg 这个对象移动到同个存储桶的 doc 路径下。首先可以复制 picture.jpg 对象到存储桶的 doc 路径下，即对象键设定为 doc/picture.jpg，复制完成后删除 picture.jpg 这个对象，来实现“移动”的效果。

同样的，如果想将 mybucket-1250000000 这个存储桶里的 picture.jpg 这个对象移动到 myanothorbucket-1250000000 这个存储桶里，可以先将对象复制到 myanothorbucket-1250000000 存储桶，然后删除原来的对象。



#### 示例代码

[//]: #	".cssg-snippet-move-object"

```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //替换为用户的 secretId，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //替换为用户的 secretKey，请登录访问管理控制台进行查看和管理，https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //替换为用户的 region，已创建桶归属的region可以在控制台查看，https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', //协议头部，默认为http
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));

try {
    $cosClient->copy(
        $bucket = 'examplebucket-125000000', //存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
        $key = 'exampleobject',
        $copySource = array(
            'Region' => '<sourceRegion>', 
            'Bucket' => '<sourceBucket>', 
            'Key' => '<sourceKey>', 
        )
    );
    $result = $cosClient->deleteObject(array(
        'Bucket' => 'examplebucket-125000000', //存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
    ));
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo($e);
}
```

