

本文档提供关于日志管理的 API 概览以及 SDK 示例代码。

| API                                                          | 操作名       | 操作描述                   |
| ------------------------------------------------------------ | ------------ | -------------------------- |
| [PUT Bucket logging](https://intl.cloud.tencent.com/document/product/436/17054) | 设置日志管理 | 为源存储桶开启日志记录     |
| [GET Bucket logging](https://intl.cloud.tencent.com/document/product/436/17053) | 查询日志管理 | 查询源存储桶的日志配置信息 |

## 设置日志管理

#### 功能说明

PUT Bucket logging 用于为源存储桶开启日志记录，将源存储桶的访问日志保存到指定的目标存储桶中。

#### 方法原型

```
public Guzzle\Service\Resource\Model PutBucketLogging(array $args = array());
```

#### 请求示例

```php
try {
    $result = $cosClient->putBucketLogging(array(
        'Bucket' => 'examplebucket-1250000000', //格式：BucketName-APPID
        'LoggingEnabled' => array(
            'TargetBucket' => 'examplebucket2-1250000000',
            'TargetPrefix' => '', 
        )); 
    // 请求成功
    print_r($result);
} catch (\Exception $e) {
    // 请求失败
    echo($e);
}
```

#### 参数说明

| 参数名称     | 描述                                                         | 类型   |
| ------------ | ------------------------------------------------------------ | ------ |
| Bucket       | 开启日志功能的源存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| TargetBucket | 存放日志的目标存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| TargetPrefix | 日志存放在目标存储桶的指定路径  | String

## 查询日志管理

#### 功能说明

GET Bucket logging 用于查询指定存储桶的日志配置信息。

#### 方法原型

```
public Guzzle\Service\Resource\Model GetBucketLogging(array $args = array());
```

#### 请求示例

```php
try {
    $result = $cosClient->getBucketLogging(array(
        'Bucket' => 'examplebucket-1250000000', //格式：BucketName-APPID
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
| Bucket   | 源存储桶，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### 返回结果示例

```php
GuzzleHttp\Command\Result Object
(
    [LoggingEnabled] => Array
        (
            [TargetBucket] => examplebucket2-1250000000
            [TargetPrefix] => 
        )

    [RequestId] => NWRmMWJjOThfMjZiMjU4NjRfODY4X2ExMjcy****
)
```

#### 返回结果说明

| 成员变量     | 描述                     | 类型   |
| ------------ | ------------------------ | ------ |
| TargetBucket | 日志存放的目标存储桶     | String |
| TargetPrefix | 日志存放的目标存储桶路径 | String |
