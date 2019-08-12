## Description
The PUT Bucket replication API is used to configure a cross-region replication rule for a bucket where versioning is enabled. If there is already a rule for the bucket, it will be overwritten.

>! When using this API, make sure that the bucket has versioning enabled. For more information, see the [API document for PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889).

## Request
### Sample Request

```http
PUT /?replication HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-MD5: MD5
Authorization: Auth String
request body
```

>Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).

### Request Headers
#### Common Headers
The implementation of this request operation uses a common request header. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Special Headers
This request operation has no special request headers.

### Request Body
You need to set the specific configuration information for cross-region replication in the request body, including information such as the status of the cross-region replication rule, content to be copied, destination bucket name, and storage region. For each bucket that has versioning enabled, COS currently supports configuring only one cross-region replication rule.

```http
<ReplicationConfiguration>
	<Role>qcs::cam::uin/<OwnerUin>:uin/<SubUin></Role>
	<Rule>
		<Status></Status>
		<ID></ID>
		<Prefix></Prefix>
		<Destination>
			<Bucket>qcs::cos:<Region>::<BucketName-APPID></Bucket>
		</Destination>
	</Rule>
</ReplicationConfiguration>
```

The content is described in details below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|---|---|---|---|---|
| ReplicationConfiguration | None | Describes all cross-region replication configuration information | Container | Yes |
|Role|ReplicationConfiguration    | Initiator ID: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`      |String    | Yes |
|Rule    |ReplicationConfiguration    | Specific configuration information of up to 1,000 rules. All rules must point to the same destination bucket |Container    | Yes |
|ID    |ReplicationConfiguration.Rule    | Identifies the name of a specific rule |String    |No |
|Status    |ReplicationConfiguration.Rule    | Indicates whether a rule is in effect; enumerated values: Enabled, Disabled |String    | Yes |
|Prefix    |ReplicationConfiguration.Rule    | Prefix matching policy. Policies cannot overlap; otherwise, an error will be returned. The prefix matching root directory is empty |String    | Yes |
|Destination    |ReplicationConfiguration.Rule    | Destination bucket information  |Container    | Yes |
|Bucket    |ReplicationConfiguration.Rule.Destination    | Resource ID: `qcs::cos:<Region>::<BucketName-APPID>`|String    | Yes |
|StorageClass    |ReplicationConfiguration.Rule.Destination    | Storage class; enumerated value: STANDARD, STANDARD_IA; default value: class of the source bucket <br>**Note:** Currently, cross-region replication does not support specifying the storage class of object copies as archive storage. If you need to set this class for the copies, you can configure lifecycle management in the destination bucket. For more information, see [PUT Bucket lifecycle](https://cloud.tencent.com/document/product/436/8280)|String    | No |

## Response

### Response Headers
#### Common Response Headers 
This response contains a common response header. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).
#### Special Response Headers
The response to this request has no special response headers.

### Response Body
This response body is empty.

### Error Analysis
Some frequent special errors that may occur with this request are listed below. For common error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

| Error Code | Description | Status Code |
|---|---|---|
|InvalidBucketState| Versioning is not enabled for the current bucket; therefore, cross-region replication cannot be enabled. |409 Conflict|
|InvalidArgument| Invalid parameter. |400 Bad Request|

## Examples
### Request
The following PUT Bucket replication request adds a cross-region replication configuration to the bucket `originBucket-1250000000`, indicating to copy objects prefixed with `testPrefix` to the destination bucket `destinationBucket-1250000000` in Guangzhou.
```shell
PUT /?replication HTTP/1.1
Date: Mon, 28 Aug 2017 02:53:38 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1503888878;1503889238&q-key-time=1503888878;1503889238&q-header-list=host&q-url-param-list=replication&q-signature=254bf9cd3d6615e89a36ab652437f9d45c5f****
Content-MD5: AAq9nzrpsz5LJ4UEe1f6Q==
Host: originBucket-1250000000.cos.ap-guangzhou.myqcloud.com
Content-Length: 312

<ReplicationConfiguration>
	<Role>qcs::cam::uin/100000000001:uin/100000000001</Role>
	<Rule>
		<Status>Enabled</Status>
		<ID>RuleId_01</ID>
		<Prefix>testPrefix</Prefix>
		<Destination>
			<Bucket>qcs::cos:ap-guangzhou::destinationBucket-1250000000</Bucket>
		</Destination>
	</Rule>
</ReplicationConfiguration>
```

### Response

After the request above is made, COS returns the following response, indicating that the cross-region replication has been successfully configured.
```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Fri, 14 Apr 2019 07:06:19 GMT
Server: tencent-cos
x-cos-bucket-region: ap-guangzhou
x-cos-request-id: NWQwMzQ3NmJfMjRiMjU4NjRfOTM4NV82ZDU1****
x-cos-trace-id: OGVmYzZiMmQzYjA2OWNhODk0NTRkMTBiOWVmMDAxODc0OWRkZjk0ZDM1NmI1M2E2MTRlY2MzZDhmNmI5MWI1OWE4OGMxZjNjY2JiNTBmMTVmMWY1MzAzYzkyZGQ2ZWM4MzUyZTg1NGRhNWY0NTJiOGUyNTViYzgyNzgxZTEwOTY=
```
