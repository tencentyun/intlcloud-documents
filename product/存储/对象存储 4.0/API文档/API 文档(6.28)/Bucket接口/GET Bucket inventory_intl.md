## Feature Description

The GET Bucket inventory API is used to query the inventory task information in a bucket. When initiating this request, you need to provide the name of the inventory task and get the request signature to indicate that the request has been authorized. For more information of the inventory feature, see [Inventory Feature Overview](https://intl.cloud.tencent.com/document/product/436/30622).

>
> - When calling this request, make sure that you have sufficient permission to manipulate the bucket's inventory tasks.
> - This permission is granted to the bucket owner by default. If you do not have it, apply for it to the bucket owner first.  

## Request

### Request Example

```shell
GET /?inventory&id=inventory-configuration-ID HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).

### Request Parameter

Calling Get Bucket inventory requires the inventory task name parameter. The parameter is in the following format:

| Parameter | Description | Type | Required |
| ---- | ------------------------------------------------------------ | ------ | ---- |
| id | Name of the inventory task. Default value: None <br />Valid characters: `a-z，A-Z，0-9，-，_，. ` | String | Yes   |

### Request Header

#### Common Header

The implementation of this request operation uses a common request header. For more information about the common request header, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Non-common Header

This request operation has no special request headers.

### Request Body

The request body of this request is empty.

## Response

### Response Header

#### Common Response Header 

This response uses a common response header. For more information about the common response header, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Special Response Header

This response has no special response headers.

### Response Body

The return of this response body is **application/xml** data. Below is an example containing all the node data:

```shell
<InventoryConfiguration>
    <Id>list1</Id>
    <IsEnabled>True</IsEnabled>
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

The content is described in details below:

| Node name | Parent node | Description | Type |
| ----------------------- | ----------------------- | ------------------------------------------------------------ | --------- |
| Inventory Configuration | None | This contains configuration parameters of the inventory | Container |
| Id | Inventory Configuration | Inventory name, corresponding to the ID in the request parameter | Container |
| IsEnabled | Inventory Configuration | Flag about whether the inventory is enabled. If this is set to True, the inventory is enabled; if False, no inventories will be generated | String |
| IncludedObject Versions | Inventory Configuration | Whether to include object versions in the inventory. If this is set to All, the inventory will include all object versions and add VersionId, IsLatest, and DeleteMarker fields; if Current, no object version information will be included in the inventory | String |
| Filter | Inventory Configuration | This filters the objects to be analyzed. The inventory feature will analyze the objects that match the prefix set in Filter | Container |
| Prefix | Filter | Prefix of the objects to be analyzed | String |
| OptionalFields | Inventory Configuration | This sets the analysis dimensions that should be included in the inventory result | Container |
| Field | OptionalFields | Name of the analysis dimension that can be optionally included in the inventory result. Optional fields include Size, LastModifiedDate, StorageClass, ETag, IsMultipartUploaded, and ReplicationStatus | String |
| Schedule | Inventory Configuration | This configures the inventory task cycle | Container |
| Frequency | Schedule | Inventory task cycle. Options include daily and weekly | String |
| Destination | Inventory Configuration | This describes the information of the inventory result storage | Container |
| COSBucket Destination | Destination | Information of the bucket where the inventory result is stored after export | Container |
| Bucket | COSBucket Destination | Name of the bucket where the inventory result is stored | String |
| AccountId | COSBucket Destination | ID of the bucket owner | String |
| Prefix | COSBucket Destination | Prefix of the inventory result | String |
| Format | COSBucket Destination | File format of the inventory result. CSV and OCR are available | String |
| Encryption | COSBucket Destination | Option to provide server-side encryption for the inventory result | Container |
| SSE-COS | Encryption | Encryption with COS-managed key | Container |

## Error Codes

This request does not generate special error messages. For common error codes, see [Error Codes](https://cloud.tencent.com/document/product/436/7730).

## Use Case

### Request

The following request sample shows the configuration information for getting the inventory task list1 from the bucket examplebucket-1250000000.

```shell
GET /?inventory&id=list1 HTTP/1.1
Date: Mon, 28 Aug 2018 02:53:38 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98JM&q-sign-time=1503895278;1503895638&q-key-time=1503895278;1503895638&q-header-list=host&q-url-param-list=inventory&q-signature=f77900be432072b16afd8222b4b349aabd837cb9
Host: examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
```

### Response

After the request above is made, COS returns the following response indicating that the inventory task list1 is currently enabled in the bucket.
This inventory task analyzes the objects prefixed with myPrefix in the bucket examplebucket-1250000000 and all their versions.
The frequency of analysis is once a day.
Analysis dimensions include Size, LastModifiedDate, StorageClass, ETag, IsMultipartUploaded, and ReplicationStatus.
The analysis result is stored in the bucket examplebucket-1250000000 as a CSV file, which is prefixed with list1 and encrypted with SSE-COS.

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
    <IsEnabled>True</IsEnabled>
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