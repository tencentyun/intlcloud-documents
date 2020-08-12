## Description

This API is used to configure a cross-region replication rule for a bucket where versioning is enabled. If there is already a rule for the bucket, the existing one will be overwritten.

> !
> - To use this API, make sure that the bucket has versioning enabled. For more information, see the API documentation [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889).
> - Currently, for a MAZ-enabled bucket, you can only delete expired objects, but not transition them to the STANDARD_IA or ARCHIVE storage class.

## Request

#### Sample request

```http
PUT /?replication HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-MD5: MD5
Authorization: Auth String
request body
```

> ?Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

The request body contains the configuration information for cross-region replication, including the status of the cross-region replication rule, content to be replicated, and the name and the region of the destination bucket.

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

The nodes are described in details below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------------ | ----------------------------------------- | ------------------------------------------------------------ | --------- | ---- |
| ReplicationConfiguration | None                                        | Contains all information about the cross-region configuration                                       | Container | Yes   |
|Role|ReplicationConfiguration    | Initiator ID: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`  |String    | Yes |
| Rule                     | ReplicationConfiguration                  | Replication rules up to 1,000                                 | Container | Yes   |
| ID                       | ReplicationConfiguration.Rule             | ID that identifies a rule                                     | String    | No   |
| Status                   | ReplicationConfiguration.Rule             | Indicates whether a rule is in effect. Enumerated values: Enabled, Disabled                | String    | Yes   |
|Prefix    |ReplicationConfiguration.Rule    | Prefix to be matched in the rule. Prefixes cannot overlap; otherwise, an error will be returned. The prefix matching root directory is empty |String    | Yes |
| Destination              | ReplicationConfiguration.Rule             | Destination bucket information                                               | Container | Yes   |
|Bucket    |ReplicationConfiguration.Rule.Destination    | Resource ID: <br>`qcs::cos:<Region>::<BucketName-APPID>` |String    | Yes |
| StorageClass | ReplicationConfiguration.Rule.Destination | Storage class. Enumerated values: STANDARD, STANDARD_IA, ARCHIVE. It is specified as that of the source bucket by default | String | No |

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The response body is empty.

#### Error codes

This API returns uniform error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

#### Request

The following PUT Bucket replication request adds a cross-region replication configuration to the bucket `originbucke-1250000000`, specifying that objects prefixed with `testPrefix` are to be replicated to the destination bucket `destinationbucket-1250000000` in Guangzhou.

```shell
PUT /?replication HTTP/1.1
Date: Mon, 28 Aug 2017 02:53:38 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1503888878;1503889238&q-key-time=1503888878;1503889238&q-header-list=host&q-url-param-list=replication&q-signature=254bf9cd3d6615e89a36ab652437f9d45c5f****
Content-MD5: AAq9nzrpsz5LJ4UEe1f6Q==
Host: originbucket-1250000000.cos.ap-guangzhou.myqcloud.com
Content-Length: 312

<ReplicationConfiguration>
	<Role>qcs::cam::uin/100000000001:uin/100000000001</Role>
	<Rule>
		<Status>Enabled</Status>
		<ID>RuleId_01</ID>
		<Prefix>testPrefix</Prefix>
		<Destination>
			<Bucket>qcs::cos:ap-guangzhou::destinationbucket-1250000000</Bucket>
		</Destination>
	</Rule>
</ReplicationConfiguration>
```

#### Response

After the request above is made, COS returns the following response, indicating that the cross-region replication rule has been successfully configured.

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
