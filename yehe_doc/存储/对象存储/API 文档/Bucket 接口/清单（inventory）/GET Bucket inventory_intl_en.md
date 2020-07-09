## Description

This API is used to query inventory jobs for a bucket. To initiate this request, you need to provide the ID of an inventory job and a signature to authenticate the request. For more information, see [Inventory Overview](https://intl.cloud.tencent.com/document/product/436/30622).

> !
> - To call this API, make sure that you have adequate permission for inventory jobs of the bucket.
> - The bucket owner has such permission by default. If you do not have it, apply for it to the bucket owner first.
> - If you specify a prefix for inventory delivery, the COS backend will automatically add `/` behind the prefix. For example, if you specify `Prefix` as the prefix, an inventory report will be delivered to the path `Prefix/inventory_report`.

## Request

#### Sample request

```shell
GET /?inventory&id=inventory-configuration-ID HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>?Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).

#### Request parameters

To call this API requires the following parameter:

| Parameter Name | Description | Type | Required |
| ---- | ------------------------------------------------------------ | ------ | ---- |
| id   | ID of the inventory job. Default value: None<br/>Valid characters: `a-z, A-Z, 0-9, -, _, .`| String | Yes   |

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
	</OptionalFields>
</InventoryConfiguration>
```

The nodes are described in details below:

| Node Name | Parent Node | Description | Type |
| ----------------------- | ----------------------- | ------------------------------------------------------------ | --------- |
| Inventory Configuration | None | Contains configuration parameters of the inventory | Container |
| Id | Inventory Configuration | Inventory name, corresponding to the ID in the request parameters | Container |
| IsEnabled               | Inventory Configuration | Indicates whether to enable inventory:<br><li>`true`: enabled<br><li>`false`: disabled | String    |
| IncludedObject Versions | Inventory Configuration | Indicates whether to include object versions in the inventory:<br>`All`: the inventory will include all object versions and add the `VersionId`, `IsLatest`, and `DeleteMarker` fields<br>`Current`: the inventory includes no object version | String |
| Filter                  | Inventory Configuration | Filters objects to be analyzed based on the prefix set in `Filter` | Container |
| Prefix | Filter | Prefix of the objects to be analyzed | String |
| OptionalFields | Inventory Configuration | Sets the analysis dimensions that should be included in the inventory result | Container |
| Field | OptionalFields | Analysis dimension fields that can be optionally included in the inventory result. Valid values: Size, LastModifiedDate, StorageClass, ETag, IsMultipartUploaded, and ReplicationStatus | String |
| Schedule | Inventory Configuration | Configures the inventory job cycle | Container |
| Frequency | Schedule | Inventory job cycle. Options include daily and weekly | String |
| Destination | Inventory Configuration | Storage destination for the inventory result | Container |
| COSBucket Destination | Destination | Destination bucket where the exported inventory result is stored | Container |
| Bucket | COSBucket Destination | Name of the bucket where the inventory result is stored | String |
| AccountId | COSBucket Destination | ID of the bucket owner | String |
| Prefix | COSBucket Destination | Prefix of the inventory result | String |
| Format | COSBucket Destination | File format of the inventory result. Valid values: CSV, OCR | String |
| Encryption | COSBucket Destination | Provides an option of server-side encryption for the inventory result | Container |
| SSE-COS | Encryption | Encryption with COS-managed key | Container |

#### Error codes

This API returns uniform error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

#### Request

The following sample request shows how to get the configuration of the inventory job list1 from the bucket `examplebucket-1250000000`.

```shell
GET /?inventory&id=list1 HTTP/1.1
Date: Mon, 28 Aug 2018 02:53:38 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1503895278;1503895638&q-key-time=1503895278;1503895638&q-header-list=host&q-url-param-list=inventory&q-signature=f77900be432072b16afd8222b4b349aabd83****
Host: examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
```

#### Response

If the request above succeeds, COS returns the following response indicating that the inventory job list1 is currently enabled for the bucket.
- This inventory job analyzes the objects prefixed with `myPrefix` and all their versions in the bucket `examplebucket-1250000000`.
- The analysis frequency is once a day.
- Analysis dimensions include Size, LastModifiedDate, StorageClass, ETag, IsMultipartUploaded, and ReplicationStatus.
- The analysis result is stored in the bucket `examplebucket-1250000000` as a CSV file, which is prefixed with `list1` and encrypted with SSE-COS.

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
