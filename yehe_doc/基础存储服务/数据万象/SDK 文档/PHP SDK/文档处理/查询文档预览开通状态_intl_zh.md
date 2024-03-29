## 简介

本文档提供关于查询文档预览开通状态的 API 概览和 SDK 示例代码。

| API                                                          | 操作描述                              |
| ------------------------------------------------------------ | ------------------------------------- |
| [查询文档预览开通状态](https://intl.cloud.tencent.com/document/product/436/46919) | 用于查询已经开通文档预览功能的 Bucket |


## 查询文档预览开通状态

#### 功能说明

用于查询已经开通文档预览功能的 Bucket。

#### 方法原型

```php
public Guzzle\Service\Resource\Model describeDocProcessBuckets(array $args = array());
```

#### 请求示例

```php
<?php

require dirname(__FILE__, 2) . '/vendor/autoload.php';

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
    // 查询文档预览开通状态 https://cloud.tencent.com/document/product/460/46945
    $result = $cosClient->describeDocProcessBuckets(array(
        'Regions' => '', // 可选 地域信息，例如 ap-shanghai、ap-beijing，若查询多个地域以“,”分隔字符串
        'BucketNames' => '', // 可选 存储桶名称，以“,”分隔，支持多个存储桶，精确搜索
        'BucketName' => '', // 可选 存储桶名称前缀，前缀搜索
        'PageNumber' => 1, // 可选 第几页
        'PageSize' => 20, // 可选 每页个数
    ));
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo($e);
}
```

#### 参数说明

| 名称        | 描述                                                         | 类型   | 是否必选 |
| :---------- | :----------------------------------------------------------- | :----- | :------- |
| Regions     | 地域信息，以“,”分隔字符串，支持 All、ap-shanghai、ap-beijing | string | 否       |
| BucketNames | 存储桶名称，以“,”分隔，支持多个存储桶，精确搜索              | string | 否       |
| BucketName  | 存储桶名称前缀，前缀搜索                                     | string | 否       |
| PageNumber  | 第几页                                                       | string | 否       |
| PageSize    | 每页个数                                                     | string | 否       |

#### 返回结果示例

```php
GuzzleHttp\Command\Result Object
(
    [RequestId] => NjMxMDcwZDlfAHDKAJHSDKJASHDKY3
    [ContentType] => application/xml
    [ContentLength] => 4600
    [TotalCount] => 59
    [PageNumber] => 1
    [PageSize] => 3
    [DocBucketList] => Array
        (
            [0] => Array
                (
                    [BucketId] => xxx-123
                    [Name] => xxx-123
                    [Region] => ap-chongqing
                    [CreateTime] => 2022-08-30T10:41:31+0800
                    [AliasBucketId] => 
                )

            [1] => Array
                (
                    [BucketId] => xxx-123
                    [Name] => xxx-123
                    [Region] => ap-chongqing
                    [CreateTime] => 2022-08-30T10:41:31+0800
                    [AliasBucketId] => 
                )

            [2] => Array
                (
                    [BucketId] => xxx-123
                    [Name] => xxx-123
                    [Region] => ap-chongqing
                    [CreateTime] => 2022-08-30T10:41:31+0800
                    [AliasBucketId] => 
                )

        )

    [Location] => ci.ap-guangzhou.myqcloud.com/docbucket
)
```



