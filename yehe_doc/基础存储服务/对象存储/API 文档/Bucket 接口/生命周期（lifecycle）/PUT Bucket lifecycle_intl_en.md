## Feature Description

COS introduces the lifecycle feature for you to manage the lifecycle of objects in buckets. The lifecycle configuration contains one or more rules that apply to a set of objects. Each rule defines one operation.
There are two types of operations:

- **Transition**: defines when an object is transitioned to another storage class. For example, you can transition an object to STANDARD_IA (suitable for infrequently accessed objects) 30 days after its creation. You can also transition the object to INTELLIGENT TIERING (suitable for objects with irregular access patterns) or ARCHIVE (offering lower costs). For specific parameters, please see `Transition` in the sample request description.
- **Expiration**: specifies when an object shall expire. COS will automatically delete expired objects.


<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer (recommended)
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=PutBucketLifecycle&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                Tencent Cloud API Explorer makes it easy for you to make online API calls, verify signatures, generate SDK code, and search for APIs. You can use it to query the request and response of each API call and generate sample SDK codes for the call.
            </div>
        </div>
    </div>
</div>

#### Notes

This API (`PUT Bucket lifecycle`) is used to create a lifecycle configuration for a bucket.

> !
> - If a lifecycle configuration has already been set for the bucket, the new configuration created with this API will overwrite the existing one.
> - `Days` and `Date` cannot be both specified in the same lifecycle rule. Please pass them to two separate rules. For details, please see the following [Sample](#.E5.AE.9E.E9.99.85.E6.A1.88.E4.BE.8B).
> - Objects in buckets with [MAZ configuration](https://intl.cloud.tencent.com/document/product/436/35208) enabled cannot be transitioned to an OAZ bucket.
> - Up to 1,000 lifecycle rules can be added for each bucket.

## Requests

#### Request example

```plaintext
PUT /?lifecycle HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Content-Length: length
Date: GMT Date
Authorization: Auth String 
Content-MD5: MD5
```

>? 
> - Host: <BucketName-APPID>.cos.<Region>.myqcloud.com, where <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://www.tencentcloud.com/document/product/436/6224)).
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> 

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).


#### Request body

Nodes of the request body for this API are as follows:

```shell
<LifecycleConfiguration>
    <Rule>
        <ID></ID>
        <Filter>
            <And>
                <Prefix></Prefix>
                <Tag>
                    <Key></Key>
                    <Value></Value>
                </Tag>
            </And>
        </Filter>
        <Status></Status>
        <Transition>
            <Days></Days>
            <StorageClass></StorageClass>
        </Transition>
        <NoncurrentVersionExpiration>
            <NoncurrentDays></NoncurrentDays>
        </NoncurrentVersionExpiration>
    </Rule>
    <Rule>
        <ID></ID>
        <Filter>
            <Prefix></Prefix>
        </Filter>
        <Status></Status>
        <Transition>
            <Days></Days>
            <StorageClass></StorageClass>
        </Transition>
        <NoncurrentVersionTransition>
            <NoncurrentDays></NoncurrentDays>
            <StorageClass></StorageClass>
        </NoncurrentVersionTransition>
    </Rule>
    <Rule>
        <ID></ID>
        <Filter>
            <Prefix></Prefix>
        </Filter>
        <Status></Status>
        <Expiration>
            <ExpiredObjectDeleteMarker></ExpiredObjectDeleteMarker>
        </Expiration>
        <NoncurrentVersionExpiration>
            <NoncurrentDays></NoncurrentDays>
        </NoncurrentVersionExpiration>
        <AbortIncompleteMultipartUpload>
            <DaysAfterInitiation></DaysAfterInitiation>
        </AbortIncompleteMultipartUpload>
    </Rule>
</LifecycleConfiguration>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | --------- | -------- |
| LifecycleConfiguration | None | Lifecycle configuration | Container | Yes |
| Rule | LifecycleConfiguration | Rule description | Container | Yes |
| ID | LifecycleConfiguration.Rule | A unique identifier for the rule. It can be up to 255 characters. | String | No |
| Filter | LifecycleConfiguration.Rule | Identifies objects that a lifecycle rule applies to. | Container | Yes |
| And | LifecycleConfiguration.Rule<br>.Filter | A subset of the object filter. This element is only required when there are more than one filter criteria (for example, filtering with `Prefix` and `Tag` at the same time, or with more than one `Tag`). | Container | No |
| Prefix | LifecycleConfiguration.Rule<br>.Filter.And | Matching prefix for the rule. It specifies objects that the lifecycle rule applies to. There can be one `Prefix` at most. | String | No |
| Tag | LifecycleConfiguration.Rule<br>.Filter.And | A set of tags. Up to 10 tags are supported. | Container | No |
| Key | LifecycleConfiguration.Rule<br>.Filter.And.Tag | Key of the tag. It can be up to 128 bytes. Letters, digits, spaces, plus signs (+), minus signs (-), underscores (_), equal signs (=), dots (.), colons (:), and slashes (/) are supported. | String | No |
|  Value  |    LifecycleConfiguration.Rule<br>.Filter.And.Tag | Value of the tag. It can be up to 256 bytes. Letters, digits, spaces, plus signs (+), minus signs (-), underscores (_), equal signs (=), dots (.), colons (:), and slashes (/) are supported. | String | No |
| Status | LifecycleConfiguration.Rule | Indicates whether the rule is enabled. Enumerated values: `Enabled`, `Disabled` | String | Yes |
| Expiration | LifecycleConfiguration.Rule | Expiration attributes of the rule | Container | No |
| Transition | LifecycleConfiguration.Rule    | Specifies when to transition the object and the target storage class. | Container | No  |
| Days | LifecycleConfiguration.Rule<br>.Transition or Expiration | Specifies the number of days between the date an object was last modified and the date when the operation corresponding to the rule is performed. <br><li>If it is a `Transition` operation, this value should be a non-negative integer. <br><li>If it is an `Expiration` operation, this value should be a positive integer. The maximum value is 3650 (days). | Integer | No |
| ExpiredObjectDeleteMarker | LifecycleConfiguration.Rule<br>.Expiration | Indicates whether the delete marker of an expired object will be removed. Enumerated values: `true`, `false` | String | No |
| AbortIncompleteMultipartUpload | LifecycleConfiguration.Rule | Specifies the time to abort the multipart upload. | Container | No |
| DaysAfterInitiation | LifecycleConfiguration.Rule<br>.AbortIncompleteMultipartUpload | Specifies the number of days within which the multipart upload must be completed after it starts. | Integer | Yes |
| NoncurrentVersionExpiration | LifecycleConfiguration.Rule | Specifies when noncurrent object versions shall expire. | Container | No |
| NoncurrentVersionTransition | LifecycleConfiguration.Rule | Specifies when to transition objects of noncurrent versions and the target storage class. | Container | No |
| NoncurrentDays | LifecycleConfiguration.Rule<br>.NoncurrentVersionExpiration <br>or NoncurrentVersionTransition | Specifies the number of days between the date when an object becomes noncurrent and the date when the operation corresponding to a rule is performed.<br><li>If it is a `Transition` operation, this value should be a non-negative integer.<br><li>If it is an `Expiration` operation, this value should be a positive integer. The maximum value is 3650 (days). | Integer | No |
| StorageClass | LifecycleConfiguration.Rule<br>.Transition or <br>NoncurrentVersionTransition | Specifies the storage class of the transitioned object. Enumerated values: `STANDARD_IA`, `MAZ_STANDARD_IA`, `INTELLIGENT_TIERING`, `MAZ_INTELLIGENT_TIERING`, `ARCHIVE`, `DEEP_ARCHIVE`. For more information about storage classes, see [Storage Class Overview](https://intl.cloud.tencent.com/document/product/436/30925). | String | Yes |

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The response body is empty.

#### Error codes

This API returns common error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Examples

#### Request

```plaintext
PUT /?lifecycle HTTP/1.1
Host:examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 16 Aug 2017 11:59:33 GMT
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1502855771;1502935771&q-key-time=1502855771;1502935771&q-header-list=content-md5;host&q-url-param-list=lifecycle&q-signature=f3aa2c708cfd8d4d36d658de56973c9cf1c2****
Content-MD5: LcNUuow8OSZMrEDnvndw1Q==
Content-Length: 348
Content-Type: application/x-www-form-urlencoded



<LifecycleConfiguration>
      <Rule>
            <ID>id1</ID>
            <Filter>
                  <Prefix>documents/</Prefix>
            </Filter>
            <Status>Enabled</Status>
            <Transition>
                  <Days>100</Days>
                  <StorageClass>ARCHIVE</StorageClass>
            </Transition>
      </Rule>
      <Rule>
            <ID>id2</ID>
            <Filter>
                  <Prefix>logs/</Prefix>
            </Filter>
            <Status>Enabled</Status>
            <Transition>
                  <Days>10</Days>
                  <StorageClass>STANDARD_IA</StorageClass>
            </Transition>
      </Rule>
</LifecycleConfiguration>
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Date: Wed, 16 Aug 2017 11:59:33 GMT
Server: tencent-cos
x-cos-request-id: NTk5NDMzYTRfMjQ4OGY3Xzc3NGRf****
```
