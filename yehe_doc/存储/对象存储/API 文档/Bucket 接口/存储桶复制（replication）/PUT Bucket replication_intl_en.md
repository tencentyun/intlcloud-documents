## Overview

This API is used to add a cross-bucket replication rule to a versioning-enabled bucket. Note that the existing cross-bucket replication rule (if any) will be overwritten.

> !
>
> - To use this API, ensure that versioning is enabled for the bucket. For the API documentation of versioning, please see [PUT Bucket versioning](https://www.tencentcloud.com/document/product/436/19889).
> - Objects in MAZ buckets cannot be replicated to an OAZ bucket. For example, objects in MAZ_STANDARD cannot be replicated to STANDARD.



<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer (recommended)
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=PutBucketReplication" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                Tencent Cloud API Explorer makes it easy for you to make online API calls, verify signatures, generate SDK code, and search for APIs. You can use it to query the request and response of each API call and generate sample SDK codes for the call.
            </div>
        </div>
    </div>
</div>



## Requests

#### Request example

```plaintext
PUT /?replication HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-MD5: MD5
Authorization: Auth String
request body
```

>? 
> - Host: <BucketName-APPID>.cos.<Region>.myqcloud.com, where <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://www.tencentcloud.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://www.tencentcloud.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://www.tencentcloud.com/document/product/436/6224)).
> - Authorization: Auth String (see [Request Signature](https://www.tencentcloud.com/document/product/436/7778) for more information)
> 

#### Request headers

This API only uses [Common Request Headers](https://www.tencentcloud.com/document/product/436/7728).

#### Request body

You can set the cross-bucket replication configuration in the request body, which includes the rule status, priority, objects to replicate, filter scope, name and region of the destination bucket, and more.

```plaintext
<ReplicationConfiguration>
    <Role>qcs::cam::uin/<OwnerUin>:uin/<SubUin></Role>
    <Rule>
        <Status></Status>
        <ID></ID>
        <Prefix></Prefix>
        <Destination>
            <Bucket>qcs::cos:<Region>::<BucketName-APPID></Bucket>
            <StorageClass></StorageClass>
        </Destination>
        <DeleteMarkerReplication>
            <Status></Status>
        </DeleteMarkerReplication>
    </Rule>
</ReplicationConfiguration>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------------ | ----------------------------------------- | ------------------------------------------------------------ | --------- | -------- |
| ReplicationConfiguration | None | All replication configurations | Container | Yes |
| Role | ReplicationConfiguration | Request initiator identifier, formatted as `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` | String | Yes |
| Rule | ReplicationConfiguration | Specific configuration. You can set a maximum of 1,000 rules. | Container | Yes |
| ID | ReplicationConfiguration.Rule  | Name of a specific rule | String | No |
| Status | ReplicationConfiguration.Rule | `Rule` status identifier. Enumerated values: `Enabled`, `Disabled`. | String | Yes |
| Prefix                   | ReplicationConfiguration.Rule            | Prefix of the object to be replicated  | String    | No       |
| Destination | ReplicationConfiguration.Rule | Destination bucket information | Container | Yes |
| Bucket | ReplicationConfiguration.Rule.Destination | Resource identifier, formatted as <br>`qcs::cos:<Region>::<BucketName-APPID>` | String | Yes |
| DeleteMarkerReplication             | ReplicationConfiguration.Rule | Whether to sync the delete marker |Container    | No       |
|Status             | ReplicationConfiguration.Rule. DeleteMarkerReplication | Whether to sync the delete marker. Valid values: `Disabled`, `Enabled`. Default value: `Enabled`. |String    | No       |

## Response

#### Response headers

This API only returns [Common Response Headers](https://www.tencentcloud.com/document/product/436/7729).

#### Response body

The response body is empty.

#### Error codes

This API returns uniform error responses and error codes. For more information, see [Error Codes](https://www.tencentcloud.com/document/product/436/7730).

## Examples
#### Request

The following request adds a cross-bucket replication rule to the `originbucket-1250000000` bucket. The `ReplicationConfiguration` specifies that all objects prefixed with `testPrefix` are to be replicated to the `destinationbucket-1250000000` destination bucket in Guangzhou region.

```plaintext
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

After the request above is made, COS returns the following response, indicating that the cross-bucket replication rule has been successfully configured.

```plaintext
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

