
## Overview

This document provides an overview of APIs and SDK code samples related to object tagging.

| API | Operation | Description |
| :----------------------------------------------------------- | :----------- | :--------------------------- |
| [PUT Object tagging](https://intl.cloud.tencent.com/document/product/436/35709) | Tagging an object | Tags an uploaded object. |
| [GET Object tagging](https://intl.cloud.tencent.com/document/product/436/35710) | Querying object tags | Queries all tags of an object. |
| [DELETE Object tagging](https://intl.cloud.tencent.com/document/product/436/35711) | Deleting object tags | Deletes all tags of an object. |

## Tagging an Object

#### Description

This API (PUT Object tagging) is used to tag an object.


#### Method prototype

```
public Guzzle\Service\Resource\Model PutObjectTagging(array $args = array());
```

#### Sample request


```php
try {
    $result = $cosClient->putObjectTagging(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key'    => 'exampleobject',
        'TagSet' => array(
            array('Key'=>'key1',
                  'Value'=>'value1',
            ),  
            array('Key'=>'key2',
                  'Value'=>'value2',
            ),  
        ),  
    ));
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}
```

#### Parameter description

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| Bucket | Bucket of the object to tag in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| Key | Key of the object to tag. An object key uniquely identifies an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String |
| TagSet    | Tags to add to the object                                                     | Array |

`TagSet` member description:

| Parameter | Description | Type |
| ----- | ---- | ---- |
| Key | Tag key | String |
| Value | Tag value | String |

## Querying Object Tags

#### Description

This API (GET Object tagging) is used to query the existing tags of an object.

#### Method prototype

```
public Guzzle\Service\Resource\Model GetObjectTagging(array $args = array());
```

#### Sample request

```php
try {
    $result = $cosClient->getObjectTagging(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key'    => 'exampleobject',
    ));
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| Bucket | Bucket of the object to tag in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| Key | Key of the object to tag. An object key uniquely identifies an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String |



#### Sample response

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

#### Response description

| Member | Description | Type |
| -------- | -------- | ------ |
| Key      | Tag key | String |
| Value    | Tag value | String |

## Deleting Object Tags

#### Description

This API (DELETE Object tagging) is used to delete the existing tags of an object.

#### Method prototype

```
public Guzzle\Service\Resource\Model DeleteObjectTagging(array $args = array());
```

#### Sample request

```php
try {
    $result = $cosClient->deleteObjectTagging(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'Key'    => 'exampleobject',
    );
    // Request successful
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| Bucket | Bucket of the object to tag in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| Key | Key of the object to tag. An object key uniquely identifies an object in a bucket. For more information, see [Object Overview > Object Key](https://intl.cloud.tencent.com/document/product/436/13324) | String |


