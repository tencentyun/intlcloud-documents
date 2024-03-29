## 简介

本文档提供快捷查询某个存储桶是否存在的示例代码。

示例代码实际调用了COS API [HeadBucket](https://intl.cloud.tencent.com/document/product/436/7735)，是该接口的简化版。

HeadBucket除了检查存储桶是否存在，还可以判断是否有权限访问存储桶，有以下几种情况：

- 存储桶存在且有读取权限，返回 HTTP 状态码为200。
- 无存储桶读取权限，返回 HTTP 状态码为403。
- 存储桶不存在，返回 HTTP 状态码为404。


## 检查存储桶是否存在

#### 功能说明

检查存储桶是否存在。

#### 方法原型

```php
public Guzzle\Service\Resource\Model doesBucketExist(array $args = array());
```

#### 示例代码

[//]: # ".cssg-snippet-object-exist"

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
    $result = $cosClient->doesBucketExist(
        'examplebucket-125000000'//存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
    ); ;
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo($e);
}
```
