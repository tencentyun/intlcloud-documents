## Description

This API is used to create an inventory job for a bucket after you created an inventory job ID. For more information, see [Inventory Overview](https://intl.cloud.tencent.com/document/product/436/30622).

> !
> - Up to 1,000 inventory jobs can be configured on one COS bucket.
> - You must write a bucket policy to the destination bucket for COS to put the result files of inventory jobs into it.
> - To call this operation, make sure that you have adequate access permission for the bucket's inventory jobs. The bucket owner has such permission by default. If you do not have it, apply for it to the bucket owner first.  
> - If you specify a prefix for inventory delivery, COS will automatically add `/` behind the prefix. Assume you specify `Prefix` as the prefix, then COS will deliver inventory reports to the path `Prefix/inventory_report`.

## Request

#### Sample request

```shell
PUT /?inventory&id=inventory-configuration-ID HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
Content-MD5: MD5
```

>?Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).

#### Request parameters

To call this API requires the ID of the inventory job.

| Parameter Name | Description | Type | Required |
| ---- | ------------------------------------------------------------ | ------ | ---- |
| id   | ID of the inventory job. Default value: None<br/>Valid values: `a-z, A-Z, 0-9, -, _, .`| String | Yes   |

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).


#### Request body

You can specify the configuration for the inventory job in the request body using XML language, including objects to be analyzed, analysis frequency and dimension, and format and storage location of analysis result. 

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

The nodes are described in details below:

| Node Name | Parent Node | Description | Type | Required |
| ---------------------- | ---------------------- | ------------------------------------------------------------ | --------- | -------- |
| InventoryConfiguration | None | Contains configuration parameters of the inventory | Container | Yes |
| Id | InventoryConfiguration | Inventory ID, corresponding to the ID in the request parameter | Container | Yes |
| IsEnabled              | InventoryConfiguration | Indicates whether to enable inventory:<br><li>`true`: enabled<br><li>`false`: disabled | String    | Yes       |
| IncludedObjectVersions | InventoryConfiguration | Indicates whether to include object versions in the inventory<br>`All`: the inventory will include all object versions and add the `VersionId`, `IsLatest`, and `DeleteMarker` fields<br>`Current`: the inventory will include no object version | String | Yes |
| Filter                 | InventoryConfiguration | Filters objects to analyze. Only objects with the prefix specified in `Filter` are to be analyzed | Container | No       |
| Prefix | Filter | Prefix of the objects to be analyzed | String | No |
| OptionalFields | InventoryConfiguration | Analysis dimensions that should be included in the inventory result | Container | No |
| Field | OptionalFields | Analysis dimensions that can be optionally included in the inventory result. Valid values: Size, LastModifiedDate, StorageClass, ETag, IsMultipartUploaded, and ReplicationStatus | String | No |
| Schedule | InventoryConfiguration | Configures the inventory job schedule | Container | Yes |
| Frequency | Schedule | Inventory job frequency. Enumerated values: Daily, Weekly | String | Yes |
| Destination | InventoryConfiguration | The destination where the inventory result is stored | Container | Yes |
| COSBucketDestination | Destination | The destination bucket where the inventory result is stored after export | Container | Yes |
| Bucket | COSBucketDestination | Name of the bucket where the inventory result is stored | String | Yes |
| AccountId | COSBucketDestination | ID of the bucket owner such as 100000000001 | String | No |
| Prefix | COSBucketDestination | Prefix of the inventory result | String | No |
| Format | COSBucketDestination | Format of the inventory result file. Valid value: CSV | String | Yes |
| Encryption | COSBucketDestination | Provides an option of server-side encryption for the inventory result | Container | No |
| SSE-COS | Encryption | Encryption with COS-managed key. This can be left blank | Container | No |

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

This request returns an empty response body.

#### Error codes

This API returns uniform error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).


## Samples

#### Request

This example adds an inventory job named list1 to the bucket `examplebucket-1250000000`.
- This inventory job analyzes the objects prefixed with `myPrefix` and all their versions in the bucket.
- The frequency of analysis is once a day.
- Analysis dimensions include Size, LastModifiedDate, StorageClass, ETag, IsMultipartUploaded, and ReplicationStatus.
- The analysis result is stored in the bucket `examplebucket-1250000000` as a CSV file, which is prefixed with `list1` and encrypted with SSE-COS.

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

After the request above is made, COS returns the following response, indicating that the inventory job `list1` has been successfully configured.

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Date: Mon, 28 Aug 2018 02:53:38 GMT
Server: tencent-cos
x-cos-request-id: NTlhMzg1ZWVfMjQ4OGY3MGFfMWE1NF8****
```

