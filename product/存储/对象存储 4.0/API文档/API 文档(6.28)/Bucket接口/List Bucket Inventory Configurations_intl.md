## Feature Description

List Bucket Inventory Configurations is used to request that all inventory tasks in a bucket be returned. Up to 1,000 inventory tasks can be configured in one bucket.  

This request supports list pagination, i.e., returning up to 100 inventory tasks per page at a time. Check the value of the IsTruncated node in the request. If IsTruncated is false, all inventory tasks in the bucket have been listed. If IsTruncated is true and there is a parameter value in the NextContinuationToken node, you can pass this value to the continuation-token node to get the inventory task information of the next page. For more information of the inventory feature, see [Inventory Feature Overview](https://intl.cloud.tencent.com/document/product/436/30622).

>  When calling this request, make sure that you have sufficient permission to manipulate the bucket's inventory tasks, which is granted to the bucket owner by default. If you do not have it, apply for it to the bucket owner first.

## Request

### Request Example

```shell
GET /?inventory HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).

### Request Parameter

The request parameter is in the following format:

| Parameter | Description | Type | Required |
| ------------------ | ------------------------------------------------------------ | ------ | ---- |
| continuation-token | If IsTruncated in the COS response body is true and there is a parameter value in the NextContinuationToken node, you can use this parameter as the parameter value of continuation-token to get the inventory task information of the next page <br>Default value: None | String | No |

### Request Header

#### Common Header

The implementation of this request operation uses a common request header. For more information about the public request header, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

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
<ListInventoryConfigurationResult>
    <InventoryConfiguration>
        <Id>list1</Id>
        <IsEnabled>True</IsEnabled>
        <Destination>
            <COSBucketDestination>
                <Format>CSV</Format>
                <AccountId>1250000000</AccountId>
                <Bucket>qcs::cos:ap-beijing::examplebucket-1250000000</Bucket>
                <Prefix>list1</Prefix>
                <SSE-COS></SSE-COS>
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
            <Field>IsMultipartUpload</Field>
            <Field>ReplicationStatus</Field>
        </OptionalFields>
    </InventoryConfiguration>
    <InventoryConfiguration>
        <Id>list2</Id>
        <IsEnabled>True</IsEnabled>
        <Destination>
            <COSBucketDestination>
                <Format>CSV</Format>
                <AccountId>1250000000</AccountId>
                <Bucket>qcs::cos:ap-beijing::examplebucket-1250000000</Bucket>
                <Prefix>list2</Prefix>
                <SSE-COS></SSE-COS>
            </COSBucketDestination>
        </Destination>
        <Schedule>
            <Frequency>Weekly</Frequency>
        </Schedule>
        <Filter>
            <Prefix>myPrefix2</Prefix>
        </Filter>
        <IncludedObjectVersions>All</IncludedObjectVersions>
        <OptionalFields>
            <Field>Size</Field>
            <Field>LastModifiedDate</Field>
            <Field>ETag</Field>
            <Field>StorageClass</Field>
        </OptionalFields>
    </InventoryConfiguration>
    <IsTruncated>false</IsTruncated>
    ------If ContinuationToken was provided in the request---
    <ContinuationToken>...</ContinuationToken>
    <IsTruncated>true</IsTruncated>
    <NextContinuationToken>1ueSDFASDF1Tr/XDAFdadEADadf2J/wm36Hy4vbOwM=</NextContinuationToken>
</ListInventoryConfigurationResult>
```

The content is described in details below:

| Node name | Parent node | Description | Type |
| ------------------------------------ | ----------------------------------- | ------------------------------------------------------------ | --------- |
| List Inventory Configuration Results | None | List of all inventory tasks in the bucket | Container |
| Inventory Configuration | ListInventory Configuration Results | Details of the inventory tasks. See [GET Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30623) for the XML structure | Container |
| IsTruncated | ListInventory Configuration Results | Flag about whether all inventory tasks have been listed. If yes, it is false; otherwise, it is true | Boolean |
| Continuation Token | ListInventory Configuration Results | Flag of the inventory list on the current page, which can be understood as the page number. It corresponds to the continuation-token parameter in the request | String |
| NextContinuation Token | ListInventory Configuration Results | Flag of the next page of inventory list. If there is a value in this parameter, the value can be used as the continuation-token parameter to initiate a GET request to get the inventory task information of the next page | String |

## Error Codes

This request does not generate special error messages. For common error codes, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Use Case

### Request

The following request sample shows the configuration information for getting the inventory task list1 from the bucket examplebucket-1250000000.

```shell
GET /?inventory HTTP/1.1
Date: Mon, 28 Aug 2018 02:53:38 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98JM&q-sign-time=1503895278;1503895638&q-key-time=1503895278;1503895638&q-header-list=host&q-url-param-list=inventory&q-signature=f77900be432072b16afd8222b4b349aabd837cb9
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
```

### Response

After the request is made, COS returns the following response indicating that currently there are inventory tasks list1 and list2 in the bucket.  

**Inventory task list1**

Analyze the objects prefixed with myPrefix in the bucket examplebucket-1250000000 and all their versions.
The frequency of analysis is once a day.
Analysis dimensions include Size, LastModifiedDate, StorageClass, ETag, IsMultipartUploaded, and ReplicationStatus.
The analysis result is stored in the bucket examplebucket-1250000000 as a CSV file, which is prefixed with list1 and encrypted with SSE-COS.  

**Inventory task list2**

Analyze the objects prefixed with myPrefix2 in the bucket examplebucket-1250000000 and all their versions.
The frequency of analysis is once a week. The analysis dimensions include Size, LastModifiedDate, StorageClass, and ETag.
The analysis result is stored in the bucket examplebucket-1250000000 as a CSV file, which is prefixed with list2 and encrypted with SSE-COS.  

Suppose there are 100 inventory tasks on this page. If IsTruncated is true, COS will further return NextContinuationToken, whose value can be used as the parameter of continuation-token in the GET request to get the next page of information.

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 331
Date: Mon, 28 Aug 2018 02:53:39 GMT
Server: tencent-cos
x-cos-request-id: NTlhMzg1ZWVfMjQ4OGY3MGFfMWE1NF84Y2M
<?xml version = "1.0" encoding = "UTF-8">
<ListInventoryConfigurationResult xmlns = "http://....">
    <InventoryConfiguration>
        <Id>list1</Id>
        <IsEnabled>True</IsEnabled>
        <Destination>
            <COSBucketDestination>
                <Format>CSV</Format>
                <AccountId>1250000000</AccountId>
                <Bucket>qcs::cos:ap-beijing::examplebucket-1250000000</Bucket>
                <Prefix>list1</Prefix>
                <SSE-COS></SSE-COS>
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
            <Field>IsMultipartUpload</Field>
            <Field>ReplicationStatus</Field>
        </OptionalFields>
    </InventoryConfiguration>
    <InventoryConfiguration>
        <Id>list2</Id>
        <IsEnabled>True</IsEnabled>
        <Destination>
            <COSBucketDestination>
                <Format>CSV</Format>
                <AccountId>1250000000</AccountId>
                <Bucket>qcs::cos:ap-beijing::examplebucket-1250000000</Bucket>
                <Prefix>list2</Prefix>
                <SSE-COS></SSE-COS>
            </COSBucketDestination>
        </Destination>
        <Schedule>
            <Frequency>Weekly</Frequency>
        </Schedule>
        <Filter>
            <Prefix>myPrefix2</Prefix>
        </Filter>
        <IncludedObjectVersions>All</IncludedObjectVersions>
        <OptionalFields>
            <Field>Size</Field>
            <Field>LastModifiedDate</Field>
            <Field>ETag</Field>
            <Field>StorageClass</Field>
        </OptionalFields>
    </InventoryConfiguration>
    <IsTruncated>false</IsTruncated>
    ------If ContinuationToken was provided in the request---
    <ContinuationToken>...</ContinuationToken>
    <IsTruncated>true</IsTruncated>
    <NextContinuationToken>1ueSDFASDF1Tr/XDAFdadEADadf2J/wm36Hy4vbOwM=</NextContinuationToken>
</ListInventoryConfigurationResult>
```

