## Overview

This API is used to create an inventory job for a bucket. For more information, see [Inventory Overview](https://intl.cloud.tencent.com/document/product/436/30622).

> !
> - You can create up to 1,000 inventory jobs for each COS bucket.
> - You must add a bucket policy to the destination bucket for COS to write the output file of the inventory job to the destination bucket.
> - To call this API, ensure that you have obtained required permissions from the bucket owner to operate on the inventory jobs for the bucket. The bucket owner has such permissions by default. For the authorization directions, please see [Inventory Overview - Directions](https://intl.cloud.tencent.com/document/product/436/30622#.E4.BD.BF.E7.94.A8.E6.96.B9.E6.B3.95).
> - If you specify a prefix for the destination path of the inventory report, COS will automatically append a slash (/) to the specified prefix. For example, if you set the prefix to `Prefix`, COS will deliver the inventory report to `Prefix/inventory_report`.
> 


<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=PutBucketInventory&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                API Explorer makes it easy to make online API calls, verify signatures, generate SDK code, search for APIs, etc. You can also use it to query the content of each request as well as its response.
            </div>
        </div>
    </div>
</div>


## Request

#### Sample request

```shell
PUT /?inventory&id=inventory-configuration-ID HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
Content-MD5: MD5
```

>? 
> - In `Host: <BucketName-APPID>.cos.<Region>.myqcloud.com`, <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224)).
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> 

#### Request parameters

To call `PUT Bucket inventory`, specify the following parameter:

| Parameter | Description | Type |Required |
| ---- | ------------------------------------------------------------ | ------ | ---- |
| Id | ID of the inventory job. Default value: `None` <br>Letters, digits, hyphens (-), underscores (_), and dots (.) are supported. | String | Yes |

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).


#### Request body

You can configure the inventory job in the request body using the XML markup language. The configuration includes objects to analyze, analysis frequency, analysis dimensions, and the format and destination path of the analysis result. 

```shell
<InventoryConfiguration>
    <Id>list1</Id>
    <IsEnabled>true</IsEnabled>
    <Destination>
        <COSBucketDestination>
            <Format>CSV</Format>
            <AccountId>100000000001</AccountId>
            <Bucket>qcs::cos:ap-guangzhou::examplebucket-1250000000</Bucket>
            <Prefix>list1</Prefix>
            <Encryption>
                <SSE-COS></SSE-COS>
            </Encryption>
        </COSBucketDestination>
    </Destination>
    <Schedule>
        <Frequency>Daily</Frequency>
    </Schedule>
    <Filter>
        <Prefix>myPrefix</Prefix>
    </Filter>
    <IncludedObjectVersions>All</IncludedObjectVersions>
    <OptionalFields>
        <Field>Size</Field>
        <Field>LastModifiedDate</Field>
        <Field>ETag</Field>
        <Field>StorageClass</Field>
        <Field>IsMultipartUploaded</Field>
        <Field>ReplicationStatus</Field>
	</OptionalFields>
</InventoryConfiguration>
```

The nodes are described as follows:

| Node | Parent Node | Description | Type | Required |
| ---------------------- | ---------------------- | ------------------------------------------------------------ | --------- | -------- |
| InventoryConfiguration | None | Inventory configurations | Container | Yes |
| Id | InventoryConfiguration | Inventory ID, corresponding to the request parameter `id` | Container | Yes |
| IsEnabled | InventoryConfiguration | Whether to enable the inventory <br><li>`true`: yes <br><li>`false`: no (no inventory will be generated.) | String  | Yes   |
| IncludedObjectVersions | InventoryConfiguration | Whether to include object versions in the inventory <br><li>`All`: yes (the inventory will include all object versions and the additional fields `VersionId`, `IsLatest`, and `DeleteMarker`.)<br><li>`Current`: no | String | Yes |
| Filter  | InventoryConfiguration | Filters objects prefixed with the specified value to analyze. | Container | No |
| Prefix | Filter | Prefix of the objects to analyze | String | No |
| OptionalFields | InventoryConfiguration | Analysis dimensions to include in the inventory result | Container | No |
| Field | OptionalFields | Optional analysis dimensions, including `Size`, `LastModifiedDate`, `StorageClass`, `ETag`, `IsMultipartUploaded`, and `ReplicationStatus` | String | No |
| Schedule | InventoryConfiguration | Inventory job cycle | Container | Yes |
| Frequency | Schedule | Frequency of the inventory job. Enumerated values: `Daily`, `Weekly` | String | Yes   |
| Destination | InventoryConfiguration | Information about the inventory result destination | Container | Yes |
| COSBucketDestination | Destination | Information about the bucket that stores the exported inventory result | Container | Yes |
| Bucket | COSBucketDestination | Bucket name | String | Yes |
| AccountId | COSBucketDestination | ID of the bucket owner, for example, `100000000001` | String | No |
| Prefix | COSBucketDestination | Prefix of the inventory result | String | No |
| Format | COSBucketDestination | Format of the inventory result. Valid value: `CSV` | String | Yes |
| Encryption | COSBucketDestination | Server-side encryption for the inventory result | Container | No |
| SSE-COS | Encryption | Encryption with COS-managed key. This field can be left empty. | Container | No |

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The response body is empty.

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).


## Samples

#### Request

This sample adds an inventory job named `list1` to the `examplebucket-1250000000` bucket.
- Objects to analyze: objects prefixed with `myPrefix` and all their versions in the bucket
- Analysis frequency: daily
- Analysis dimensions: `Size`, `LastModifiedDate`, `StorageClass`, `ETag`, `IsMultipartUploaded`, and `ReplicationStatus`
- Analysis result: to be stored in the `examplebucket-1250000000` bucket as a CSV file, which is prefixed with `list1` and encrypted with SSE-COS.

```shell
PUT /?inventory&id=list1 HTTP/1.1
Date: Mon, 28 Aug 2018 02:53:38 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1503888878;1503889238&q-key-time=1503888878;1503889238&q-header-list=host&q-url-param-list=inventory&q-signature=254bf9cd3d6615e89a36ab652437f9d45c5f****
Content-MD5: AAq9nzrpsz5LJ4UEe1f6Q==
Host: examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
Content-Length: 1024

<?xml version = "1.0" encoding = "UTF-8">
<InventoryConfiguration xmlns = "http://....">
    <Id>list1</Id>
    <IsEnabled>true</IsEnabled>
    <Destination>
        <COSBucketDestination>
            <Format>CSV</Format>
            <AccountId>100000000001</AccountId>
            <Bucket>qcs::cos:ap-guangzhou::examplebucket-1250000000</Bucket>
            <Prefix>list1</Prefix>
            <Encryption>
                <SSE-COS></SSE-COS>
            </Encryption>
        </COSBucketDestination>
    </Destination>
    <Schedule>
        <Frequency>Daily</Frequency>
    </Schedule>
    <Filter>
        <Prefix>myPrefix</Prefix>
    </Filter>
    <IncludedObjectVersions>All</IncludedObjectVersions>
    <OptionalFields>
        <Field>Size</Field>
        <Field>LastModifiedDate</Field>
        <Field>ETag</Field>
        <Field>StorageClass</Field>
        <Field>IsMultipartUploaded</Field>
        <Field>ReplicationStatus</Field>
	</OptionalFields>
</InventoryConfiguration>
```

#### Response

The response below indicates that the inventory job `list1` has been successfully configured.

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Date: Mon, 28 Aug 2018 02:53:38 GMT
Server: tencent-cos
x-cos-request-id: NTlhMzg1ZWVfMjQ4OGY3MGFfMWE1NF8****
```

