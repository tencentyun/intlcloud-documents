本文档提供关于生命周期的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名       | 操作描述                       |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | 设置生命周期 | 设置存储桶的生命周期管理的配置 |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | 查询生命周期 | 查询存储桶生命周期管理的配置   |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | 删除生命周期 | 删除存储桶生命周期管理的配置   |

## 设置生命周期

#### 功能说明

设置指定存储桶的生命周期配置信息（PUT Bucket lifecycle）。

#### 方法原型

```php
public Guzzle\Service\Resource\Model putBucketLifecycle(array $args = array());
```

#### 请求示例

#### 示例一：全部对象生成1天后删除

[//]: # (.cssg-snippet-put-bucket-lifecycle)

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
    $result = $cosClient->putBucketLifecycle(array(
        'Bucket' => 'examplebucket-1250000000', //存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
        'Rules' => array(
            array(
                'Expiration' => array(
                    'Days' => 1,
                ),
                'ID' => 'rule01',
                'Filter' => array(
                    'Prefix' => ''
                ),
                'Status' => 'Enabled',
            ),
        )
    ));
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo "$e\n";
}
```

#### 示例二：某前缀下对象生成1天沉降为归档

[//]: # (.cssg-snippet-put-bucket-lifecycle-archive)

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
    $result = $cosClient->putBucketLifecycle(array(
        'Bucket' => 'examplebucket-1250000000', //存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
        'Rules' => array(
            array(
                'ID' => 'rule01',
                'Filter' => array(
                    'Prefix' => 'prefix01/'
                ),  
                'Status' => 'Enabled',
                'Transitions' => array(
                    array(
                        'Days' => 1,
                        'StorageClass' => 'Archive'
                    ),
                ),  
            ),
        )
    ));  
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo "$e\n";
}
```

#### 参数说明

| 参数名称                    | 类型         | 描述                                                         | 必填 |
| --------------------------- | ------------ | ------------------------------------------------------------ | ---- |
| Bucket                      | String       | 设置生命周期的存储桶，格式：BucketName-APPID                 | 是   |
| Rules                       | Array        | 生命周期信息列表                                             | 是   |
| Rule                        | Array        | 生命周期信息                                                 | 是   |
| Expiration                  | Array        | 设置 Object 过期规则，可以指定天数 Days 或者指定日期 Date    | 否   |
| Transition                  | Array        | 设置 Object 转换存储类型规则                                 | 否   |
| NoncurrentVersionExpiration | Array        | 设置 历史 Object 过期规则                                    | 否   |
| NoncurrentVersionTransition | Array        | 设置 历史 Object 转换存储类型规则                            | 否   |
| Filter                      | Array        | 用于描述规则影响的 Object 集合                               | 是   |
| Prefix                      | String       | 过滤的对象的前缀                                             | 是   |
| Status                      | String       | 设置 Rule 是否启用，可选值为 Enabled 、 Disabled             | 是   |
| ID                          | String       | 配置规则的 ID                                                | 是   |
| Days                        | Int          | 设置生效的天数                                               | 否   |
| Date                        | Int / String | 设置生效的日期                                               | 否   |
| NoncurrentDays              | Int          | 设置非多版本对象生效的天数                                   | 否   |
| StorageClass                | String       | 转换的文件的存储类型，STANDARD 、 STANDARD_IA 、 ARCHIVE，默认值：STANDARD | 是   |

## 查询生命周期

#### 功能说明

查询存储桶的生命周期管理配置（GET Bucket lifecycle）。

#### 方法原型

```php
public Guzzle\Service\Resource\Model getBucketLifecycle(array $args = array());
```

#### 请求示例

[//]: # (.cssg-snippet-get-bucket-lifecycle)

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
    $result = $cosClient->getBucketLifecycle(array(
        'Bucket' => 'examplebucket-1250000000' //存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
    )); 
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo($e);
}
```

#### 参数说明

| 参数名称 | 类型   | 描述                                         | 是否必填 |
| -------- | ------ | -------------------------------------------- | -------- |
| Bucket   | String | 查询生命周期的存储桶，格式：BucketName-APPID | 是       |

#### 返回结果示例

```php
Guzzle\Service\Resource\Model Object
(
    [data:protected] => Array
        (
            [Rules] => Array
                (
                    [0] => Array
                        (
                            [ID] => id1
                            [Filter] => Array
                                (
                                    [Prefix] => documents/
                                )
                            [Status] => Enabled
                            [Transition] => Array
                                (
                                    [Days] => 200
                                    [StorageClass] => Standard_IA
                                )
                            [Expiration] => Array
                                (
                                    [Days] => 1000
                                )
                        )
                )
            [RequestId] => NWE3YzhlZjNfY2FhMzNiMGFfNDVkNF8yZDIxODE=
        )
)
```

#### 返回结果说明

| 参数名称     | 类型         | 描述                                                         | 父节点                  |
| ------------ | ------------ | ------------------------------------------------------------ | ----------------------- |
| Rules        | Array        | 生命周期信息列表                                             | 无                      |
| Rule         | Array        | 生命周期信息                                                 | Rules                   |
| Expiration   | Array        | 设置 Object 过期规则，可以指定天数 Days 或者指定日期 Date    | Rule                    |
| Transition   | Array        | 设置 Object 转换存储类型规则                                 | Rule                    |
| Filter       | Array        | 用于描述规则影响的 Object 集合                               | Rule                    |
| Prefix       | String       | 过滤的对象的前缀                                             | Filter                  |
| Status       | String       | 设置 Rule 是否启用，可选值为 Enabled 、 Disabled             | Rule                    |
| ID           | String       | 配置规则的 ID                                                | Rule                    |
| Days         | Int          | 设置生效的天数                                               | Expiration / Transition |
| Date         | Int / String | 设置生效的日期                                               | Expiration / Transition |
| StorageClass | String       | 转换的文件的存储类型，STANDARD 、 STANDARD_IA 、 ARCHIVE，默认值：STANDARD | Transition              |



## 删除生命周期

#### 功能说明

删除 Bucket 生命周期管理的配置（DELETE Bucket lifecycle）。

#### 方法原型

```php
public Guzzle\Service\Resource\Model deleteBucketLifecycle(array $args = array());
```

#### 请求示例

[//]: # (.cssg-snippet-delete-bucket-lifecycle)

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
    $result = $cosClient->deleteBucketLifecycle(array(
        'Bucket' => 'examplebucket-1250000000' //存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
    )); 
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo($e);
}
```

#### 参数说明

| 参数名称 | 类型   | 描述                                               | 是否必填 |
| -------- | ------ | -------------------------------------------------- | -------- |
| Bucket   | String | 被删除生命周期配置的存储桶，格式：BucketName-APPID | 是       |
