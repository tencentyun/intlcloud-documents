## Overview

This API (PUT Bucket replication) is used to add a cross-bucket replication rule to a versioning-enabled bucket. Note that the existing cross-bucket replication rule (if any) will be overwritten.

> !
>
> - To use this API, ensure that versioning is enabled for the bucket. For the API documentation of versioning, please see [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889).

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

> ?Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)

#### Request headers

This API only uses common request headers. For more information, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

You can set the cross-bucket replication configuration in the request body, which includes the rule status, objects to replicate, name and region of the destination bucket, and more.

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

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------------ | ----------------------------------------- | ------------------------------------------------------------ | --------- | -------- |
| ReplicationConfiguration | None | All replication configurations | Container | Yes |
| Role | ReplicationConfiguration | Request initiator identifier, formatted as `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` | String | Yes |
| Rule | ReplicationConfiguration | Specific configuration. You can set a maximum of 1,000 rules. | Container | Yes |
| ID | ReplicationConfiguration.Rule  | Name of a specific rule | String | No |
| Status | ReplicationConfiguration.Rule | `Rule` status identifier. Enumerated values: `Enabled`, `Disabled` | String | Yes |
| Prefix | ReplicationConfiguration.Rule | Prefix matching policy. Policies cannot overlap; otherwise, an error will be returned. To match the root directory, leave this parameter empty. | String | Yes |
| Destination | ReplicationConfiguration.Rule | Destination bucket information | Container | Yes |
| Bucket | ReplicationConfiguration.Rule.Destination | Resource identifier, formatted as <br>`qcs::cos:<Region>::<BucketName-APPID>` | String | Yes |
| StorageClass | ReplicationConfiguration.Rule.Destination | Storage class. Enumerated values: `STANDARD`, `INTELLIGENT_TIERING`, `STANDARD_IA`. Defaults to the storage class of the source bucket. | String | No |

## Response

#### Response headers

This API returns only common response headers. For more information, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The response body is empty.

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Sample

#### Request

The following `PUT Bucket replication` request adds a cross-bucket replication rule to the `originbucket-1250000000` bucket. The `ReplicationConfiguration` specifies that all objects prefixed with `testPrefix` are to be replicated to the `destinationbucket-1250000000` destination bucket in the Guangzhou region.

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

After the request above is made, COS returns the following response, indicating that the cross-bucket replication rule has been successfully configured.

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
