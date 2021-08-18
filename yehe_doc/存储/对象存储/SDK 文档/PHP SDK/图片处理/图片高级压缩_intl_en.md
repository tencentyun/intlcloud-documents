
## Overview

This document provides an overview of APIs and SDK code samples related to advanced image compression.


| API | Description |
| :--------------- |  :--------------------- |
| [Advanced Image Compression](https://intl.cloud.tencent.com/document/product/436/40119) | Advanced image compression allows you to easily convert images into formats that provide a high compression ratio, such as TPG and HEIF. This effectively reduces the transmission time, loading time, and the use of bandwidth and traffic. |


## Advanced Image Compression

#### Feature description

COS uses the `imageMogr2` API of Cloud Infinite (CI) to provide advanced image compression.


#### Sample code

```php
try {
        $imageMogrTemplate = new Qcloud\Cos\ImageParamTemplate\ImageMogrTemplate(); //Create an instance of the basic image processing parameter template
        $imageMogrTemplate->format('tpg'); //Convert the original image into the TPG format
        $imageMogrTemplate->format('heif'); //Convert the original image into the HEIF format
        $result = $cosClient->getObject(array(
        'Bucket' => 'examplebucket-1250000000', //Format: BucketName-APPID
        'Key' => 'exampleobject',
        'ImageHandleParam' => $imageMogrTemplate->queryString(), //Generate basic image processing parameters
    ));
    // Request succeeded
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
| Key | String | Uniquely identifies an object in a bucket. For example, if the object access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg`.  | Yes |
| ImageHandleParam  | String      | CI image processing parameter, for example, imageMogr2/format/tpg          | Yes          |

#### Response sample

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

#### Response description

| Parameter | Type | Description | Parent Node |
| -------------------- | ----------- | ------------------------------------------------- | ------ |
| Body | File/String | Downloaded content                                                   | None |
| ETag | String | MD5 checksum of the file | None |
| ContentLength | Int | Length of the response body | None |
| ContentType | String | Content type. Sets `Content-Type` | None |
| RequestId             | String      | Request ID                                | None     |
| Key                  | String      | Object key                                    | None     |
| Bucket | String | Bucket name in the format of `BucketName-APPID` | None |
| Location             | String      | Address of the requested resource                                 | None     |
