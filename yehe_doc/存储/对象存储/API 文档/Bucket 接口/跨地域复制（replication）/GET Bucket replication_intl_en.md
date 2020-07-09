## Description
This API is used to query the cross-region replication configuration for a bucket. To make this request, you need to get a signature to authenticate the request.

## Request
#### Sample request

```shell
GET /?replication HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>?Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).


#### Request body
The request body of this request is empty.

## Response
#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body
This response body returns **application/xml** data. The following example contains all the node data:

```shell
<ReplicationConfiguration>
	<Role>qcs::cam::uin/[UIN]:uin/[Subaccount]</Role>
	<Rule>
		<Status></Status>
		<ID></ID>
		<Prefix></Prefix>
		<Destination>
			<Bucket>qcs::cos:[Region]::[BucketName-APPID]</Bucket>
		</Destination>
	</Rule>
</ReplicationConfiguration>
```

The nodes are described in details below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|---|---|---|---|---|
| ReplicationConfiguration | None | Contains all information about the cross-region replication configuration | Container | Yes |
|Role|ReplicationConfiguration    | Initiator ID: <br>`qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>`  |String    | Yes |
|Rule    |ReplicationConfiguration    | Configuration rules up to 1,000, which must point to the same destination bucket  |Container    | Yes |
|ID    |ReplicationConfiguration.Rule    | ID that identifies a specific rule |String    |No |
|Status    |ReplicationConfiguration.Rule    | Indicates whether a rule is in effect; enumerated values: Enabled, Disabled |String    | Yes |
|Prefix    |ReplicationConfiguration.Rule    | Prefix matching rule. Rules cannot overlap; otherwise, an error will be returned. The prefix matching root directory is empty |String    | Yes |
|Destination    |ReplicationConfiguration.Rule    | Destination bucket information  |Container    | Yes |
|Bucket    |ReplicationConfiguration.Rule.Destination    | Resource ID: <br>`qcs::cos:[region]::[bucketname-Appid]`   |String    | Yes |
|StorageClass    |ReplicationConfiguration.Rule.Destination    | Storage class; enumerated values: Standard, Standard_IA. By default, it’s the same as that of the source bucket |String    | No |


#### Error codes

This API returns uniform error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).




## Samples

#### Request

The following request sample gets the cross-region replication configuration from the bucket `originbucket-1250000000`.
```shell
GET /?replication HTTP/1.1
Date: Fri, 14 Apr 2019 07:17:19 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98JM&q-sign-time=1503895278;1503895638&q-key-time=1503895278;1503895638&q-header-list=host&q-url-param-list=replication&q-signature=f77900be432072b16afd8222b4b349aabd837cb9
Host: originbucket-1250000000.cos.ap-guangzhou.myqcloud.com
Content-Length: 0
```

#### Response

After the request succeeds, COS returns the following response, indicating that the cross-region replication configuration for the bucket is enabled. In this example, the replication rule dictates that objects to be replicated are the ones prefixed with `testPrefix` in the bucket `originbucket-1250000000`, and the storage class of the object copies is by default the same as that of the objects in the source bucket.
```shell
Content-Type: application/xml
Content-Length: 309
Connection: keep-alive
Date: Fri, 14 Apr 2019 07:17:19 GMT
Server: tencent-cos
x-cos-replication-rule-creation-time: Fri, 14 Apr 2019 07:06:19 GMT
x-cos-request-id: NWQwMzQ5ZmZfMjBiNDU4NjRfNjAwOV84MzA2****
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
