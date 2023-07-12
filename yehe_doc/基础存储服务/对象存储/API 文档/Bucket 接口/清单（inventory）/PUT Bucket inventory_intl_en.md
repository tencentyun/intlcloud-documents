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
                API Explorer (recommended)
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=PutBucketInventory&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                Tencent Cloud API Explorer makes it easy for you to make online API calls, verify signatures, generate SDK code, and search for APIs. You can use it to query the request and response of each API call and generate sample SDK codes for the call.
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
> - Host: <BucketName-APPID>.cos.<Region>.myqcloud.com, where <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://www.tencentcloud.com/document/product/436/6224)).
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
        <Field>Tag</Field>
        <Field>Crc64</Field>
        <Field>x-cos-meta-*</Field>
	</OptionalFields>
</InventoryConfiguration>
```

The nodes are described as follows:

| Node | Parent Node | Description | Type | Required |
| ---------------------- | ---------------------- | ------------------------------------------------------------ | --------- | -------- |
| InventoryConfiguration | None | Inventory configurations | Container | Yes |
| Id | InventoryConfiguration | Inventory ID, corresponding to the request parameter `id` | Container | Yes |
| IsEnabled | InventoryConfiguration | Whether to enable the inventory <ul  style="margin: 0;"><li>`true`: Yes </li><li>`false`: No (no inventory will be generated.)</li></ul> | String  | Yes   |
| IncludedObjectVersions | InventoryConfiguration | Whether to include object versions in the inventory <ul  style="margin: 0;"><li>`All`: Yes (the inventory will include all object versions and the additional fields `VersionId`, `IsLatest`, and `DeleteMarker`.)</li><li>`Current`: No</li></ul> | String | Yes |
| Filter  | InventoryConfiguration | Filters objects prefixed with the specified value to analyze. | Container | No |
| And                     | Filter                  | When you filter the objects to analyze, if both conditions `Prefix` and `Tag` are required, use the `And` container.  | Container | No       |
| Prefix | And | Prefix of the objects to analyze | String | No |
| Tag                     | And                     | When you filter the objects to analyze, you can use one or multiple object tags as a filter condition.    | Container | No       |
| Period                  | Filter                  | Creation time range of the objects to analyze                                | Container | No       |
| StartTime               | Period                  | Creation start time of the objects to analyze. The parameter is a timestamp in seconds, for example, 1568688761. | String    | No       |
| EndTime                 | Period                  | Creation end time of the objects to analyze. The parameter is a timestamp in seconds, for example, 1568688762. | String    | No       |
| OptionalFields | InventoryConfiguration | Analysis items to include in the inventory result | Container | No |
| Field                   | OptionalFields          | Optional analysis items to include in the inventory result. The optional fields include `Size`, `LastModifiedDate`, `StorageClass`, `ETag`, `IsMultipartUploaded`, `ReplicationStatus`, `Tag`, `Crc64`, and `x-cos-meta-*`.<br/>Note that if `Tag` is used as a filter condition, the `Tag` field must be included in the inventory result.  <br/>In addition, custom headers in the format of `x-cos-meta-*` are supported, for example, `x-cos-meta-testheader`. If such a custom header is entered, the corresponding object metadata will be output in the inventory. If the object does not include the metadata, the field is null. | String    |No |
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

This API returns common error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Examples

#### Example 1: Adding an inventory job with a specified object prefix

#### Request

This example adds an inventory job named `list1` to the `examplebucket-1250000000` bucket.
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
      <Period>
        <StartTime>1568688761</StartTime>
        <EndTime>1568688762</EndTime>
      </Period>
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

#### Example 2: Adding an inventory job with a specified object prefix and object tag

#### Request 

This example adds an inventory job named `list2` to the `examplebucket-1250000000` bucket.

- The object (including its all versions) prefixed with `myPrefix` and tagged with {age:18} in the bucket will be analyzed.
- Analysis frequency: daily
- Analysis dimensions: `Size`, `LastModifiedDate`, `StorageClass`, `ETag`, `Tag`
- The result will be stored in the `inventorybucket-1250000000` bucket as a CSV file.

```shell
PUT /?inventory&id=list2 HTTP/1.1
Date: Mon, 28 Aug 2018 02:53:38 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1503888878;1503889238&q-key-time=1503888878;1503889238&q-header-list=host&q-url-param-list=inventory&q-signature=254bf9cd3d6615e89a36ab652437f9d45c5f****
Content-MD5: AAq9nzrpsz5LJ4UEe1f6Q==
Host: examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
Content-Length: 1024

