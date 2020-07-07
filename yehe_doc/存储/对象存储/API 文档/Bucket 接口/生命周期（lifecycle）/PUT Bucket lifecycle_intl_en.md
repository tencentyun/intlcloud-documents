## Feature

COS allows you to manage the lifecycle of objects in buckets through lifecycle configuration, which contains one or more rule sets that will be applied to a set of objects. Each rule defines an operation for COS.
There are two types of operations:

- **Transition**: defines the time when an object is transitioned to another storage class. For example, you can choose to transition an object 30 days after its creation to the `STANDARD_IA` storage class, which is suitable for objects that are not accessed frequently. You can also choose to transition the data to the `ARCHIVE` storage class, which is available in regions within Mainland China, to lower cost. For specific parameters, see `Transition` in sample request description.
- **Expiration**: specifies the expiration time of an object. COS will automatically delete expired objects.

#### Notes

This API is used to create a new lifecycle configuration for a bucket. If a lifecycle configuration has already been set, the new configuration created with this API will overwrite the existing one.

>
> - You cannot specify both `Days` and `Date` in one lifecycle rule. Please pass them in as two separate rules. For details, see the following [Samples](#.E5.AE.9E.E9.99.85.E6.A1.88.E4.BE.8B).
> - Currently, [MAZ](https://intl.cloud.tencent.com/document/product/436/35208)-enabled buckets allow you to set the specified number of days/time after which an object expires and is deleted, but do not support transitioning objects to STANDARD_IA or ARCHIVE storage.

## Request

#### Sample request

```plaintext
PUT /?lifecycle HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Content-Length: length
Date: GMT Date
Authorization: Auth String 
Content-MD5: MD5
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information)

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

The specific nodes of the request body for this API request are:

```xml
<LifecycleConfiguration>
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
  </Rule>
</LifecycleConfiguration>
```

The nodes are described in details below:

| Node Name             | Parent Node                                                       | Description                                                         | Type      | Required |
| ------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | --------- | -------- |
| LifecycleConfiguration         | None                                                           | Lifecycle configuration                                                 | Container | Yes       |
| Rule                           | LifecycleConfiguration                                       | Specifies the rule                                                     | Container | Yes       |
| Filter                         | LifecycleConfiguration.Rule                                  | Specifies which objects are subject to the rule                        | Container | Yes       |
| Status                         | LifecycleConfiguration.Rule                                  | Specifies whether the rule is enabled. Enumerated values: Enabled, Disabled                  | String    | Yes       |
| ID                             | LifecycleConfiguration.Rule                                  | Uniquely identifies the rule; up to 255 characters in length                    | String    | No       |
| Prefix                         | LifecycleConfiguration.Rule.Filter                           | Specifies zero or only one prefix in the rule. All objects that match this prefix are subject to the rule. | String    | No       |
| Expiration                     | LifecycleConfiguration.Rule                                  | Rule expiration attribute                                        | Container | No       |
| Transition                     | LifecycleConfiguration.Rule                                  | Specifies in the rule when an object transitions to STANDARD_IA or ARCHIVE          | Container | No       |
| Days | LifecycleConfiguration.Rule.Transition <br>or Expiration | Specifies the number of days the action specified in the rule will be performed after the last modified date of the object.<br><li>If the action is `Transition`, the valid value of this field should be a non-negative integer<br><li>If it is `Expiration`, the valid value of this field should be a positive integer. Maximum: 3,650 days | Integer | No |
| Date | LifecycleConfiguration.Rule.Transition<br>or Expiration | Indicates when the action specified in the rule will be performed, supported formats are `2007-12-01T12:00:00.000Z` and `2007-12-01T00:00:00+08:00` | String | No |
| ExpiredObjectDeleteMarker      | LifecycleConfiguration.Rule.Expiration                       | Deletes delete markers of expired objects. Enumerated values: true, false                     | String    | No       |
| AbortIncompleteMultipartUpload | LifecycleConfiguration.Rule                                  | Sets the maximum duration for an in-progress multipart upload                           | Container | No       |
| DaysAfterInitiation | LifecycleConfiguration.Rule<br>.AbortIncompleteMultipartUpload | Specifies the number of days before a multipart upload must be completed once started | Integer | Yes |
| NoncurrentVersionExpiration    | LifecycleConfiguration.Rule                                  | Specifies when noncurrent versions of an object expire                                   | Container | No       |
| NoncurrentVersionTransition | LifecycleConfiguration.Rule | Specifies when non-current versions of an object are transitioned to `STANDARD_IA` or `ARCHIVE` storage class | Container | No |
| NoncurrentDays | LifecycleConfiguration.Rule<br>.NoncurrentVersionExpiration<br>or NoncurrentVersionTransition | Specifies the number of days the action specified in the rule will be performed after an object version becomes noncurrent.<br><li>If the action is `Transition`, the valid value of this field should be a non-negative integer.<br><li>If it is `Expiration`, the valid value of this field should be a positive integer. Maximum: 3,650 days | Integer | No |
|StorageClass    |LifecycleConfiguration.Rule.Transition <br>or NoncurrentVersionTransition    | Specifies to which storage class an object is transitioned. Enumerated values: `STANDARD_IA`, `ARCHIVE`   |String    | Yes |

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The response body of this response is empty.

#### Error codes

This API uses standardized error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) .

## Samples

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
    <Expiration>
      <Days>10</Days>
    </Expiration>
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
