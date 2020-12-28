## Overview


This document provides an overview of APIs and SDK code samples related to basic bucket operations.

| API | Operation |  Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service (List Buckets)](https://intl.cloud.tencent.com/document/product/436/8291) | Querying bucket list | Queries the list of all buckets under a specified account |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | Creating a bucket | Creates a bucket under a specified account |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | Checking a bucket and its permissions | Checks whether a bucket exists and you have access permission for it |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket under a specified account |



## Querying Bucket List

#### Feature description

This API (GET Service (List Buckets)) is used to query the list of all buckets under a specified account.

#### Method prototype

```java
public Guzzle\Service\Resource\Model listBucket(array $args = array())
```

#### Sample request

[//]: # (.cssg-snippet-get-service)

```java
try {
    // Request succeeded
    $result = $cosClient->listBuckets();
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Sample response

```java
Array
(
    [data:protected] => Array
        (
            [Owner] => Array
                (
                    [ID] => qcs::cam::uin/100000000001:uin/100000000001
                    [DisplayName] => 100000000001
                )

            [Buckets] => Array
                (
                    [0] => Array
                        (
                            [Name] => examplebucket-1250000000
                            [Location] => ap-beijing
                            [CreationDate] => 2016-07-29T03:09:54Z
                        )

                    [1] => Array
                        (
                            [Name] => examplebucket2-1250000000
                            [Location] => ap-beijing
                            [CreationDate] => 2017-08-02T04:00:24Z
                        )

                )

            [RequestId] => NWE3YzgxZmFfYWZhYzM1MGFfMzc3MF9iOGY5OQ==
        )

)
```

#### Response description

| Parameter Name | Parent Node | Description | Type |
| ------------ | ------- | ---------------------- | ------ |
| Owner        | None      | Bucket owner information       | Array  |
| ID           | Owner   | Bucket owner ID      | String |
| DisplayName  | Owner   | Bucket owner name | String |
| Buckets      | None      | Bucket list             | Array  |
| Bucket       | Buckets | Bucket information             | Array  |
| Name         | Bucket  | Bucket name             | String |
| Location     | Bucket  | Bucket region name     | String |
| CreationDate | Bucket  | Bucket creation time       | String |

## Creating Bucket

#### Feature description

This API (PUT Bucket) is used to create a bucket under a specified account.

#### Method prototype

```java
public Guzzle\Service\Resource\Model createBucket(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket)

```java
try {
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
    $result = $cosClient->createBucket(array('Bucket' => $bucket));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Parent Node | Description | Type |
| -------- | ------ | ---------------------------------- | ------ |
| Bucket   | None     | Bucket name in the format of `BucketName-APPID` | String |

## Checking Bucket and Its Permission

#### Feature description

This API (HEAD Bucket) is used to check whether a bucket exists and you have permission to access it.

#### Method prototype

```java
public Guzzle\Service\Resource\Model headBucket(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-head-bucket)

```java
try {
    $result = $cosClient->headBucket(array(
        'Bucket' => 'examplebucket-1250000000' // Format: BucketName-APPID
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Parent Node | Description | Type |
| -------- | ------ | ---------------------------------- | ------ |
| Bucket   | None     | Bucket name in the format of `BucketName-APPID` | String |

## Deleting Bucket

#### Feature description

This API (DELETE Bucket) is used to delete an empty bucket under a specified account.

#### Method prototype

```java
public Guzzle\Service\Resource\Model deleteBucket(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-delete-bucket)

```java 
try {
    $result = $cosClient->deleteBucket(array(
        'Bucket' => 'examplebucket-1250000000' // Format: BucketName-APPID
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Parent Node | Description | Type |
| -------- | ------ | ---------------------------------- | ------ |
| Bucket   | None     | Bucket name in the format of `BucketName-APPID` | String |

