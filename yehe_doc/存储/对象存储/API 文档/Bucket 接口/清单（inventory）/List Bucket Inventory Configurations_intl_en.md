## Description

This API is used to request all inventory jobs (up to 1,000) configured on a bucket.  

This request supports pagination, with up to 100 inventory jobs listed per page. Please note the value of the `IsTruncated` node in the request:
- `false` indicates that all inventory jobs for the bucket have been listed.
- If `IsTruncated` is true and the `NextContinuationToken` node has been assigned with a value, you can pass that value to the `continuation-token` node to get the next page of inventory jobs.

For more information, please see [Inventory Overview](https://intl.cloud.tencent.com/document/product/436/30622).

>!To call this API, make sure that you have adequate access permission for the bucket's inventory jobs. The bucket owner has such permission by default. If you do not have it, apply for it to the bucket owner first.

## Request

#### Sample request

```shell
GET /?inventory HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>?Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).

#### Request parameters

The request parameters are detailed as below:

| Parameter Name | Description | Type | Required |
| ------------------ | ------------------------------------------------------------ | ------ | ---- |
| continuation-token | If `IsTruncated` is true in the response body, and the `NextContinuationToken` node has been assigned with a value, you can pass that value to this node to get the next page of inventory jobs.<br>Default value: None | String | No |

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

The nodes are described in details below:

| Node Name | Parent Node | Description | Type |
| ------------------------------------ | ----------------------------------- | ------------------------------------------------------------ | --------- |
| List Inventory Configuration Results | None | List of all inventory jobs in the bucket | Container |
| Inventory Configuration | ListInventory Configuration Results | Details of the inventory jobs. See [GET Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30623) for the XML structure | Container |
| IsTruncated | ListInventory Configuration Results | A flag that indicates whether all inventory jobs have been listed. `false`: yes; `true`: no  | Boolean   |
| Continuation Token | ListInventory Configuration Results | Identifies the current page for inventory listing; can be understood as the page number. It corresponds to the `continuation-token` in the request | String    |
| NextContinuation Token               | ListInventory Configuration Results | Identifies the next page for inventory listing. If this parameter has a value, you can pass it to the `continuation-token` in the subsequent GET request for the next page of inventory jobs | String    |

#### Error codes

This API returns uniform error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

#### Request

The following request sample shows how to get the inventory job list1 from the bucket `examplebucket-1250000000`.

```shell
GET /?inventory HTTP/1.1
Date: Mon, 28 Aug 2018 02:53:38 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98JM&q-sign-time=1503895278;1503895638&q-key-time=1503895278;1503895638&q-header-list=host&q-url-param-list=inventory&q-signature=f77900be432072b16afd8222b4b349aabd837cb9
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
```

#### Response

After the request succeeds, COS returns the following response indicating that currently there are inventory jobs list1 and list2 in the bucket.  

**Inventory job list1**

- Analyze the objects prefixed with `myPrefix` and all their versions in the bucket `examplebucket-1250000000`.
- The frequency of analysis is once a day.
- Analysis dimensions include Size, LastModifiedDate, StorageClass, ETag, IsMultipartUploaded, and ReplicationStatus.
- The analysis results are stored in the bucket `examplebucket-1250000000` as a CSV file, which is prefixed with `list1` and encrypted with SSE-COS.  

**Inventory job list2**

- Analyze the objects prefixed with `myPrefix2` and all their versions in the bucket `examplebucket-1250000000`.
- The frequency of analysis is once a week. The analysis dimensions include Size, LastModifiedDate, StorageClass, and ETag.
- The analysis results are stored in the bucket `examplebucket-1250000000` as a CSV file, which is prefixed with `list2` and encrypted with SSE-COS.  

Suppose there are 100 inventory jobs on this page. If `IsTruncated` is true, COS will further return `NextContinuationToken`, whose value can be used as that of `continuation-token` in a new GET request to get the next page of inventory jobs.

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 331
Date: Mon, 28 Aug 2018 02:53:39 GMT
Server: tencent-cos
x-cos-request-id: NTlhMzg1ZWVfMjQ4OGY3MGFfMWE1NF8****
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

