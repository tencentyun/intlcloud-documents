## Feature Overview

This API is used to query all inventory jobs configured for a bucket. You can configure up to 1,000 inventory jobs for a bucket.  

This request supports returning the results in multiple responses. Each response can contain up to 100 inventory jobs. The value of `IsTruncated` in the request is described as follows:
- If the value of `IsTruncated` is `false`, all inventory jobs of the bucket have been listed.
- If the value of `IsTruncated` is `true` and `NextContinuationToken` carries a value, you can pass this value to `continuation-token` in the next request to obtain the remaining inventory jobs from the next response.

For more information, see [Inventory Overview](https://intl.cloud.tencent.com/document/product/436/30622).

>! To call this API, make sure that you have the required permission for bucket inventory jobs. The bucket owner has the permission by default. If you don’t have it, you must request it from the bucket owner first.
>


<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer (recommended)
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=ListBucketInventoryConfigurations&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                Tencent Cloud API Explorer makes it easy for you to make online API calls, verify signatures, generate SDK code, search for APIs, etc. You can use it to query the request and response of each API call as well as generate sample code for calls.
            </div>
        </div>
    </div>
</div>

## Request

#### Sample request

```shell
GET /?inventory HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>? 
> - In `Host: <BucketName-APPID>.cos.<Region>.myqcloud.com`, <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224)).
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> 

#### Request parameters

The request parameter is as follows:

| Parameter | Description | Type |Required |
| ------------------ | ------------------------------------------------------------ | ------ | ---- |
| continuation-token | If the value of `IsTruncated` is `true` in the last COS response and `NextContinuationToken` carries a value, you can pass this value to `continuation-token` to obtain the inventory jobs in the response. <br>Default value: `None` | String | No |

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

The nodes are described as follows:

| Node Name | Parent Node | Description | Type |
| ------------------------------------ | ----------------------------------- | ------------------------------------------------------------ | --------- |
| List InventoryConfigurationResult | None | Information about all inventory jobs of the bucket | Container |
| InventoryConfiguration | ListInventoryConfigurationResult | Detailed configuration of an inventory job. For the XML structure, see [GET Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30623). | Container |
| IsTruncated | ListInventoryConfigurationResult | Whether all inventory jobs have been listed. If yes, the value is `false`. Otherwise, the value is `true`. | Boolean   |
| ContinuationToken | ListInventoryConfigurationResult | Identifier of the current response. This parameter corresponds to the `continuation-token` request parameter. | String |
| NextContinuationToken | ListInventoryConfigurationResult | Identifier of the next response. You can pass the value of this parameter to `continuation-token` and initiate a GET request to obtain the inventory jobs from the next response. | String    |

#### Error codes

This API returns common error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Examples

#### Request

The following example queries the inventory jobs of the `examplebucket-1250000000` bucket:

```shell
GET /?inventory HTTP/1.1
Date: Mon, 28 Aug 2018 02:53:38 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98JM&q-sign-time=1503895278;1503895638&q-key-time=1503895278;1503895638&q-header-list=host&q-url-param-list=inventory&q-signature=f77900be432072b16afd8222b4b349aabd837cb9
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
```

#### Response

After the request above is made, COS returns the following response, indicating that the inventory jobs `list1` and `list2` are set for the bucket.  

**Inventory job `list1`**

- Objects to analyze: objects prefixed with `myPrefix` and all their versions in the `examplebucket-1250000000` bucket
- Analysis frequency: daily
- Analysis dimensions: `Size`, `LastModifiedDate`, `StorageClass`, `ETag`, `IsMultipartUploaded`, and `ReplicationStatus`
- Analysis result: to be stored in the `inventorybucket-1250000000` bucket as a CSV file, which is prefixed with `list1` and encrypted with SSE-COS.

**Inventory job `list2`**

- Objects to analyze: objects prefixed with `myPrefix2` and labeled `{age:18}` and all their versions in the `examplebucket-1250000000` bucket
- Analysis frequency: once a week<br>Analysis dimensions: `Size`, `LastModifiedDate`, `StorageClass`, `ETag` and `Tag`.
- The result will be stored in the `inventorybucket-1250000000` bucket as a CSV file.  

Assume that 100 inventory jobs are listed in this response. If the value of `IsTruncated` is `true`, COS will return `NextContinuationToken`, whose value can be passed to `continuation-token` for a GET request to obtain the inventory jobs from the next response.

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
                <Bucket>qcs::cos:ap-beijing::inventorybucket-1250000000</Bucket>
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
                <Bucket>qcs::cos:ap-beijing::inventorybucket-1250000000</Bucket>
            </COSBucketDestination>
        </Destination>
        <Schedule>
            <Frequency>Weekly</Frequency>
        </Schedule>
        <Filter>
            <And>
                <Prefix>myPrefix2</Prefix>
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
    <IsTruncated>false</IsTruncated>
    ------If ContinuationToken was provided in the request---
    <ContinuationToken>...</ContinuationToken>
    <IsTruncated>true</IsTruncated>
    <NextContinuationToken>1ueSDFASDF1Tr/XDAFdadEADadf2J/wm36Hy4vbOwM=</NextContinuationToken>
</ListInventoryConfigurationResult>
```

