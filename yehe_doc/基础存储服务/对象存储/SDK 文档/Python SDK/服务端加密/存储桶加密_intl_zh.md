## 简介
本文档提供存储桶加密的 API 概览和 SDK 示例代码。

| API                                                          | 操作名         | 操作描述                       |
| ------------------------------------------------------------ | -------------- | ------------------------------ |
| [PUT Bucket encryption](https://intl.cloud.tencent.com/document/product/436/33459) | 设置存储桶加密 | 设置指定存储桶下的默认加密配置 |
| [GET Bucket encryption](https://intl.cloud.tencent.com/document/product/436/33460) | 查询存储桶加密 | 查询指定存储桶下的默认加密配置 |
| [DELETE Bucket encryption](https://intl.cloud.tencent.com/document/product/436/33461) | 删除存储桶加密 | 删除指定存储桶下的默认加密配置 |

## 设置存储桶加密

#### 功能说明

用于设置指定存储桶下的默认服务端加密配置。如需执行此接口，必须拥有 PutBucketEncryption 权限。默认情况下，Bucket 的持有者直接拥有权限使用该 API 接口，Bucket 持有者也可以将权限授予其他用户。

#### 方法原型

```
put_bucket_encryption(Bucket, ServerSideEncryptionConfiguration={}, **kwargs)
```

#### 请求示例

[//]: # ".cssg-snippet-put-bucket-sse"
```python
config_dict = {
    'Rule': [
        {
            'ApplySideEncryptionConfiguration': {
                'SSEAlgorithm': 'AES256',
            }
        },
    ]
}
client.put_bucket_encryption(Bucket='examplebucket-1250000000', ServerSideEncryptionConfiguration=config_dict)
```

#### 参数说明

| 参数名称   | 参数描述   |类型 | 是否必填 |
| -------------- | -------------- |---------- | ----------- |
|Bucket|存储桶名称，由 BucketName-APPID 构成|String|是|
|ServerSideEncryptionConfiguration|服务端加密配置 |Dict| 是|

ServerSideEncryptionConfiguration 说明：

| 参数名         | 参数描述                                         | 类型    | 是否必填 |
| -------------- | ----------------------------------------------- | ------ | ---- |
|Rule|服务端加密规则列表，目前只支持一个规则|List|是 |
|ApplySideEncryptionConfiguration|具体的服务加密配置描述|Dict|是 |
|SSEAlgorithm| 服务端加密算法，目前桶加密只支持 SSE-COS 类型，使用 AES256 加密算法|String|是 |

#### 返回结果说明

该方法返回值为 None。

## 查询存储桶加密

#### 功能说明

用于查询指定存储桶下的默认服务端加密配置。如需执行此接口，必须拥有 GetBucketEncryption 权限。默认情况下，Bucket 的持有者直接拥有权限使用该 API 接口，Bucket 持有者也可以将权限授予其他用户。

#### 方法原型

```
get_bucket_encryption(Bucket, **kwargs)
```
#### 请求示例

[//]: # ".cssg-snippet-get-bucket-sse"
```python
response = client.get_bucket_encryption(Bucket='examplebucket-1250000000')
sse_algorithm = response['Rule'][0]['ApplyServerSideEncryptionByDefault']['SSEAlgorithm']
```

#### 参数说明

| 参数名称   | 参数描述   |类型 | 是否必填 |
| -------------- | -------------- |---------- | ----------- |
|Bucket|存储桶名称，由 BucketName-APPID 构成|String|是|

#### 返回结果说明

| 参数名称   | 参数描述   |类型 | 是否必填 |
| -------------- | -------------- |---------- | ----------- |
|ServerSideEncryptionConfiguration|服务端加密配置 |Dict| 是|

ServerSideEncryptionConfiguration 说明：

| 参数名         | 参数描述                                         | 类型    | 是否必填 |
| -------------- | ----------------------------------------------- | ------ | ---- |
|Rule|服务端加密规则列表，目前只支持一个规则|List|是 |
|ApplySideEncryptionConfiguration|具体的服务加密配置描述|Dict|是 |
|SSEAlgorithm| 服务端加密算法，目前桶加密只支持 SSE-COS 类型，使用 AES256 加密算法|String|是 |

## 删除存储桶加密

#### 功能说明

用于删除指定存储桶下的默认加密配置。如需执行此接口，必须拥有 DeleteBucketEncryption 权限。默认情况下，Bucket 的持有者直接拥有权限使用该 API 接口，Bucket 持有者也可以将权限授予其他用户。

#### 方法原型

```
delete_bucket_encryption(Bucket, **kwargs)
```
#### 请求示例

[//]: # ".cssg-snippet-del-bucket-sse"
```python
response = client.delete_bucket_encryption(Bucket='examplebucket-1250000000')
```

#### 参数说明

| 参数名称   | 参数描述   |类型 | 是否必填 |
| -------------- | -------------- |---------- | ----------- |
|Bucket|存储桶名称，由 BucketName-APPID 构成|String|是|

#### 返回结果说明

该方法返回值为 None。
