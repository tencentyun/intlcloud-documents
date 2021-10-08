
## Overview

This document provides an overview of APIs and SDK code samples related to image styles.

| API | Description |
| :----------------------------------------------------------- | :--------- |
| [Adding a Style](https://intl.cloud.tencent.com/document/product/1045/33708)  | Adds a style to a bucket |
| [Querying Styles](https://intl.cloud.tencent.com/document/product/1045/33707)  | Queries styles set for a bucket  |
| [Deleting a Style](https://intl.cloud.tencent.com/document/product/1045/33709)   | Deletes a style from a bucket |


## Adding a Style

#### API description

This API is used to add a style to a bucket. This style will be added to images newly uploaded to this bucket.

#### Sample code

```php
try {
        $result = $cosClient->PutBucketImageStyle(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'StyleName' => 'style_name',// Style name
        'StyleBody' => 'imageMogr2/thumbnail/!50px', // Style configurations
    ));
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter | Type | Description | Required |
| -------------------- | ----------- | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| StyleName          | String      | Style name | Yes |
| StyleBody          | String      | Style configurations | Yes |


#### Sample response

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [RequestId] => NWQwOGRkNDdfMjJiMjU4NjRfNzVjXzEwNmVjY2M=
            [Bucket] => examplebucket-1250000000
            [Location] => examplebucket-1250000000.pic.ap-beijing.myqcloud.com/
        )
)

```

#### Response description

| Parameter | Type | Description | Parent Node |
| -------------------- | ----------- | ------------------------------------------------- | ------ |
| RequestId             | String      | Request ID                                | None     |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | None |
| Location             | String      | Address of the requested resource                                 | None     |

## Querying Styles

#### API description

This API is used to query the styles set for a bucket.

#### Sample code
```php
try {
        $result = $cosClient->GetBucketImageStyle(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'StyleName' => 'style_name', // Style name
    ));
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter | Type | Description | Required |
| -------------------- | ----------- | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| StyleName       | String      | Style name | No |


#### Sample response

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [RequestId] => NWQwOGRkNDdfMjJiMjU4NjRfNzVjXzEwNmVjY2M=
            [Bucket] => examplebucket-1250000000
            [Location] => examplebucket-1250000000.pic.ap-beijing.myqcloud.com/
            [StyleRule] => Array(
                [0] => Array(
                    [StyleName] => style_name
                    [StyleBody] => imageMogr2/thumbnail/!50px
                )
            )
       )
)

```

#### Response description

| Parameter | Type | Description | Parent Node |
| -------------------- | ----------- | ------------------------------------------------- | ------ |
| RequestId             | String      | Request ID                                | None     |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | None |
| Location             | String      | Address of the requested resource                                 | None     |
| StyleRule             | Array      | A list of styles      | None |

## Deleting a Style

#### API description

This API is used to delete a style from a bucket.

#### Sample code
```php
try {
        $result = $cosClient->DeleteBucketImageStyle(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'StyleName' => 'style_name', // Style name
    ));
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter | Type | Description | Required |
| -------------------- | ----------- | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | Yes |
| StyleName       | String      | Style name     | Yes |


#### Sample response

```php
Guzzle\Service\Resource\Model Object
(
    [structure:protected] => 
    [data:protected] => Array
        (
            [RequestId] => NWQwOGRkNDdfMjJiMjU4NjRfNzVjXzEwNmVjY2M=
            [Bucket] => examplebucket-1250000000
            [Location] => examplebucket-1250000000.pic.ap-beijing.myqcloud.com/
       )
)

```

#### Response description

| Parameter | Type | Description | Parent Node |
| -------------------- | ----------- | ------------------------------------------------- | ------ |
| RequestId             | String      | Request ID                                | None     |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | None |
| Location             | String      | Address of the requested resource                                 | None     |

