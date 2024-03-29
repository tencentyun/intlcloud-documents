## 简介

本文档提供快捷查询存储桶中某个对象是否存在的示例代码。

示例代码实际调用了 COS API [HeadObject](https://intl.cloud.tencent.com/document/product/436/7745)，是该接口的简化版。

HeadObject 除了检查对象是否存在，主要功能为返回对象元数据。包含了 HeadObject 完整功能的 SDK 接口，可参见 [查询对象元数据](https://intl.cloud.tencent.com/document/product/436/37688)。


## 查询对象元数据

#### 功能说明

检查存储桶中是否存在某个对象。

#### 方法原型

```php
public Guzzle\Service\Resource\Model doesObjectExist(array $args = array());
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
    $result = $cosClient->doesObjectExist(
        'examplebucket-125000000', //存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
        'exampleobject' //对象名
    );
    // 请求成功
    print_r($result);//返回布尔值
} catch (\Exception $e) {
    // 请求失败
    echo($e);
}
```

