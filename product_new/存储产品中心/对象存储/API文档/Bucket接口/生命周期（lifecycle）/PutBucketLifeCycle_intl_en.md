## Description
COS allows you to manage the lifecycle of objects in buckets through lifecycle configuration that contains one or more rule sets that will be applied to a set of objects. Each rule defines an operation for COS.
There are two types of operations:
- **Transition**: Defines the time when an object is transitioned to another storage class. For example, 30 days after the creation of an object, you can choose to transition it to the `STANDARD_IA` storage class which is suitable for objects that are not accessed frequently. You can also choose to transition it to the `ARCHIVE` storage class for even lower costs which is available in regions within Mainland China. For specific parameters, see `Transition` in the sample request description.
- **Expiration**: Specifies the expiration time of an object. COS will automatically delete expired objects.

### Notes

This API is used to create a new lifecycle configuration for a bucket. If a lifecycle configuration has already been made for the bucket, the new configuration created with this API will overwrite the existing one.

## Request
### Sample Request

```shell
PUT /?lifecycle HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Content-Length: length
Date: GMT Date
Authorization: Auth String 
Content-MD5: MD5
```
> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).

### Request Headers

#### Common Headers
The implementation of this operation uses common request headers. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Special Headers

**Required headers**
The implementation of this request operation uses the following required request headers:

| Name | Description | Type | Required |
| ---------------- | ----------- | ------ | ---- |
| Content-MD5 | **Base64-encoded** 128-bit MD5 checksum as defined in RFC 1864. This header is used to verify whether the file content has changed | String | No |


### Request Body
The node content of this request body is:

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

The content is described in details below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|---|---|---|---|---|
|LifecycleConfiguration    | None    | Lifecycle configuration    |Container    | Yes |
|Rule|    LifecycleConfiguration    | Rule description    |Container| Yes |
|Filter    |LifecycleConfiguration.Rule    | Describes the set of objects subject to a rule    |Container    | Yes |
|Status    |LifecycleConfiguration.Rule    | Specifies whether a rule is enabled. Enumerated values: `Enabled`, `Disabled`     |Container    | Yes |
|ID    |LifecycleConfiguration.Rule| Uniquely identifies a rule; up to 255 characters in length   |String    | No |
|And    |LifecycleConfiguration.Rule.Filter    | Used to connect `Prefix`    |Container    | Yes |
|Prefix    |LifecycleConfiguration.Rule.Filter <br>or LifecycleConfiguration.Rule.Filter.And    | Specifies the prefix to which a rule applies. Objects that match the prefix are subject to the rule. You can specify at most one `Prefix`   |Container    | No |
|Expiration    |LifecycleConfiguration.Rule    | Expiration attribute of a rule    |Container    | No |
|Transition    |LifecycleConfiguration.Rule    | Transition attribute of a rule, specifying when an object is transitioned to `Standard_IA` or `ARCHIVE` storage class   |Container    | No |
|Days    |LifecycleConfiguration.Rule.Transition <br>or Expiration    | Specifies the number of days between the last modified date of an object and the date when the operation corresponding to a rule is performed. If the operation is `Transition`, a valid value of this field should be a non-negative integer; if it is `Expiration`, a valid value of this field should be a positive integer. Maximum: 3,650 days | Integer | No |
|Date    |LifecycleConfiguration.Rule.Transition <br>or  Expiration    | Specifies when the operation corresponding to a rule is performed    |String    | No |
|ExpiredObjectDeleteMarker    |LifecycleConfiguration.Rule.Expiration    | Whether to delete the delete marker of an expired object. Enumerated values: `true`, `false`    |String    | No |
|AbortIncompleteMultipartUpload    |LifecycleConfiguration.Rule    |Sets the maximum amount of time allowed for a multipart upload to keep running    |Container    | No |
|DaysAfterInitiation    |LifecycleConfiguration.Rule<br>.AbortIncompleteMultipartUpload    | Specifies in how many days a multipart upload must be completed once started    |Integer    | Yes |
|NoncurrentVersionExpiration    |LifecycleConfiguration.Rule    | Specifies when non-current versions of an object expire    |Container    | No |
|NoncurrentVersionTransition    |LifecycleConfiguration.Rule    | Specifies when non-current versions of an object are transitioned to `STANDARD_IA` or `ARCHIVE` storage class   |Container   | No |
|NoncurrentDays    |LifecycleConfiguration.Rule, <br>.NoncurrentVersionExpiration, <br>or NoncurrentVersionTransition    | Specifies the number of days between the date when an object becomes non-current and the date when the operation corresponding to a rule is performed. If the operation is `Transition`, a valid value of this field should be a non-negative integer; if it is `Expiration`, a valid value of this field should be a positive integer. Maximum: 3,650 days | Integer | No |
|StorageClass    |LifecycleConfiguration.Rule.Transition <br>or NoncurrentVersionTransition    | Specifies to which storage class an object is transitioned. Enumerated values: `STANDARD_IA`, `ARCHIVE`   |String    | Yes |


## Response
### Response Headers

#### Common Response Headers 
This response uses common response headers. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).
#### Special Response Headers
This response does not use any special response header.

### Response Body
The response body of this response is empty.

### Error Codes
The following describes some frequent special errors that may occur when you make this request. For specific reasons of errors, see the returned error messages. For more COS error codes or a complete list of errors, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

| Error Code | HTTP Status Code | Description |
|--------|--------|----------|
|NoSuchBucket|404 Not Found| The bucket you are trying to access does not exist |
|MalformedXML|400 Bad Request| Invalid XML format. Please check against the RESTful API documentation |
|InvalidRequest|400 Bad Reques| Invalid request. If the error message shows "Conflict lifecycle rule", it means that multiple rules in the XML data conflict with each other. |
|InvalidArgument|400 Bad Reques| Invalid request parameter. If the error message shows "Rule ID must be unique. Found same ID for more than one rule", it means that multiple rules have the same `ID` field. |

## Example

### Request
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

### Response
```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Date: Wed, 16 Aug 2017 11:59:33 GMT
Server: tencent-cos
x-cos-request-id: NTk5NDMzYTRfMjQ4OGY3Xzc3NGRfMWY=
```
