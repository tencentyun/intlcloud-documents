## Overview

This API is used to query an inventory job of a bucket. When calling this API, you need to specify the inventory job ID and carry a request signature. For more information, please see [Inventory Overview](https://intl.cloud.tencent.com/document/product/436/30622).

> !
> - To call this API, ensure that you have the necessary permission on the bucket inventory job.
> - The bucket owner has such permission by default. If you do not have the permission, you can request it from the bucket owner.
> - If you specify a prefix for the destination path of the inventory report, COS will automatically append a slash (/) to the specified prefix. For example, if you set the prefix to `Prefix`, COS will deliver the inventory report to `Prefix/inventory_report`.
> 

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer (recommended)
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=GetBucketInventory&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Debug</a>
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
GET /?inventory&id=inventory-configuration-ID HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>? 
> - Host: <BucketName-APPID>.cos.<Region>.myqcloud.com, where <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://www.tencentcloud.com/document/product/436/6224)).
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> 

#### Request parameters

To call `GET Bucket inventory`, specify the following parameter:

| Parameter | Description | Type |Required |
| ---- | ------------------------------------------------------------ | ------ | ---- |
| Id | ID of the inventory job. Default value: `None` <br/>Letters, digits, hyphens (-), underscores (_), and dots (.) are supported. | String | Yes |

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).


#### Request body

The request body of this request is empty.

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).


#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```shell
<InventoryConfiguration>
    <Id>list1</Id>
    <IsEnabled>true</IsEnabled>
    <Destination>
        <COSBucketDestination>
            <Format>CSV</Format>
            <AccountId>1250000000</AccountId>
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

| Node | Parent Node | Description | Type |
| ----------------------- | ----------------------- | ------------------------------------------------------------ | --------- |
| InventoryConfiguration | None | Inventory configuration | Container |
| Id | InventoryConfiguration | Inventory ID, corresponding to the request parameter `Id` | Container |
| IsEnabled | InventoryConfiguration | Whether the inventory is enabled <ul  style="margin: 0;"><li>`true`: Yes</li><li>`false`: No (no inventory will be generated.)</li></ul> | String |
| IncludedObjectVersions | InventoryConfiguration | Whether object versions are included in the inventory <ul  style="margin: 0;"><li>`All`: Yes (the inventory includes all object versions and the additional fields `VersionId`, `IsLatest`, and `DeleteMarker`.)</li><li>`Current`: No</li></ul> | String |
| Filter  | InventoryConfiguration | Filters objects prefixed with the specified value to analyze. | Container |
| And                     | Filter                  | When you filter the objects to analyze, if both conditions `Prefix` and `Tag` are required, use the `And` container.  | Container |
| Prefix | And | Prefix of the objects to analyze | String |
| Tag                     | And                     | When you filter the objects to analyze, you can use one or multiple object tags as a filter condition.    | Container |
| Period                  | Filter                  | Creation time range of the objects to analyze                                | Container |
| StartTime               | Period                  | Creation start time of the objects to analyze. The parameter is a timestamp in seconds, for example, 1568688761. | String    |
| EndTime                 | Period                  | Creation end time of the objects to analyze. The parameter is a timestamp in seconds, for example, 1568688762. | String    |
| OptionalFields | InventoryConfiguration | Analysis dimensions to include in the inventory result | Container |
| Field                   | OptionalFields          | Optional analysis items to include in the inventory result. The optional fields include `Size`, `LastModifiedDate`, `StorageClass`, `ETag`, `IsMultipartUploaded`, `ReplicationStatus`, `Tag`, `Crc64`, and `x-cos-meta-*`.<br/>Note that if `Tag` is used as a filter condition, the `Tag` field must be included in the inventory result. <br/>In addition, custom headers in the format of `x-cos-meta-*` are supported, for example, `x-cos-meta-testheader`. If such a custom header is entered, the corresponding object metadata will be output in the inventory. If the object does not include the metadata, the field is null. | String    |
| Schedule | InventoryConfiguration | Inventory job cycle | Container |
| Frequency | Schedule | Frequency of the inventory job, which can be daily or weekly | String |
| Destination | InventoryConfiguration | Information about the inventory result destination | Container |
| COSBucketDestination | Destination | Information about the bucket that stores the exported inventory result | Container |
| Bucket | COSBucketDestination | Bucket name | String |
| AccountId | COSBucketDestination | ID of the bucket owner | String |
| Prefix | COSBucketDestination | Prefix of the inventory result | String |
| Format | COSBucketDestination | Format of the inventory result. Valid values: `CSV`, `ORC` | String |
| Encryption | COSBucketDestination | Server-side encryption for the inventory result | Container |
| SSE-COS | Encryption | Encryption with COS-managed key | Container |