<?xml version = "1.0" encoding = "UTF-8">
<InventoryConfiguration xmlns = "http://....">
    <Id>list2</Id>
    <IsEnabled>true</IsEnabled>
    <Destination>
        <COSBucketDestination>
            <Format>CSV</Format>
            <AccountId>100000000001</AccountId>
            <Bucket>qcs::cos:ap-guangzhou::inventorybucket-1250000000</Bucket>
        </COSBucketDestination>
    </Destination>
    <Schedule>
        <Frequency>Daily</Frequency>
    </Schedule>
    <Filter>
    	<And>
        	<Prefix>myPrefix</Prefix>
            <Tag>
                <Key>age</Key>
                <Value>18</Value>
            </Tag>
        </And>
    </Filter>
    <IncludedObjectVersions>All</IncludedObjectVersions>
    <OptionalFields>
        <Field>Size</Field>
        <Field>LastModifiedDate</Field>
        <Field>StorageClass</Field>
        <Field>ETag</Field>
        <Field>Tag</Field>
	</OptionalFields>
</InventoryConfiguration>
```

#### Response

After the request above is made, COS returns the following response, indicating that the inventory task list2 has been successfully configured.

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Date: Mon, 28 Aug 2018 02:53:38 GMT
Server: tencent-cos
x-cos-request-id: NTlhMzg1ZWVfMjQ4OGY3MGFfMWE1NF8****
```

#### Example 3: Adding an inventory job that supports outputting of custom headers of the object

#### Request 

This example adds an inventory job named `list3` to the `examplebucket-1250000000` bucket.

- The object (including its all versions) prefixed with `myPrefix` and tagged with {age:18} in the bucket will be analyzed.
- Analysis frequency: daily
- Analysis dimensions: `Size`, `LastModifiedDate`, `StorageClass`, `ETag`, `Tag`, `x-cos-meta-myheader`
- The result will be stored in the `inventorybucket-1250000000` bucket as a CSV file.

```shell
PUT /?inventory&id=list2 HTTP/1.1
Date: Mon, 28 Aug 2018 02:53:38 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1503888878;1503889238&q-key-time=1503888878;1503889238&q-header-list=host&q-url-param-list=inventory&q-signature=254bf9cd3d6615e89a36ab652437f9d45c5f****
Content-MD5: AAq9nzrpsz5LJ4UEe1f6Q==
Host: examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
Content-Length: 1024

<?xml version = "1.0" encoding = "UTF-8">
<InventoryConfiguration xmlns = "http://....">
    <Id>list3</Id>
    <IsEnabled>true</IsEnabled>
    <Destination>
        <COSBucketDestination>
            <Format>CSV</Format>
            <AccountId>100000000001</AccountId>
            <Bucket>qcs::cos:ap-guangzhou::inventorybucket-1250000000</Bucket>
        </COSBucketDestination>
    </Destination>
    <Schedule>
        <Frequency>Daily</Frequency>
    </Schedule>
    <Filter>
    	<And>
        	<Prefix>myPrefix</Prefix>
            <Tag>
                <Key>age</Key>
                <Value>18</Value>
            </Tag>
        </And>
    </Filter>
    <IncludedObjectVersions>All</IncludedObjectVersions>
    <OptionalFields>
        <Field>Size</Field>
        <Field>LastModifiedDate</Field>
        <Field>StorageClass</Field>
        <Field>ETag</Field>
        <Field>Tag</Field>
        <Field>Crc64</Field>
        <Field>x-cos-meta-myheader</Field>
	</OptionalFields>
</InventoryConfiguration>
```

#### Response

After the request above is made, COS returns the following response, indicating that the inventory job list3 has been successfully configured.

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Date: Mon, 28 Aug 2018 02:53:38 GMT
Server: tencent-cos
x-cos-request-id: NTlhMzg1ZWVfMjQ4OGY3MGFfMWE1NF8****
```
