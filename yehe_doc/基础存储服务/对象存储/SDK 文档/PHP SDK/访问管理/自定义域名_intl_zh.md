
## 简介

本文档提供关于自定义域名的 API 概览以及 SDK 示例代码。

| API               | 操作名         | 操作描述                   |
| ----------------- | -------------- | -------------------------- |
| PUT Bucket domain | 设置自定义域名 | 设置存储桶的自定义域名信息 |
| GET Bucket domain | 查询自定义域名 | 查询存储桶的自定义域名信息 |

## 设置自定义域名

#### 功能说明

PUT Bucket domain 用于为存储桶配置自定义域名。

#### 方法原型

```
public Guzzle\Service\Resource\Model PutBucketDomain(array $args = array());
```

#### 请求示例

[//]: # (.cssg-snippet-put-bucket-domain)
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
    $result = $cosClient->putBucketDomain(array( 
        'Bucket' => 'examplebucket-1250000000', //存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket 
        'DomainRules' => array( 
            array( 
                'Name' => 'www.qq.com', 
                'Status' => 'ENABLED', 
                'Type' => 'REST', 
                'ForcedReplacement' => 'CNAME', 
            ),  
            // ... repeated 
        ),  
    )); 
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo($e);
}
```

#### 参数说明

| 参数名称          | 描述                                                         | 类型   |
| ----------------- | ------------------------------------------------------------ | ------ |
| Bucket            | 设置自定义域名的存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| Name              | 自定义域名                                                   | String |
| Status            | 域名上线状态，可选值有 ENABLED、DISABLED                     | String |
| Type              | 绑定的源站类型，可选值有 REST、WEBSITE                       | String |
| ForcedReplacement | 强制覆盖已存在的配置，可选值有 CNAME、TXT                    | String |

#### 返回错误码说明

该请求可能会发生的一些常见的特殊错误如下：

| 状态码                                 | 说明                                                         |
| -------------------------------------- | ------------------------------------------------------------ |
| HTTP 409 Conflict                      | 该域名记录已存在，且请求中没有设置强制覆盖。或者该域名记录不存在，且请求中设置了强制覆盖 |
| HTTP 451 Unavailable For Legal Reasons | 该域名是中国境内域名，并且没有备案                           |

## 查询自定义域名

#### 功能说明

GET Bucket domain 用于查询存储桶的自定义域名信息。

#### 方法原型

```
public Guzzle\Service\Resource\Model GetBucketDomain(array $args = array());
```

#### 请求示例

[//]: # (.cssg-snippet-get-bucket-domain)
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
    $result = $cosClient->getBucketDomain(array( 
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

| 参数名称 | 描述                                                         | 类型   |
| -------- | ------------------------------------------------------------ | ------ |
| Bucket   | 查询自定义域名的存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### 返回结果示例

```php
GuzzleHttp\Command\Result Object
(
    [DomainRules] => Array
        (
            [0] => Array
                (
                    [Status] => ENABLED
                    [Name] => www.qq.com
                    [Type] => REST
                )

        )
    [DomainTxtVerification] => tencent-cloud-cos-verification=9d2258433b1f38c7dd4b29fe272d2128
)
```

#### 返回结果说明

| 参数名称              | 描述                                                         | 类型   |
| --------------------- | ------------------------------------------------------------ | ------ |
| Name                  | 自定义域名                                                   | String |
| Status                | 域名上线状态，可选值有 ENABLED、DISABLED                     | String |
| Type                  | 绑定的源站类型，可选值有 REST、WEBSITE                       | String |
| ForcedReplacement     | 强制覆盖已存在的配置，可选值有 CNAME、TXT                    | String |
| DomainTXTVerification | 域名校验信息，该字段是一个 MD5 校验值，原串格式为：<br>`cos[Region][BucketName-APPID][BucketCreateTime]`，其中 Region 为存储桶所在地域，BucketCreateTime 为存储桶 GMT 创建时间 | String |
