## Feature Description

PUT Bucket inventory is used to create an inventory task in a bucket. You can use this request to create an inventory task after naming it. For more information, see [Inventory Feature Overview](https://intl.cloud.tencent.com/document/product/436/30622).

>
> - Up to 1,000 inventory tasks can be configured in one COS bucket.
> - You must write a bucket policy to the destination bucket for COS to put the result file of the inventory task in it.
> - When calling this request, make sure that you have sufficient permission to manipulate the bucket's inventory tasks, which is granted to the bucket owner by default. If you do not have it, apply for it to the bucket owner first.  

## Request

### Request Example

```shell
PUT /?inventory&id=inventory-configuration-ID HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
Content-MD5: MD5
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).

### Request Parameter

Calling PUT Bucket inventory requires the inventory task name parameter. The parameter is in the following format:

| Parameter | Description | Type | Required |
| ---- | ------------------------------------------------------------ | ------ | ---- |
| id | Name of the inventory task. <br>Default value: None <br>Valid characters: `a-z，A-Z，0-9，-，_，.` | String | Yes |

### Request Header

#### Common Header

The implementation of this request operation uses a common request header. For more information about the common request header, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Non-common Header

This request operation has no special request headers.

### Request Body

You can use the XML language to set specific configuration information for the inventory task in the request body, including the objects to be analyzed by the inventory task, frequency of analysis, analysis dimensions, format of analysis result, and storage location. 

```shell
<InventoryConfiguration>
    <Id>list1</Id>
    <IsEnabled>True</IsEnabled>
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

The content is described in details below:

| Node name | Parent node | Description | Type | Required |
| ---------------------- | ---------------------- | ------------------------------------------------------------ | --------- | -------- |
| InventoryConfiguration | None | This contains configuration parameters of the inventory | Container | Yes |
| Id | InventoryConfiguration | Inventory name, corresponding to the id in the request parameter | Container | Yes |
| IsEnabled | InventoryConfiguration | Flag about whether the inventory is enabled. If this is set to True, the inventory is enabled; if False, no inventories will be generated | String | Yes |
| IncludedObjectVersions | InventoryConfiguration | Whether to include object versions in the inventory <br>If this is set to All, the inventory will include all object versions and add VersionId, IsLatest, and DeleteMarker fields <br>If Current, no object version information will be included in the inventory | String | Yes |
| Filter | InventoryConfiguration | This filters the objects to be analyzed. The inventory feature will analyze the objects that match the prefix set in Filter | Container | No |
| Prefix | Filter | Prefix of the objects to be analyzed | String | No |
| OptionalFields | InventoryConfiguration | This sets the analysis items that should be included in the inventory result | Container | No |
| Field | OptionalFields | Name of the analysis items that can be optionally included in the inventory result. Optional fields include Size, LastModifiedDate, StorageClass, ETag, IsMultipartUploaded, and ReplicationStatus | String | No |
| Schedule | InventoryConfiguration | This configures the inventory task cycle | Container | Yes |
| Frequency | Schedule | Inventory task cycle. Options include daily and weekly | String | Yes |
| Destination | InventoryConfiguration | This describes the information of the inventory result storage | Container | Yes |
| COSBucketDestination | Destination | Information of the bucket where the inventory result is stored after export | Container | Yes |
| Bucket | COSBucketDestination | Name of the bucket where the inventory result is stored | String | Yes |
| AccountId | COSBucketDestination | ID of the bucket owner such as 100000000001 | String | No |
| Prefix | COSBucketDestination | Prefix of the inventory result | String | No |
| Format | COSBucketDestination | File format of the inventory result. CSV is available | String | Yes |
| Encryption | COSBucketDestination | Option to provide server-side encryption for the inventory result | Container | No |
| SSE-COS | Encryption | Encryption with COS-managed key. This can be left blank | Container | No |

## Response

### Response Header

#### Common Response Header 

This response uses a common response header. For more information about the common response header, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Special Response Header

The response to this request has no special response headers.

### Response Body

The response body return of this request is empty.

### Error Codes

Some frequent special errors that may occur with this request are listed below. For common error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

| Error code | Description | Status code |
| --------------------- | ---------------------------------------------- | -------------------- |
| InvalidArgument | Invalid parameter value | HTTP 400 Bad Request |
| TooManyConfigurations | The number of inventories has reached the upper limit of 1,000 | HTTP 400 Bad Request |
| AccessDenied | Unauthorized access. You probably do not have access to the bucket | HTTP 403 Forbidden |

## Use Case

### Request

This example adds an inventory task named list1 to the bucket examplebucket-1250000000.
This inventory task analyzes the objects prefixed with myPrefix in the bucket and all their versions.
The frequency of analysis is once a day.
Analysis dimensions include Size, LastModifiedDate, StorageClass, ETag, IsMultipartUploaded, and ReplicationStatus.
The analysis result is stored in the bucket examplebucket-1250000000 as a CSV file, which is prefixed with list1 and encrypted with SSE-COS.

```shell
PUT /?inventory&id=list1 HTTP/1.1
Date: Mon, 28 Aug 2018 02:53:38 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98JM&q-sign-time=1503888878;1503889238&q-key-time=1503888878;1503889238&q-header-list=host&q-url-param-list=inventory&q-signature=254bf9cd3d6615e89a36ab652437f9d45c5f63f9
Content-MD5: AAq9nzrpsz5LJ4UEe1f6Q==
Host: examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
Content-Length: 1024

<?xml version = "1.0" encoding = "UTF-8">
<InventoryConfiguration xmlns = "http://....">
    <Id>list1</Id>
    <IsEnabled>True</IsEnabled>
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

### Response

After the request above is made, COS returns the following response, indicating that the inventory task list1 has been successfully configured.

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 0
Date: Mon, 28 Aug 2018 02:53:38 GMT
Server: tencent-cos
x-cos-request-id: NTlhMzg1ZWVfMjQ4OGY3MGFfMWE1NF84Y2M
```
