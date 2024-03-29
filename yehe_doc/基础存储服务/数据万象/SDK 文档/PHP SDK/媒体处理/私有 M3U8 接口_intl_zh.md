## 简介

本文档提供关于私有 M3U8 接口的 API 概览和 SDK 示例代码。

| API           | 操作描述                 |
| ------------- |  ---------------------- |
| GetPrivateM3U8 | 用于获取私有 M3U8 ts 资源的下载授权。（此方式通过对象存储转发请求至数据万象）。 |


## GetPrivateM3U8

#### 功能说明

用于获取私有 M3U8 ts 资源的下载授权。（此方式通过对象存储转发请求至数据万象）。

#### 方法原型

```php
public Guzzle\Service\Resource\Model getPrivateM3U8(array $args = array());
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
    $result = $cosClient->GetPrivateM3U8(array(
        'Bucket' => 'examplebucket-1250000000', //存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'xxx.m3u8', // 桶文件
        'ci-process' => 'pm3u8', // 操作类型，固定使用 pm3u8
        'expires' => '3600', // 私有 ts 资源 url 下载凭证的相对有效期，单位为秒，范围为[3600, 43200]
    ));
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo($e);
}
```

#### 参数说明

Request 中的具体数据描述如下：

| 参数名称   | 描述                                                         | 类型   | 是否必选 |
| :--------- | :----------------------------------------------------------- | :----- | :------- |
| ci-process | 操作类型，固定使用 pm3u8                                     | String | 是       |
| expires    | 私有 ts 资源 url 下载凭证的相对有效期，单位为秒，范围为[3600, 43200] | String | 是       |

#### 返回结果示例

```php
 GuzzleHttp\Command\Result Object
(
    [Body] => GuzzleHttp\Psr7\Stream Object
        (
            [stream:GuzzleHttp\Psr7\Stream:private] => Resource id #89
            [size:GuzzleHttp\Psr7\Stream:private] => 
            [seekable:GuzzleHttp\Psr7\Stream:private] => 1
            [readable:GuzzleHttp\Psr7\Stream:private] => 1
            [writable:GuzzleHttp\Psr7\Stream:private] => 1
            [uri:GuzzleHttp\Psr7\Stream:private] => php://temp
            [customMetadata:GuzzleHttp\Psr7\Stream:private] => Array
                (
                )

        )

    [RequestId] => NjI2MTFjYSDHIUsdsdSJDOIDTRfMjVjYzcw
    [ContentType] => application/x-mpegURL
    [ContentLength] => 4310
    [Key] => xxx.m3u8
    [Bucket] => examplebucket-1250000000
    [Location] => examplebucket-1250000000.cos.ap-beijing.myqcloud.com/xxx.m3u8
    [Data] => m3u8文件内容
)
```
