## Feature Description

This API is used to add a cross-bucket replication rule to a versioning-enabled bucket. Note that the existing cross-bucket replication rule (if any) will be overwritten.

> !
>
> - To use this API, ensure that versioning is enabled for the bucket. For the API documentation of versioning, see [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889).
> - Objects in MAZ buckets cannot be replicated to an OAZ bucket. For example, objects in MAZ_STANDARD cannot be replicated to STANDARD.

## Request

#### Sample request

```plaintext
PUT /?replication HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-MD5: MD5
Authorization: Auth String
request body
```

>? 
> - Host: &lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com, where &lt;BucketName-APPID> is the bucket name followed by the `APPID`, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and &lt;Region> is a COS region (see [Regions and Access Endpoints](https://www.tencentcloud.com/document/product/436/6224)).
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> 

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

You can set the cross-bucket replication configuration in the request body, which includes the rule status, priority, objects to replicate, filter scope, name and region of the destination bucket, and more.

```plaintext
<ReplicationConfiguration>
    <Role>qcs::cam::uin/<OwnerUin>:uin/<SubUin></Role>
    <Rule>
        <Status></Status>
        <Priority></Priority>
        <ID></ID>
        <Filter>
            <And>
                <Prefix></Prefix>
                <Tag>
                    <Key></Key>
                    <Value></Value>
                </Tag>
                <Tag>
                    <Key></Key>
                    <Value></Value>
                </Tag>
            </And>
        </Filter>
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
|Priority                   | ReplicationConfiguration.Rule             | Rule execution priority, which is used to handle the situation where the destination buckets are the same and the replication rule hits the same object. All bucket replication rules must carry or not carry `Priority`, which can be an integer in the range of 1–1000 and must be unique for each rule. <li>If all rules carry `Priority`, when the destination buckets are the same, the object filtering prefixes in different rules can overlap. When different rules hit the same object, the rule with the smallest `Priority` value will be triggered first. <li>If all rules do not carry `Priority`, the object filtering prefixes in different rules cannot overlap. | Integer | No. All rules of the same bucket must carry or not carry `Priority`. |
|Filter                   | ReplicationConfiguration.Rule             | Object filter. The bucket replication feature will replicate objects matching the object prefix and tag set in `Filter`. | Container | No |
|And                   | ReplicationConfiguration.Rule             | When filtering the objects to be replicated, if you want to use both object prefix and object tag as filter conditions, you need to wrap them with `And`. | Container | No |
| Prefix                   | ReplicationConfiguration.Rule.Filter.And             | Prefix of the object to be replicated  | String    | No       |
| Tag                  | ReplicationConfiguration.Rule.Filter.And             | You can filter the objects to be replicated by one or more (up to 10) object tags. If tags are added as filter conditions, the `DeleteMarkerReplication` option must be set to `false`.	 | String | No       |
| Destination | ReplicationConfiguration.Rule | Destination bucket information | Container | Yes |
| Bucket | ReplicationConfiguration.Rule.Destination | Resource identifier, formatted as <br>`qcs::cos:<Region>::<BucketName-APPID>` | String | Yes |
| DeleteMarkerReplication             | ReplicationConfiguration.Rule | Whether to sync the delete marker |Container    | No       |
|Status             | ReplicationConfiguration.Rule. DeleteMarkerReplication | Whether to sync the delete marker. Valid values: `Disabled`, `Enabled`. Default value: `Enabled`. |String    | No       |

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The response body is empty.

#### Error codes

This API returns common error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

#### Sample 1: Bucket replication rule that filters by object prefix
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

#### Sample 2: Bucket replication rule that filters by object tag
#### Request

The following request adds a cross-bucket replication rule to the `originbucket-1250000000` bucket. The `ReplicationConfiguration` specifies that all objects prefixed with `test1` and tagged with `<111, 232>` are to be replicated to the `destinationbucket-1250000000` destination bucket in Guangzhou. After object tag filtering is set, `DeleteMarkerReplication` in the rule must be set to `Disabled`.

```plaintext
PUT /?replication HTTP/1.1
Host: originbucket-1250000000.cos.ap-guangzhou.myqcloud.com
Authorization: q-sign-algorithm=sha1&q-ak=AKIDYv3vWrwkHXVDfqkNj*********&q-sign-time=1667303319;1668303369&q-key-time=1667303319;1668303369&q-url-param-list=replication&q-header-list=content-md5;host&q-signature=78c13df3ce3bca422fcb994*****
Content-Md5: Hmy/6lHINHLKhp/PY****
Content-Length: 674
Content-Type: application/x-www-form-urlencoded

<ReplicationConfiguration>
    <Role>qcs::cam::uin/100000000001:uin/100000000001</Role>
    <Rule>
        <Status>Enabled</Status>
        <Filter>
            <And>
                <Prefix>test1</Prefix>
                <Tag>
                    <Key>111</Key>
                    <Value>222</Value>
                </Tag>
            </And>
        </Filter>
        <Destination>
            <Bucket>qcs::cos:ap-guangzhou::destinationbucket-1250000000</Bucket>
            <StorageClass>Standard</StorageClass>
        </Destination>
        <DeleteMarkerReplication>
            <Status>Disabled</Status>
        </DeleteMarkerReplication>
    </Rule>
</ReplicationConfiguration>
```

#### Response

After the request above is made, COS returns the following response, indicating that the cross-bucket replication rule has been successfully configured.

```plaintext
HTTP/1.1 200 OK
Content-Length: 0
Connection: keep-alive
Date: Tue, 01 Nov 2022 11:49:48 GMT
Server: tencent-cos
x-cos-bucket-region: ap-guangzhou
x-cos-request-id: NjM2MTA3ZGNfNmE1MGI3MDlfYWU5N1*******
```

#### Sample 3: Setting multiple rules that replicate objects to the same destination bucket with overlapping object prefixes and different priorities configured by `Priority`

#### Request

The following request adds two bucket replication rules for the bucket `originbucket-1250000000`.
- Rule 1: Specify to replicate the object prefixed with `test1` and tagged with `<a,a>` to the destination bucket `destinationbucket-1250000000` in `Standard` storage class in Guangzhou, with `DeleteMarkerReplication` set to `Disabled` and `Priority` set to `1`.
- Rule 2: Specify to replicate the object prefixed with `test1` and tagged with `<b,b>` to the destination bucket `destinationbucket-1250000000` in `Standard_IA` storage class in Guangzhou, with `DeleteMarkerReplication` set to `Disabled` and `Priority` set to `2`.

When you upload the object `test1/temp.txt` to the bucket `originbucket-1250000000` and set tags `<a,a>` and `<b,b>` at the same time, according to `Priority`, rule 1 will take effect to replicate the object to the bucket `destinationbucket-1250000000` in `Standard` storage class.

```plaintext
PUT /?replication HTTP/1.1
Host: originbucket-1250000000.cos.ap-guangzhou.myqcloud.com
Authorization: q-sign-algorithm=sha1&q-ak=AKIDYv3vWrwkHXVDfqkNjoc9PP8a******&q-sign-time=1667309117;1668309167&q-key-time=1667309117;1668309167&q-url-param-list=replication&q-header-list=content-md5;host&q-signature=b5730a15142d4bbc9974e42814918435*******
Content-Md5: OngWIL6wb2pnJZHk*****
Content-Length: 1351
Content-Type: application/x-www-form-urlencoded

<ReplicationConfiguration>
    <Role>qcs::cam::uin/100000000001:uin/100000000001</Role>
    <Rule>
        <Status>Enabled</Status>
        <Priority>1</Priority>
        <Filter>
            <And>
                <Prefix>test1</Prefix>
                <Tag>
                    <Key>a</Key>
                    <Value>a</Value>
                </Tag>
            </And>
        </Filter>
        <Destination>
            <Bucket>qcs::cos:ap-guangzhou::destinationbucket-1250000000</Bucket>
            <StorageClass>Standard</StorageClass>
        </Destination>
        <DeleteMarkerReplication>
            <Status>Disabled</Status>
        </DeleteMarkerReplication>
    </Rule>
    <Role>qcs::cam::uin/100000000001:uin/100000000001</Role>
    <Rule>
        <Status>Enabled</Status>
        <Priority>2</Priority>
        <Filter>
            <And>
                <Prefix>test1</Prefix>
                <Tag>
                    <Key>b</Key>
                    <Value>b</Value>
                </Tag>
            </And>
        </Filter>
        <Destination>
            <Bucket>qcs::cos:ap-guangzhou::destinationbucket-1250000000</Bucket>
            <StorageClass>Standard_IA</StorageClass>
        </Destination>
        <DeleteMarkerReplication>
            <Status>Disabled</Status>
        </DeleteMarkerReplication>
    </Rule>
</ReplicationConfiguration>
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Length: 0
Connection: keep-alive
Date: Tue, 01 Nov 2022 13:26:23 GMT
Server: tencent-cos
x-cos-bucket-region: ap-guangzhou
x-cos-request-id: NjM2MTFlN2ZfYjA1MGI3MDlfMjQ2ZmZfOWE******
```

