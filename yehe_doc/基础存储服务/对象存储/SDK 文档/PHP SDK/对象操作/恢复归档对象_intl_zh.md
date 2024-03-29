## 简介

本文档提供关于恢复归档对象操作相关的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名         | 操作描述                                  |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | 恢复归档对象 | 将归档类型的对象取回访问                      |

## 恢复归档对象 

#### 功能说明

将归档类型的对象取回访问（POST Object restore）。

#### 方法原型

```php
public Guzzle\Service\Resource\Model restoreObject(array $args = array());
```

#### 请求示例

[//]: # (.cssg-snippet-restore-object)

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
    $result = $cosClient->restoreObject(array(
        'Bucket' => 'examplebucket-1250000000', //存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
        'Days' => 10,
        'CASJobParameters' => array(
            'Tier' =>'Expedited'
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

| 参数名称         | 类型   | 描述                                                         | 是否必填 |
| ---------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket           | String | 存储桶名称，格式：BucketName-APPID                           | 是       |
| Key              | String | 对象键                                                       | 是       |
| Days             | String | 设置临时副本的过期时间，单位(天)                             | 是       |
| CASJobParameters | Array  | 恢复信息                                                     | 是       |
| Tier             | String | 恢复归档存储类型的数据时，Tier 可以指定为 COS 支持的三种恢复模式，分别为 Expedited、Standard、Bulk。恢复深度归档存储类型的数据时，Tier 可以指定为 COS 支持的两种恢复模式，分别为 Standard、Bulk。 | 是       |