#### Error codes

This API returns common error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Examples

#### Example 1: Obtaining an inventory job with a specified object prefix

#### Request

The following example queries the `list1` inventory job configuration of the `examplebucket-1250000000` bucket:

```shell
GET /?inventory&id=list1 HTTP/1.1
Date: Mon, 28 Aug 2018 02:53:38 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1503895278;1503895638&q-key-time=1503895278;1503895638&q-header-list=host&q-url-param-list=inventory&q-signature=f77900be432072b16afd8222b4b349aabd83****
Host: examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
```

#### Response

After the request above is made, COS returns the following response, indicating that the inventory job `list1` is currently enabled in the bucket:
- Objects to analyze: objects prefixed with `myPrefix` and all their versions in the `examplebucket-1250000000` bucket
- Analysis frequency: daily
- Analysis dimensions: `Size`, `LastModifiedDate`, `StorageClass`, `ETag`, `IsMultipartUploaded`, and `ReplicationStatus`
- Analysis result: to be stored in the `examplebucket-1250000000` bucket as a CSV file, which is prefixed with `list1` and encrypted with SSE-COS.

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 331
Date: Mon, 28 Aug 2018 02:53:39 GMT
Server: tencent-cos
x-cos-request-id: NTlhMzg1ZWVfMjQ4OGY3MGFfMWE1NF84Y2M
<?xml version = "1.0" encoding = "UTF-8">
<InventoryConfiguration xmlns = "http://....">
    <Id>list1</Id>
    <IsEnabled>true</IsEnabled>
    <Destination>
        <COSBucketDestination>
            <Format>CSV</Format>
            <AccountId>1250000000</AccountId>
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

#### Example 2: Obtaining an inventory job with a specified object prefix and object tag

#### Request

The following example queries the `list2` inventory job configuration of the `examplebucket-1250000000` bucket:

```shell
GET /?inventory&id=list2 HTTP/1.1
Date: Mon, 28 Aug 2018 02:53:38 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1503895278;1503895638&q-key-time=1503895278;1503895638&q-header-list=host&q-url-param-list=inventory&q-signature=f77900be432072b16afd8222b4b349aabd83****
Host: examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
```

#### Response

After the request above is made, COS returns the following response indicating that the inventory job list2 is currently enabled in the bucket.

- Objects to analyze: objects prefixed with `myPrefix` and tagged with `{age:18}` and all their versions in the `examplebucket-1250000000` bucket
- Analysis frequency: daily
- Analysis dimensions: `Size`, `LastModifiedDate`, `StorageClass`, `ETag`, and `Tag`
- The result will be stored in the `inventorybucket-1250000000` bucket as a CSV file.

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 331
Date: Mon, 28 Aug 2018 02:53:39 GMT
Server: tencent-cos
x-cos-request-id: NTlhMzg1ZWVfMjQ4OGY3MGFfMWE1NF84Y2M
<?xml version = "1.0" encoding = "UTF-8">
<InventoryConfiguration xmlns = "http://....">
    <Id>list2</Id>
    <IsEnabled>true</IsEnabled>
    <Destination>
        <COSBucketDestination>
            <Format>CSV</Format>
            <AccountId>1250000000</AccountId>
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
