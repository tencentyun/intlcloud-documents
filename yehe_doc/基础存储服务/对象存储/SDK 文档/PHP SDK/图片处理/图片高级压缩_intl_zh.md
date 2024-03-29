
## 简介

本文档提供关于图片高级压缩的 API 概览以及 SDK 示例代码。


| API           |  操作描述               |
| :--------------- |  :--------------------- |
| [图片高级压缩](https://intl.cloud.tencent.com/document/product/436/40119)|   图片高级压缩可以更加高效地将图片转换为 TPG 或 HEIF 等高压缩比格式，有效降低图片传输链路及加载耗时，降低带宽及流量成本  |


## 图片高级压缩

#### 功能说明

通过数据万象 imageMogr2 接口提供图片高级压缩功能。


#### 示例代码

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
        $imageMogrTemplate = new Qcloud\Cos\ImageParamTemplate\ImageMogrTemplate();//创建基础图片处理参数模版实例
        $imageMogrTemplate->format('tpg');//将原图转换为 TPG 格式,
        $imageMogrTemplate->format('heif');//将原图转换为 HEIF 格式
        $result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-1250000000', //存储桶名称，由BucketName-Appid 组成，可以在COS控制台查看 https://console.cloud.tencent.com/cos5/bucket
        'Key' => 'exampleobject',
        'ImageHandleParam' => $imageMogrTemplate->queryString(),//生成基础图片处理参数
    ));
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo($e);
}
```

#### 参数说明

| 参数名称             | 类型        | 描述                                                         | 是否必填 |
| -------------------- | ----------- | ------------------------------------------------------------ | -------- |
| Bucket          | String      | 存储桶名称，格式：BucketName-APPID                        | 是       |
| Key             | String      | 此处的 Key 为对象键，对象键是对象在存储桶中的唯一标识。例如，在对象的访问域名`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg` 中，对象键为`doc/pic.jpg` | 是        |
| ImageHandleParam  | String      | 万象图片处理参数，例如：imageMogr2/format/tpg          | 是          |

#### 返回结果示例

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [Body] => 
            [ETag] => "698d51a19d8a121ce581499d7b701668"
            [RequestId] => NWQwOGRkNDdfMjJiMjU4NjRfNzVjXzEwNmVjY2M=
            [ContentLength] => 100
            [ContentType] => image/jpeg
            [Key] => exampleobject
            [Bucket] => examplebucket-1250000000
            [Location] => examplebucket-1250000000.cos.ap-beijing.myqcloud.com/exampleobject
        )

)

```

#### 返回结果说明

| 参数名称             | 类型        | 描述                                          | 父节点  |
| -------------------- | ----------- | ------------------------------------------------- | ------ |
| Body                 | File/String | 下载内容                                     | 无     |
| ETag                 | String      | 文件的 MD5 值                                | 无     |
| ContentLength         | Int         | 响应体长度                                  | 无     |
| ContentType          | String      | 内容类型，设置 Content-Type                     | 无     |
| RequestId             | String      | 请求 ID 标识                                | 无     |
| Key                  | String      | 对象键                                     | 无     |
| Bucket               | String      | 存储桶名称，格式：BucketName-APPID              | 无     |
| Location             | String      | 请求资源地址                                 | 无     |
