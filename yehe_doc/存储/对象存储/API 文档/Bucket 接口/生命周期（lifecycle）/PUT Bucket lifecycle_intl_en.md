## Feature Description

COS allows you to manage the lifecycle of objects in buckets through the lifecycle configuration, which contains one or more rule sets that will be applied to a set of objects. Each rule defines a COS operation.
There are two types of operations:

- **Transition**: defines when an object is transitioned to another storage class. For example, you can choose to transition an object to the `STANDARD_IA` storage class 30 days after its creation, which is suitable for objects that are not accessed frequently. You can also choose to transition the data to the `ARCHIVE` storage class, which is available for regions within Mainland China, to lower your costs. For specific parameters, please see `Transition` in the sample request description.
- **Expiration**: specifies when an object shall expire. COS will automatically delete expired objects.

#### Detail analysis

This API is used to create a new lifecycle configuration for a bucket. If a lifecycle configuration has already been set for the bucket, the new configuration created with this API will overwrite the existing one.

> !`Days` and `Date` parameters cannot be used in the same lifecycle rule. Please pass them in as two separate rules. For more information, please see [Use Case](#.E5.AE.9E.E9.99.85.E6.A1.88.E4.BE.8B) below.

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

> Authorization: Auth String (for more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).

#### Request header

This API only uses common request headers. For more information, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).


#### Request body

The specific nodes of the request body for this API request are as follows:

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
  </Rule>
</LifecycleConfiguration>
```

The content is described in detail below:

| Node Name (Keyword) | Parent Node | Description  | Type | Required |
| ------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | --------- | -------- |
| LifecycleConfiguration         | None                                                           | Lifecycle configuration                                                 | Container | Yes       |
| Rule                           | LifecycleConfiguration                                       | Rule description                                                     | Container | Yes       |
| ID                             | LifecycleConfiguration.Rule                                  | Uniquely identifies a rule. Length limit: 255 characters                    | String    | No       |
| Filter                         | LifecycleConfiguration.Rule                                  | Describes the set of objects subject to the rule                        | Container | Yes       |
| And                        |   LifecycleConfiguration.Rule<br>.Filter             | A subset in the object filter, which is required only when you need to specify multiple filter rules, <br>such as both `Prefix` and `Tag` or multiple `Tag` values for filtering |Container| No   |
| Prefix                         | LifecycleConfiguration.Rule<br>.Filter.And                           | Specifies the prefix to which the rule applies. Objects that match the prefix are subject to this rule. <br>There can be at most one prefix | String    | No       |
|  Tag   |    LifecycleConfiguration.Rule<br>.Filter.And   |         Tag set. Up to 10 tags are supported    |   Container  |  No |
|  Key  |    LifecycleConfiguration.Rule<br>.Filter.And.Tag  |    Tag key, which can contain letters, digits, spaces, plus signs, minus signs, underscores, equal signs, dots, colons, and slashes <br>with a maximum length of 128 bytes     |     String	|   No    |
|  Value  |    LifecycleConfiguration.Rule<br>.Filter.And.Tag  |   Tag value, which can contain letters, digits, spaces, plus signs, minus signs, underscores, equal signs, dots, colons, and slashes <br>with a maximum length of 256 bytes	    |   String	 |  No
| Status                         | LifecycleConfiguration.Rule                                  | Indicates whether the rule is enabled. Enumerated values: Enabled, Disabled                  | String    | Yes       |
| Expiration                     | LifecycleConfiguration.Rule                                  | Rule expiration attribute                                                 | Container | No       |
| Transition                     | LifecycleConfiguration.Rule                                  | Rule transition attribute, which specifies when an object should be transitioned to `Standard_IA` or `ARCHIVE` storage class          | Container | No       |
| Days                           | LifecycleConfiguration.Rule<br>.Transition or Expiration      | Specifies the number of days between the date an object was last modified and the date when the operation corresponding to a rule should be performed. <br><li>If it is a `Transition` operation, this value should be a non-negative integer. <br><li>If it is an `Expiration` operation, this value should be a positive integer. Maximum value: 3,650 days | Integer   | No       |
| Date                           | LifecycleConfiguration.Rule<br>.Transition or Expiration      | Specifies when the operation corresponding to a rule will be performed. Supported formats are `2007-12-01T12:00:00.000Z`<br>and `2007-12-01T00:00:00+08:00` | String    | No       |
| ExpiredObjectDeleteMarker      | LifecycleConfiguration.Rule<br>.Expiration                       | Specifies whether to delete the delete marker of an expired object. Enumerated values: true, false                     | String    | No       |
| AbortIncompleteMultipartUpload | LifecycleConfiguration.Rule                                  | Sets the maximum amount of time allowed for a multipart upload to keep running                           | Container | No       |
| DaysAfterInitiation            | LifecycleConfiguration.Rule<br>.AbortIncompleteMultipartUpload | Specifies the number of days in which a multipart upload must be completed once started                       | Integer   | Yes       |
| NoncurrentVersionExpiration    | LifecycleConfiguration.Rule                                  | Specifies when a non-current object should expire                                   | Container | No       |
| NoncurrentVersionTransition    | LifecycleConfiguration.Rule                                  | Specifies when a non-current object should be transitioned to `STANDARD_IA` or `ARCHIVE` storage class          | Container | No       |
| NoncurrentDays                 | LifecycleConfiguration.Rule<br>.NoncurrentVersionExpiration <br>or NoncurrentVersionTransition | Specifies the number of days between the date when an object becomes non-current and the date when the operation corresponding to a rule should be performed. <br><li>If it is a `Transition` operation, this value should be a non-negative integer. <br><li>If it is an `Expiration` operation, this value should be a positive integer. Maximum value: 3,650 days | Integer   | No       |
| StorageClass                   | LifecycleConfiguration.Rule<br>.Transition or <br>NoncurrentVersionTransition | Specifies the transitioned storage class of an object. Enumerated values: STANDARD_IA, <br>ARCHIVE | String    | Yes       |

## Response

#### Response headers

This API only returns common response headers. For more information, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The response body is empty.

#### Error codes

This API returns uniform error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Use Case

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
