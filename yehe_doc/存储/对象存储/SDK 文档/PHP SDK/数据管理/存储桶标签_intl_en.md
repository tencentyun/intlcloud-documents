

This document provides an overview of APIs and SDK code samples related to bucket tagging.

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8281) | Setting a bucket tag | Sets a tag for an existing bucket |
| [GET Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8277) | Querying bucket tags | Queries the existing tags of a specified bucket |
| [DELETE Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8286) | Deleting a bucket tag | Deletes a specified bucket tag |

## Setting Bucket Tag

#### Feature description

This API (PUT Bucket tagging) is used to set a tag for an existing bucket.

#### Method prototype

```
public Guzzle\Service\Resource\Model PutBucketTagging(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket-tagging)
```php
try {
    $result = $cosClient->putBucketTagging(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'TagSet' => array(
            array('Key'=>'key1',
                  'Value'=>'value1',
            ),  
            array('Key'=>'key2',
                  'Value'=>'value2',
            ),  
        ),  
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}
```

#### Parameter description

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| Bucket | Bucket for which to set a tag in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| Key      | Tag key                                                     | String |
| Value    | Tag value                                                     | String |

## Querying Bucket Tag

#### Feature description

This API (GET Bucket tagging) is used to query the existing tags of a specified bucket.

#### Method prototype

```
public Guzzle\Service\Resource\Model GetBucketTagging(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-get-bucket-tagging)
```php
try {
    $result = $cosClient->getBucketTagging(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| Bucket | Bucket for which to query a tag in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### Sample return result

```php
GuzzleHttp\Command\Result Object
(
    [TagSet] => Array
        (
            [0] => Array
                (
                    [Key] => key1
                    [Value] => value1
                )

            [1] => Array
                (
                    [Key] => key2
                    [Value] => value2
                )

        )
    [RequestId] => NWRmMWVkMjFfMjJiMjU4NjRfNWQ3X2EwMWVj****
)
```

#### Returned result description

| Member Variable | Description | Type |
| -------- | -------- | ------ |
| Key      | Tag key | String |
| Value    | Tag value                                                     | String |

## Deleting Bucket Tag

#### Feature description

This API (DELETE Bucket tagging) is used to delete an existing tag of a specified bucket.

#### Method prototype

```
public Guzzle\Service\Resource\Model DeleteBucketTagging(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-delete-bucket-tagging)
```php
try {
    $result = $cosClient->deleteBucketTagging(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
    );
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| Bucket | Bucket for which to delete a tag in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |

