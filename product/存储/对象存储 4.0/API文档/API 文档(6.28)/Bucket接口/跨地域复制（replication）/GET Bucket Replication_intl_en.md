## Description
The GET Bucket replication API is used to query the cross-region replication configuration information in a bucket. When initiating this request, you need to get the request signature to indicate that the request has been authorized.

## Request
### Sample Request

```shell
GET /?replication HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).

### Request Headers
#### Common Headers
The implementation of this request operation uses a common request header. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Special Headers
This request operation has no special request headers.

### Request Body
The request body of this request is empty.

## Response
### Response Headers
#### Common Response Headers 
This response contains a common response header. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Special Response Headers

| Parameter | Type | Description |
|---|---|---|
| x-cos-replication-rule-creation-time | UTC timestamp | Creation time of the cross-region replication rule |

### Response Body
The return of this response body is **application/xml** data. Below is an example containing all the node data:

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

The content is described in details below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|---|---|---|---|---|
| ReplicationConfiguration | None | Describes all cross-region replication configuration information | Container | Yes |
|Role|ReplicationConfiguration    | Initiator ID: <br>`qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>`  |String    | Yes |
|Rule    |ReplicationConfiguration    | Specific configuration information of up to 1,000 rules. All rules must point to the same destination bucket |Container    | Yes |
|ID    |ReplicationConfiguration.Rule    | Identifies the name of a specific rule |String    |No |
|Status    |ReplicationConfiguration.Rule    | Indicates whether a rule is in effect; enumerated values: Enabled, Disabled |String    | Yes |
|Prefix    |ReplicationConfiguration.Rule    | Prefix matching policy. Policies cannot overlap; otherwise, an error will be returned. The prefix matching root directory is empty |String    | Yes |
|Destination    |ReplicationConfiguration.Rule    | Destination bucket information  |Container    | Yes |
|Bucket    |ReplicationConfiguration.Rule.Destination    | Resource ID: <br>`qcs::cos:[region]::[bucketname-Appid]`   |String    | Yes |
|StorageClass    |ReplicationConfiguration.Rule.Destination    | Storage class; enumerated values: Standard, Standard_IA; default value: class of the source bucket |String    | No |


## Error Analysis
Some frequent special errors that may occur with this request are listed below. For common error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).


| Error Code | Description | Status Code |
| ------------------------------------- | ---------------------- | ------------- |
| ReplicationConfigurationNotFoundError | No cross-region replication rule found. | 404 Not Found |

## Examples

### Request

The following request sample gets the cross-region replication configuration in the bucket `originBucket-1250000000`.
```shell
GET /?replication HTTP/1.1
Date: Fri, 14 Apr 2019 07:17:19 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98JM&q-sign-time=1503895278;1503895638&q-key-time=1503895278;1503895638&q-header-list=host&q-url-param-list=replication&q-signature=f77900be432072b16afd8222b4b349aabd837cb9
Host: originBucket-1250000000.cos.ap-guangzhou.myqcloud.com
Content-Length: 0
```

### Response

After the request above is made, COS returns the following response, indicating that the current cross-region replication configuration in the bucket is enabled. In the rule configuration information, the items to be copied are all objects prefixed with `testPrefix` in the bucket `originBucket-1250000000`, and the storage class of the object copies is the same as that of the objects in the source bucket by default.
```shell
Content-Type: application/xml
Content-Length: 309
Connection: keep-alive
Date: Fri, 14 Apr 2019 07:17:19 GMT
Server: tencent-cos
x-cos-replication-rule-creation-time: Fri, 14 Apr 2019 07:06:19 GMT
x-cos-request-id: NWQwMzQ5ZmZfMjBiNDU4NjRfNjAwOV84MzA2MjE=
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
