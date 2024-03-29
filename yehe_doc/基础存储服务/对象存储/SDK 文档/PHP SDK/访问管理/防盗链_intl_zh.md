## 简介

本文档提供关于存储桶 Referer 白名单或者黑名单的 API 概览以及 SDK 示例代码。
>! 需要 COS PHP SDK v2.3.2 及以上版本。旧版本可能存在 bug，使用时建议升级到 [最新版本](https://github.com/tencentyun/cos-php-sdk-v5/releases/)。
>

| API                                                          | 操作名         | 操作描述                   |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket referer](https://intl.cloud.tencent.com/document/product/436/31423) | 设置存储桶 Referer | 设置存储桶 Referer 白名单或者黑名单 |
| [GET Bucket referer](https://intl.cloud.tencent.com/document/product/436/30615) | 查询存储桶 Referer | 查询存储桶 Referer 白名单或者黑名单 |

### 设置存储桶 Referer

#### 功能说明

设置存储桶 Referer 白名单或者黑名单（PUT Bucket referer）。

#### 方法原型

```php
public Guzzle\Service\Resource\Model putBucketReferer(array $args = array());
```

#### 请求示例

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
    $result = $cosClient->putBucketReplication(array(
            'Bucket' => 'examplebucket-1250000000', //存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
            'Status' => 'Enabled', //是否开启防盗链，枚举值：Enabled、Disabled
            'RefererType' => 'White-List', //防盗链类型，枚举值：Black-List、White-List
            'DomainList' => array(
                'Domains' => array(
                     '*.qq.com', //单条生效域名
                     '*.qcloud.com', //单条生效域名
                )
            ), //生效域名列表
            'EmptyReferConfiguration' => 'Allow', //是否允许空 Referer 访问，枚举值：Allow、Deny，默认值为 Deny
        ),      
    ); 
    // 请求成功    
    print_r($result);
} catch (\Exception $e) {   
    // 请求失败
    echo($e);
}
```
#### 参数说明

| 参数名  | 参数描述                                                     | 类型    | 是否必填 |
| ------- | ------------------------------------------------------------ | ------- | ---- |
| Bucket  | 存储桶的名称，命名规则为 BucketName-APPID，此处填写的存储桶名称必须为此格式 | String  | 是   |
| Status     | 是否开启防盗链，枚举值：Enabled、Disabled | String  | 是   |
| RefererType | 防盗链类型，枚举值：Black-List、White-List| String |是   |
| DomainList | 生效域名列表 | Array |是   |
| EmptyReferConfiguration | 是否允许空 Referer 访问，枚举值：Allow、Deny，默认值为 Deny| String |否   |

### 查询存储桶 Referer

#### 功能说明

查询存储桶 Referer 白名单或者黑名单（GET Bucket referer）。

#### 方法原型

```php
public Guzzle\Service\Resource\Model getBucketReferer(array $args = array());
```

#### 请求示例

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
    $result = $cosClient->getBucketReferer(array(
        'Bucket' => 'examplebucket-1250000000', //存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
    )); 
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo($e);
}
```

#### 参数说明

| 参数名  | 参数描述                                                     | 类型    | 是否必填 |
| ------- | ------------------------------------------------------------ | ------- | ---- |
| Bucket  | 存储桶的名称，命名规则为 BucketName-APPID，此处填写的存储桶名称必须为此格式 | String  | 是   |

#### 返回结果示例
```php
GuzzleHttp\Command\Result Object
(
    [RequestId] => NjE0NTk2ZWVfZmQzNDJjMGJfMWNiNmVfN2Y1MWQx
    [ContentType] => application/xml
    [ContentLength] => 260
    [Status] => Enabled
    [RefererType] => White-List
    [EmptyReferConfiguration] => Allow
    [DomainList] => Array
        (
            [Domain] => Array
                (
                    [0] => *.qq.com
                    [1] => *.qcloud.com
                )

        )

    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/
)
```
