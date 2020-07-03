## Feature description
COS allows you to manage the lifecycle of objects in buckets through the lifecycle configuration, which contains one or more rule sets that will be applied to a set of objects. Each rule defines a COS operation.
There are two types of operations:
- **Transition**: Defines when an object is transitioned to another storage class. For example, you can choose to transition an object to the `STANDARD_IA` storage class 30 days after its creation, which is suitable for objects that are not accessed frequently. You can also choose to transition the data to the `ARCHIVE` storage class, which is available for regions within the Chinese mainland, to lower your costs. For specific parameters, see `Transition` in the sample request description.
- **Expiration**: Specifies when an object shall expire. COS will automatically delete expired objects.

#### Detail Analysis

This API is used to create a new lifecycle configuration for a bucket. If a lifecycle configuration has already been set for the bucket, the new configuration created with this API will overwrite the existing one.

> Days and Date parameters are not supported in the same lifecycle rule. Please pass them in as two separate rules. For details, refer to the following [Use Case] ​​(#. E5.AE.9E.E9.99.85.E6.A1.88.E4.BE.8B).

#### Request
#### Sample request 

```shell
PUT /?lifecycle HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Content-Length: length
Date: GMT Date
Authorization: Auth String 
Content-MD5: MD5
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).

#### Request Headers

#### Common Headers
This request uses a common request headers. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Special Headers

**Required Headers**
This request uses the following required request headers:

| Name | Description | Type | Required |
| ---------------- | ----------- | ------ | ---- |
| Content-MD5 | Base64-encoded MD5 hash of the request body content defined in RFC 1864, used to verify whether the request body underwent changes during transfer | String | Yes |


#### Request Body
The specific nodes of the request body for this API request are:

```shell
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

The content is described in detail below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|---|---|---|---|---|
| LifecycleConfiguration | None | Lifecycle configuration | Container | Yes |
| Rule | LifecycleConfiguration | Rule description | Container | Yes |
| Filter | LifecycleConfiguration.Rule | Filters the set of objects subject to a rule | Container | Yes |
| Status | LifecycleConfiguration.Rule | Specifies whether a rule is enabled. Enumerated values: `Enabled`, `Disabled` | Container | Yes |
| ID | LifecycleConfiguration.Rule | Unique identifier of a rule; it can be up to 255 characters in length | String | No |
| Prefix | LifecycleConfiguration.Rule.Filter | Specifies the prefix to which a rule applies. Objects whose prefix matches the one specified are subject to this rule. Only one prefix may be specified for this parameter. | String | No |
| Expiration | LifecycleConfiguration.Rule | Expiration attributes of a rule | Container | No |
| Transition | LifecycleConfiguration.Rule | Transition attributes of a rule, which specify when an object is transitioned to `Standard_IA` or `ARCHIVE` storage class | Container | No |
| Days | LifecycleConfiguration.Rule.Transition <br>or Expiration | Specifies the number of days between the date an object was last modified and the date when the operation corresponding to a rule is performed. If it is a `Transition` operation, this value should be a non-negative integer. If it is an `Expiration` operation, this valid should be a positive integer. Maximum: 3,650 days | Integer | No |
| Date | LifecycleConfiguration.Rule.Transition<br>or Expiration | Indicates when the action corresponding to the rule will be performed; the supported formats are `2007-12-01T12:00:00.000Z` and `2007-12-01T00:00:00+08:00` | String | No |
| ExpiredObjectDeleteMarker | LifecycleConfiguration.Rule.Expiration | Deletes the delete marker of an expired object. Enumerated values: `true`, `false` | String | No |
| AbortIncompleteMultipartUpload | LifecycleConfiguration.Rule | Configures the maximum time a multipart upload is allowed to keep running | Container | No |
| DaysAfterInitiation | LifecycleConfiguration.Rule<br>.AbortIncompleteMultipartUpload | Specifies the number of days in which a multipart upload must be completed once started | Integer | Yes |
| NoncurrentVersionExpiration | LifecycleConfiguration.Rule | Specifies when non-current versions of an object expire | Container | No |
| NoncurrentVersionTransition | LifecycleConfiguration.Rule | Specifies when non-current versions of an object are transitioned to `STANDARD_IA` or `ARCHIVE` storage class | Container | No |
| NoncurrentDays | LifecycleConfiguration.Rule<br>.NoncurrentVersionExpiration<br>or NoncurrentVersionTransition | Specifies the number of days between the date when an object becomes non-current and the date when the operation corresponding to a rule is performed. If it is a `Transition` operation, this value should be a non-negative integer. If it is an `Expiration` operation, this value should be a positive integer. Maximum: 3,650 days | Integer | No |
| StorageClass | LifecycleConfiguration.Rule.Transition <br>or NoncurrentVersionTransition | Specifies the storage class to which an object is transitioned. Enumerated values: `STANDARD_IA`, `ARCHIVE` | String | Yes |


## Response
#### Response Header

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).


#### Response Body
The response body of this response is empty.

#### Error Codes
The following describes some frequent errors that may occur when you make this request. For specific error causes, see the returned error messages. For more COS error codes or a complete list of errors, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

| Error Code | HTTP Status Code | Description |
|--------|--------|----------|
| NoSuchBucket | 404 Not Found | The bucket you are trying to access does not exist |
| MalformedXML | 400 Bad Request | Invalid XML format. Please check against the RESTful API documentation for accuracy |
| InvalidRequest | 400 Bad Request | Invalid request. If the error message reads "Conflict lifecycle rule", it means that rules in the XML data conflict with each other |
| InvalidArgument | 400 Bad Request | Invalid request parameter. If the error message reads "Rule ID must be unique. Found same ID for more than one rule", it means that multiple rules have the same value for the `ID` field |

## Use Cases

#### Request
```shell
PUT /?lifecycle HTTP/1.1
Host:examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Wed, 16 Aug 2017 11:59:33 GMT
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98JM&q-sign-time=1502855771;1502935771&q-key-time=1502855771;1502935771&q-header-list=content-md5;host&q-url-param-list=lifecycle&q-signature=f3aa2c708cfd8d4d36d658de56973c9cf1c24654
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
```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Date: Wed, 16 Aug 2017 11:59:33 GMT
Server: tencent-cos
x-cos-request-id: NTk5NDMzYTRfMjQ4OGY3Xzc3NGRfMWY=
```
